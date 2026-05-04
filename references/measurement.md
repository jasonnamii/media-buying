# 측정·트래킹 일체 (신호 붕괴 시대 복구 전략)

## 1. 시그널 붕괴 시대 개요

2026년 4월 현황:
- **iOS ATT 옵트인율**: 35~50% (추적 불가 50~65%)
- **글로벌 전환 손실**: 30~60% (브라우저·OS 제약)
- **패러다임**: 개별 추적 → 다층 신호 수집 + 통계 복원 + 확률 모델링

**한국 인하우스 체크**:
- Consent Mode v2 배포 여부? (EU 필수, 한국 선택)
- CAPI 운영 여부? (Meta 픽셀 차단 시 대체)
- 1st-party CRM 구축 여부? (3rd-party cookie 단종 대비)

---

## 2. 3축 복구 전략

```
신호 손실 30~60%
├─ 서버측 추적 (Server-side GTM + CAPI)
│  └─ 데이터 손실 <5% (브라우저 우회)
│
├─ 동의 신호 보존 (Consent Mode v2)
│  └─ EU/UK DMA 강제, 한국 GDPR 대비
│
└─ 1st-party 데이터 (Customer Match + CRM)
   └─ 3rd-party cookie 폐지 대비
```

**실무 우선순위**:
1. Meta CAPI 즉시 배포 (Pixel 신호 37% → 70% 복원 가능)
2. Server-side GTM 컨테이너 구축 (BigQuery 통합)
3. Consent Mode v2 구현 (향후 필수)

---

## 3. iOS SKAN 4.0 상세 가이드

### 3.1 Source ID (4자리 캠페인 식별)

| 신호 레벨 | Source ID | 정보도 | 용도 |
|----------|-----------|-------|------|
| 4-digit | `0000`~`1111` | 캠페인 완전 구분 | 일반 (고볼륨) |
| 2-digit | `XX00` | 캠페인군만 식별 | 중간 볼륨 |
| 0-digit | 제공 안함 | 완전 애그리게이션 | 저볼륨 (프라이버시) |

**프라이버시 임계값 (Privacy Threshold)**:
- Apple이 자동 결정 (설치 볼륨 기반)
- 마케터는 수신 후 처리 로직 준비

### 3.2 Conversion Value: Fine vs. Coarse

**Fine-Grained (6비트 = 0~63)**
```
구매액 버킷 매핑:
0~20:   저가 상품 ($1~$50)
21~40:  중가 ($51~$200)
41~63:  고가 ($201+)
→ Smart Bidding이 고가 구매 학습
```

**Coarse-Grained (분류형)**
- Apple 자동 버켓팅: `none` / `low` / `medium` / `high`
- 세분도 부족 → 역추정 모델링 필요

### 3.3 Postback 타이밍 (0/1/2 차수)

```
사용자 여정:
Day 0: 앱 설치 → Postback 0 발송 (즉시, 신뢰도 90%)
Day 1~2: 재참여 활동 → Postback 1 (24시간 이내)
Day 24~100: 목표 달성 → Postback 2 (최종 전환)
```

**실무**: 각 postback의 신뢰도·볼륨을 분리 추적, Time-decay 어트리뷰션 적용

---

## 4. Consent Mode v2 (Google)

### 4.1 4가지 신호 구조

```javascript
// dataLayer 구현
gtag('consent', 'update', {
  'ad_storage': 'granted' | 'denied',        // 광고 쿠키
  'analytics_storage': 'granted' | 'denied',  // GA 쿠키
  'ad_user_data': 'granted' | 'denied',       // 개인정보 송신 (신규)
  'ad_personalization': 'granted' | 'denied'  // 리타겟·유사 대상 (신규)
});
```

### 4.2 실무 매트릭스

| 권한 조합 | 영향도 | 실행 전략 |
|----------|-------|---------|
| 모두 거부 | 리타겟 -60% | 모델링만 의존 |
| Storage만 | 어트리뷰션 60% | 기본 추적 가능 |
| Storage + 개인정보 | 리타겟 가능 | Search Ads OK |
| 완전 허용 | 100% | 풀 기능 (EU 검증) |

### 4.3 EU DMA 의무사항

- EEA/UK 사용자 → Consent Mode v2 필수
- Basic 신호만으로도 기본 추적 가능
- Advanced 신호로 Smart Bidding·모델링 활성화
- API 폐지 → Data Manager 강제 전환 (2026년 4월)

---

## 5. CAPI (Meta Conversions API)

### 5.1 3단계 구현 구조

```
Step 1: 웹사이트 이벤트 수집 (클릭·구매)
        ↓
Step 2: 서버에서 정규화 (이메일 SHA256 해싱)
        ↓
Step 3: CAPI 전송 (브라우저 우회, 신호 손실 최소)
```

### 5.2 필수 데이터 세트

```python
# 최소 구현
{
  "event_name": "Purchase",           # 표준: Purchase/AddToCart/ViewContent
  "event_time": 1617361200,           # Unix timestamp
  "user_data": {
    "em": "hashed_email",             # SHA256
    "ph": "hashed_phone",
    "fbc": "fb.1.xxx_fbclid",         # Facebook Click ID
    "fbp": "fb.1.yyy"                 # Facebook Pixel ID
  },
  "custom_data": {
    "value": 142.52,
    "currency": "USD",
    "content_name": "Product ABC"
  }
}
```

### 5.3 2026년 Meta 업데이트

- Events Manager 원클릭 CAPI 설정
- AI 기반 페이지 자동 추출 (title, price)
- **권장**: Pixel + CAPI 이중 운영 (보수적 신호 세트)

**매칭율 목표**: 70%+ (Pixel 신호와 Server-side 통합)

---

## 6. Enhanced Conversions (Google)

### 6.1 작동 원리

```
웹사이트 (고객 이메일·전화·주소)
  ↓
SHA256 해싱 (개인정보 미전송)
  ↓
Enhanced Conversion Tag
  ↓
Google Ads (해시만 전달)
  
효과: 5~15% 추가 전환 복원
```

### 6.2 설정 체크리스트

- [ ] GTM Variable: 이메일, 전화 수집
- [ ] Enhanced Conversion Trigger 생성
- [ ] Event parameter: `user_data` 해시 포함
- [ ] Smart Bidding 활성화 확인

**주의**: 미설정 시 → "전환율 낮음" 오판 → 예산 삭감 → 실제 ROI 높은 캠페인 손실 20~30%

---

## 7. Server-side GTM & BigQuery 통합

### 7.1 아키텍처

```
클라이언트 (브라우저/앱)
  ↓
Server-side GTM (Google Cloud 호스팅)
  ├→ GA4
  ├→ Meta Conversions API
  ├→ Google Ads Enhanced
  ├→ Segment/Mixpanel
  └→ BigQuery (원본 데이터 보존)
  
이점:
- 데이터 손실 <5% (서버에서 처리)
- 거부 추적 우회
- GDPR/DPA 컴플라이언스
```

### 7.2 Firebase + Server GTM (2024년 10월 공식)

```
Firebase SDK (iOS/Android)
  ↓
Server GTM 수신
  ↓
GA4 + CAPI + BigQuery 분산
```

---

## 8. First-party Data 활용 (Customer Match)

### 8.1 2026년 4월 API 변경

**Google Ads API → Data Manager API 이행**

체크리스트:
- [ ] CRM 고객 이메일 세그먼트 추출
- [ ] 포맷 표준화 (phone: +1 2025551234)
- [ ] Data Manager에서 Audience 생성
- [ ] ActiveCampaign·HubSpot 커넥터 활용 (자동 동기)

### 8.2 허용 데이터 유형

| 신원 방식 | 예시 | 신뢰도 |
|---------|------|-------|
| 이메일 | user@example.com | 85% |
| 전화 | +1 202-555-1234 | 70% |
| 우편 주소 | Seoul, ZIP | 60% |
| 모바일 AD ID | AEBE52E7-03EE-455A... | 92% |

---

## 9. GA4 Event-Based Attribution

### 9.1 DDA (Data-Driven Attribution) 요건

```
필수 조건:
├─ 핵심 이벤트: 최소 400 전환
├─ 전체 이벤트: 최소 20,000개
└─ 기간: 30일 lookback

효과:
  Last Click: 전환 100% → Search 60%
  DDA: 재분배 → Display 35% / Search 65%
```

### 9.2 2026년 신기능: Conversion Attribution Analysis

- **Assisted Conversions**: 마지막 클릭 외 기여도 시각화
- **Funnel Stage**: Early (인지) / Mid (관심) / Late (결정) 분리

**사용처**: 브랜드·Display의 숨은 기여도 정량화 → 예산 최적화

---

## 10. MMP (Mobile Measurement Partners) 선택

### 10.1 주요 플레이어 비교

| MMP | 시장점유 | 강점 | 약점 | 추천 대상 |
|-----|--------|------|------|---------|
| **AppsFlyer** | 65% | OneLink·글로벌 | 높은 비용 | 유니콘·엔터프라이즈 |
| **Adjust** | 25% | 자체 인프라·맞춤 | 오버스펙 | 초고볼륨·독립성 |
| **Singular** | 8% | 1000+ 통합 | 한국 약함 | 멀티채널 |
| **Kochava** | 2% | SKAdNetwork·사기탐지 | 소형 | 사기 높은 지역 |

### 10.2 선택 로직

```
월간 설치 기준:
- 10,000+ → AppsFlyer
- 5,000~10,000 → Adjust
- 전채널 통합 필요 → Singular
```

---

## 11. 어트리뷰션 모델 선택 기준표

| 모델 | 정의 | 사용 캠페인 | 주의점 |
|-----|------|----------|-------|
| **Last Click** | 마지막 터치 100% | 전환 최적화 초기 | 상위퍼널 무시 |
| **First Click** | 첫 터치 100% | 브랜드·인지 | 관심→결정 누락 |
| **Linear** | 균등 분배 | 신제품·미지 | 심리 무시 |
| **Time Decay** | 최근 가중 | 성숙 제품·리타겟 | 상위퍼널 저평가 |
| **Data-Driven** | ML 기반 | 월 4000+전환 | 데이터·비용 필요 |
| **Position-based** | 첫/마지막 40%, 중간 20% | 균형잡힌 분석 | 복잡도 |

**한국 기본값**: Last Click → Time Decay → DDA 순 도입

---

## 12. Incrementality Testing (4가지 방법)

### 12.1 Geo Test (지역 분할)

```
Test: 서울 (광고 100%)  → 1000 전환
Control: 인천 (광고 0%) → 100 전환 (자연)

순증가 = (1000 - 100) / 100 = 900%
(실제는 세운데 시장차이 보정 필수)
```

장점: GDPR 친화, 개별 추적 불필요
한계: 지역 차이, 경계 누수

### 12.2 Ghost Bid (RTB)

입찰은 하지만 노출 안 함 → Control Group 활용

### 12.3 PSA Test (공익광고)

실제 광고 vs 비관련 광고 치환 → 명확한 인과

### 12.4 Holdout Group (매출 포기)

광고 없음 (10%) vs 정상 노출 (90%) → 정확도 최고

---

## 13. MMM (Marketing Mix Modeling)

### 13.1 Meta Robyn vs. Google Meridian

| 기준 | Robyn | Meridian |
|------|-------|---------|
| 알고리즘 | Ridge Regression | Bayesian MCMC |
| 학습곡선 | 중간 | 높음 |
| 비용 | 낮음 (GitHub) | 높음 (GCP+전문가) |
| 데이터 | Meta 최적 | Google 최적 |

**실무 선택**:
- Meta 지출 > Google → Robyn
- Google 지출 > Meta → Meridian
- 시작 → Robyn (진입장벽 낮음)

### 13.2 필수 데이터

```
├─ 미디어 지출 (채널별·주단위)
├─ KPI (매출·설치·비용)
├─ 외부 변수 (계절성·프로모션)
└─ 최소 2년 데이터 + 월간 500만원 이상
```

---

## 14. Clean Rooms (ID 매칭)

### 14.1 3가지 플랫폼

**Google Ads Data Hub**
- YouTube·Search 인벤토리 접근
- 제약: Google 자체 인벤토리만

**Amazon Marketing Cloud (2025년 9월 무료화)**
- Sponsored Ads 광고주 자동 접근
- DSP 최적화

**LiveRamp Safe Haven**
- 독립 플레이어, 1000+ 파트너
- 최대 유연성

---

## 15. 런칭 전 측정 체크리스트 (20항목)

### Phase 1: 신호 보호 (1주)

- [ ] GA4 Server-side GTM 컨테이너 생성
- [ ] Firebase 이벤트 → GTM Server 라우팅
- [ ] Meta CAPI 설정 (Events Manager)
- [ ] Google Enhanced Conversions 활성화
- [ ] Consent Mode v2 dataLayer 구현

### Phase 2: 데이터 재구성 (2주)

- [ ] GA4 DDA 활성화 (전환 400개 확인)
- [ ] Conversion Attribution Analysis 리뷰
- [ ] Customer Match → Data Manager 마이그레이션
- [ ] CRM 고객 세그먼트 추출·동기 자동화
- [ ] 채널별 어트리뷰션 모델 선택 (Time Decay 권장)

### Phase 3: 고급 분석 (3주)

- [ ] MMP 선택·구현
- [ ] 인크리멘탈리티 테스트 설계
- [ ] MMM 파일럿 (선택)

### Phase 4: 조직화 (4주)

- [ ] 어트리뷰션 리뷰 주기 정립
- [ ] 채널별 ROAS·기여도 대시보드
- [ ] Attribution → 예산 배분 반영
- [ ] 팀 역량 강화 (GA4·서버기술·통계)
- [ ] Data Governance 문서화

---

**참조**: 
- [측정·트래킹 스포크](/sessions/exciting-happy-feynman/media-buying/references/measurement.md)
- [튜닝 플레이북](/sessions/exciting-happy-feynman/media-buying/references/tuning_playbook.md)
- [크리에이티브 설계](/sessions/exciting-happy-feynman/media-buying/references/creative.md)
- [안티패턴 20+](/sessions/exciting-happy-feynman/media-buying/references/antipatterns.md)
- [런칭 체크리스트](/sessions/exciting-happy-feynman/media-buying/references/launch_checklist.md)

