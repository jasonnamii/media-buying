# 런칭·주간·월간·시즈널 체크리스트 (프리런칭~사후분석)

## § 1. 프리런칭 체크리스트 (22항목)

### 목표·KPI 정의

- [ ] **캠페인 목표 확정**: 신규 획득 / 리마케팅 / 브랜드 인지
- [ ] **KPI 설정**: CPA / ROAS / CVR / CTR / CPL (리드)
- [ ] **기간별 목표치**:
  - 주간: CPA $XX, ROAS Y:1
  - 월간: 전환 ZZ건, 예산 효율
  - 분기: LTV 추적, 재구매율

### 구조 설계

- [ ] **계정 구조 (Media Hierarchy)**:
  ```
  Campaign 
    ├─ Campaign 1 (신규 콜드)
    ├─ Campaign 2 (리마케팅)
    └─ Campaign 3 (Lookalike)
  
  각 Campaign → Ad Set 분리
  각 Ad Set → 4~6 Creative
  ```
- [ ] **네이밍 컨벤션**: campaign_type_date_version
  - 예: `2026-04_newuser_cold_v1`
- [ ] **예산 배분**:
  - 일일 예산 (Ad set별)
  - 캠페인 총액
  - 주간 총액
- [ ] **오디언스 정의**:
  - Lookalike (고객 유사)
  - Interest-based (관심사)
  - Behavior (구매 이력)

### 크리에이티브 자산

- [ ] **최소 자산 개수**:
  - Meta: 4~6 광고 / ad set
  - TikTok: 3~5
  - Google PMax: 완전 Asset Group (15 Headlines·5 Descriptions·Images·Video)
- [ ] **스펙 확인**:
  - Meta: 1080x1920 (9:16)
  - TikTok: Full-HD 9:16
  - YouTube: 수직 영상 우선
- [ ] **Hook rate 기준**: 최소 25% 예상
- [ ] **UGC vs. 브랜드필름 비율**: UGC 50% 이상 권장

### 추적·측정 설정

- [ ] **Meta Pixel**:
  - [ ] 웹사이트 설치 완료
  - [ ] Test Event 검증 (클릭 → 전환 실시간 확인)
  - [ ] Conversion Event 선택 (Purchase / Lead / ViewContent)

- [ ] **Conversions API (CAPI)**:
  - [ ] 서버 이벤트 설정
  - [ ] 웹훅 또는 API 연동
  - [ ] 매칭율 목표 70%+

- [ ] **Google Conversions**:
  - [ ] Google Conversion Tag 설치 (ga4_send_purchase)
  - [ ] Enhanced Conversions 활성화

- [ ] **Consent Mode v2**:
  - [ ] dataLayer 신호 구현
  - [ ] EU/UK 사용자 동의 추적

- [ ] **iOS 도메인 검증**:
  - [ ] apple-app-site-association 파일 업로드
  - [ ] AEM (Aggregated Event Measurement) 우선순위 8개 선택

- [ ] **서버측 GTM (선택)**:
  - [ ] Firebase → Server GTM → GA4·CAPI 라우팅
  - [ ] BigQuery 통합 (원본 데이터 보존)

### 데이터·개인정보

- [ ] **UTM 파라미터**:
  ```
  구조: ?utm_source=meta&utm_medium=cpc&utm_campaign=newuser_cold_v1
  검증: GA4에서 각 캠페인별 추적 가능한가?
  ```

- [ ] **고객정보 정책**:
  - [ ] 개인정보처리방침 업데이트 (Pixel 사용 명시)
  - [ ] 쿠키 배너 설치 (EU 필수)
  - [ ] CRM 고객 리스트 준비 (Customer Match용)

### 랜딩페이지

- [ ] **성능**: 로드 속도 < 3초
- [ ] **모바일 최적화**: 반응형 디자인 확인
- [ ] **CVR 기준**: 최소 1~3% 예상
- [ ] **CPP (Custom Product Pages)**: 고가 제품은 CPP 활용 (Google)
- [ ] **A/B 테스트 준비**:
  - 폼 길이 (3항목 vs 7항목)
  - 제목 (이익 vs 호기심)
  - 이미지 (제품 vs 사람)

### 브랜드·안전성

- [ ] **Brand Safety**:
  - [ ] Negative Keywords 설정 (경쟁사·금지어)
  - [ ] Negative Audiences 제외 (이미 구매한 고객)
  - [ ] Brand Exclusion (PMax에서 자사 제외)

- [ ] **정보 검증**:
  - [ ] 제품·가격·배송 정보 정확
  - [ ] 약관·환불 정책 명시
  - [ ] 연락처·AS 정보 제공

### 대시보드·모니터링

- [ ] **GA4 대시보드 설정**:
  - 조회: Acquisition 채널별 ROAS
  - 전환: 이벤트별 CVR
  - 어트리뷰션: DDA 모델 비교

- [ ] **Platform 대시보드**:
  - Meta: Campaign performance (ROAS, CPA, Frequency)
  - Google: Campaign insights (Conversion rate)
  - TikTok: Campaign analytics (CTR, Conversion)

- [ ] **실시간 알림 설정**:
  - CPM 3배 이상 상승 → 일일 알림
  - CVR < 0.5% → 경고
  - 예산 소진율 > 120% → 주의

### 최종 승인

- [ ] **마케팅 팀 검토**: 캠페인 목표·전략 승인
- [ ] **브랜드 팀**: 크리에이티브·톤 검수
- [ ] **법무·개인정보**: 정책·약관 확인
- [ ] **재무**: 예산 배정 확인

### 론칭 직후 (72시간)

- [ ] **클릭 테스트**: 수동 광고 클릭 → 전환 경로 검증
- [ ] **이벤트 정확성**: GA4·Meta 이벤트 비교
- [ ] **Pixel 신호**: Pixel 신호 > 30% 확인?
- [ ] **첫 전환**: 이벤트 정상 기록되는가?

---

## § 2. 주간 루틴 (월요일 의례)

### 성과 데이터 정리

```
Metrics to review:
├─ ROAS (목표 대비)
├─ CPA (추이 확인)
├─ CTR (주대비)
├─ CVR (이벤트별)
├─ Frequency (피로도)
└─ Cost (예산 소진)

표: [캠페인] | ROAS | CPA | CTR | CVR | Freq | 상태
```

### 크리에이티브 상태

- [ ] **Hook Rate 확인**: 25% 이상?
- [ ] **Top 3 / Bottom 3 식별**:
  - Top: ROAS > 3:1 → 유지·확대
  - Bottom: ROAS < 1.5:1 → 중단
  - Mid: 모니터링 계속

- [ ] **피로도 신호**:
  - Frequency 3.5회/주 이상? → 신규 크리에이티브 추가
  - CTR 20% 급락? → 로테이션 시작

### 러닝 상태 (Learning Phase)

- [ ] **50 conversions/7days 달성 여부**:
  - 미달: 원인 진단 (신호부족? 오디언스? 크리에이티브?)
  - 달성: 축하, 학습 완료 상태 전환

- [ ] **학습 중 변경 기록**:
  - 어떤 변경 없었는가? (아무것도 변경 금지)
  - 변경 있었다면: 리셋 시간 계산

### 신호 정합성

- [ ] **Pixel 신호**: 37% 이상?
- [ ] **CAPI 매칭율**: 70% 이상?
- [ ] **Meta vs. GA4 비교**: 전환 차이 < 15%?
- [ ] **어트리뷰션 창**: 의도한 설정 유지 (7일 클릭 vs 28일)?

### 오디언스 갱신

- [ ] **Remarketing 오디언스 갱신**:
  - 방문자 리스트 업데이트
  - 카트 포기 오디언스 생성
  - 구매자 제외 (이중 타겟 방지)

- [ ] **Customer Match 갱신** (선택):
  - CRM 최신 고객 리스트 업로드
  - 자동 동기 설정 (Salesforce·HubSpot)

### 실행 항목

- [ ] **신규 크리에이티브 필요?**: Week 2~4 로테이션 계획
- [ ] **예산 조정**: 20% rule 준수하며 스텝업?
- [ ] **오디언스 확대**: 전환 50개 달성 후 오디언스 크기 1.5배
- [ ] **캠페인 추가**: 테스트 캠페인 신규 시작?

---

## § 3. 월간 리뷰 (월 1회, 보통 말일)

### Week 1: Data Audit

```
Action Items:
[ ] 전환 이벤트 정확성 (수동 재검증)
    └─ 샘플 100건 구매 데이터 대조
[ ] Pixel vs CAPI 비율 분석
    └─ 추천 비율: 50:50 (신호 다각화)
[ ] 중복 이벤트 제거 여부 확인
    └─ Event Deduplication ID 활성화?
[ ] GA4 DDA 데이터 수집 여부
    └─ 400+ 전환·20K+ 이벤트 충족?
```

### Week 2: Campaign Hygiene

```
Action Items:
[ ] 저성과 캠페인 중단
    └─ ROAS < 2:1인 캠페인 중단 계획
[ ] 중복 캠페인 통합
    └─ 같은 오디언스 여러 캠페인 → CBO로 일원화
[ ] 오디언스 규모 재검증
    └─ Lookalike < 1M (너무 좁음) 또는 > 10M (너무 넓음)?
[ ] Negative Keywords 추가
    └─ 저성과 검색어·경쟁사 제외
```

### Week 3: Creative Analysis

```
Deep Dive:
[ ] Hook Rate 벤치마크 분석
    └─ 월간 평균 < 25%? → 크리에이티브 질 검토
[ ] Diversity Score 평가
    └─ 목표: 6~8/10 (Meta)
    └─ 미달: 스타일·톤·포맷 다양화
[ ] A/B Test 결과 검증
    └─ 통계 유의성 95% 달성?
    └─ 승리자 식별 & 학습 전이
[ ] 신규 크리에이티브 Roadmap
    └─ 다음주 추가할 3~5개 크리에이티브 큐
```

### Week 4: Strategy & Forecast

```
Strategic Planning:
[ ] 월별 성과 요약
    └─ ROAS | CAC | LTV | 재구매율 종합
[ ] 채널별 기여도 분석
    └─ DDA 모델 기반 예산 재배분 제안
[ ] Incrementality Test 설계 (선택)
    └─ 인크리멘탈리티 테스트 필요한가?
    └─ 설계: Geo test / Holdout / PSA 선택
[ ] 분기 목표 대비 진도율
    └─ Q2 목표의 몇 % 달성?
    └─ Q3 계획 조정 필요?
```

---

## § 4. 시즈널 대응

### Q4 (Black Friday · Cyber Monday · 연말)

#### 10월: 준비 및 테스트

```
Timeline:
Week 1~2:
  [ ] BFCM 크리에이티브 제작 시작
  [ ] 인벤토리 확보 검증
  [ ] 가격 정책 최종 확정

Week 3~4:
  [ ] Early Test Campaign 시작 (저예산)
    └─ "조기 할인" 또는 "프리뷰" 오퍼
  [ ] 광고·랜딩페이지 성능 모니터링
  [ ] 예상 ROAS 기준 설정
```

#### 11월: 피크 집중

```
Timeline:
11월 1~7일:
  [ ] Holiday Creative 라이브 (11월 1일부터 실행)
  [ ] Budget 상향 (평년의 150% 이상)
  [ ] Frequency Cap 완화 (2→5회/주)

11월 8~15일:
  [ ] Black Friday Preview (미국)
  [ ] 예산 추가 (최대 200%)
  [ ] 신규 오퍼 테스트 (가격 vs 번들)

11월 16~30일:
  [ ] Cyber Monday 본격화
  [ ] 예산 집중 (월 40% 지출)
  [ ] Creative 초고속 로테이션 (3~4일마다 신규)
```

#### 12월: 연말 피크

```
Timeline:
12월 1~14일:
  [ ] Budget 평년 유지 (Q4 추가 예산 소진)
  [ ] Evergreen gift-giving 크리에이티브

12월 15~24일:
  [ ] 최고 피크 (선물 구매 절정)
  [ ] Budget 최대 (예산 40% 집중)
  [ ] 배송 마감 강조 ("배송은 12월 20일까지")

12월 25~31일:
  [ ] 반품·교환 준비
  [ ] 고객 서비스 강화 안내
  [ ] 예산 감소 (신년 준비)
```

#### 1월: 사후분석

```
Action Items:
[ ] Q4 전체 성과 집계
    └─ ROAS | 총 매출 | CAC | LTV
[ ] 환불 데이터 분석
    └─ 환불율 > 10%? 제품 이슈?
[ ] 재구매 고객 식별
    └─ "충성 고객" 리마케팅 세그먼트 생성
[ ] 1월 신규 캠페인 계획
    └─ New Year's Resolution (운동·다이어트)
```

### 한국 시즈널 (설·추석·연중 이벤트)

| 시즈널 | 기간 | 예산 조정 | 크리에이티브 |
|--------|------|----------|----------|
| **설 (2월)** | 2/1~2/15 | +30% | 선물·명절 감성 |
| **3월** | 신학기 이벤트 | +20% | 새학기·개학 |
| **어린이날·가정의달** | 4/24~5/15 | +20% | 가족·아이 감성 |
| **추석 (9월)** | 9/1~9/30 | +30% | 선물·가족 시간 |
| **10월** | Halloween (한국 미약) | 기본 | - |
| **11~12월** | BFCM·연말 | +50% | 위의 Q4 참조 |

---

## § 5. 위험 신호 & 대응 (상시)

### 성과 급변

| 신호 | 원인 진단 | 대응 |
|------|---------|------|
| **CPA 50% 상승** | · 신호 손실? · 크리에이티브 피로? · 경합 증가? | · Pixel 검증 · 신규 크리에이티브 · 예산 감소 |
| **CTR 20% 급락** | · 피로도 · 오디언스 포화 | · 로테이션 · 오디언스 확대 |
| **CVR < 0.5%** | · LP 이슈 · 모바일 성능 | · LP 최적화 · 폼 단축 |
| **Frequency 4.0+** | · 피로 신호 | · 신규 크리에이티브 추가 |

---

## § 6. 문서화·아카이빙

### 캠페인 백업

```
구조:
├─ Campaign Creative (이미지·영상 파일)
├─ Campaign Brief (목표·타겟·메시지)
├─ Performance Data (월별 ROAS·CPA)
└─ Learnings (무엇을 배웠는가?)

저장소: Google Drive / Notion / 올리브영 Wiki
```

### Institutional Knowledge

- [ ] 크리에이티브 성공 사례 정리
- [ ] 실패한 오디언스/오퍼 기록
- [ ] 시즈널별 ROAS 벤치마크 저장
- [ ] 팀 회고: "이번 달 가장 큰 배움"

---

**참조**: 
- [측정·트래킹 일체](/sessions/exciting-happy-feynman/media-buying/references/measurement.md)
- [튜닝 플레이북](/sessions/exciting-happy-feynman/media-buying/references/tuning_playbook.md)
- [크리에이티브 설계](/sessions/exciting-happy-feynman/media-buying/references/creative.md)
- [안티패턴 20+](/sessions/exciting-happy-feynman/media-buying/references/antipatterns.md)
- [런칭 체크리스트](/sessions/exciting-happy-feynman/media-buying/references/launch_checklist.md)

