# 안티패턴 20+ (피해야 할 운영 패턴)

## 1. 과도한 세그먼트 (너무 좁은 타겟팅)

**증상:**
- Ad set 30개+ (동일 오디언스 분산)
- 각 ad set 일일 예산 < $50
- 7일 동안 전환 10개 미만

**왜 실패:**
```
Meta 알고리즘은 마이크로 세그먼트 자동 식별
30개 좁은 타겟 > 1개 넓은 타겟 (성과)

이유: 신호 농축 + 예산 집중 > 분산 학습
```

**교정:**
```
ad set 통합 기준:
├─ 오디언스 차이 < 20% (나이/관심사)
├─ 예산 일일 $100+ (학습 가능)
└─ CBO로 일원화 (Meta 자동 최적화)

결과: ROAS 15~25% 향상
```

---

## 2. 러닝 페이즈 중 편집 (조기 최적화)

**증상:**
- 3일 후 "전환 적음" → 즉시 예산 증가
- 5일 후 "CPA 높음" → 즉시 타겟팅 변경
- 6일 후 "CTR 낮음" → 크리에이티브 스왑

**왜 실패:**
```
Learning Phase = 알고리즘이 신호 축적 중
변경 1회 = 누적 신호 폐기 + 7일 리셋

예시:
  Day 1~3: 신호 20개 축적
  Day 4: 예산 증가 → 신호 0으로 리셋
  Day 5~11: 다시 학습 시작 (7일 낭비)
```

**교정:**
```
Rule: 50 conversions/7days 달성까지 변경 금지

모니터링만 허용:
├─ CPA 추세 확인
├─ CTR 변화 모니터링
└─ Frequency 상승 감시

변경 필요 시:
  → Week 2 (학습 완료 후) 또는
  → 신규 ad set 생성 (기존과 별개)
```

---

## 3. 예산 급변 (20% rule 위반)

**증상:**
- $100/day → $200/day (일괄 증가)
- CPM 급락 기대 → 오히려 CPM 상승
- 예산 증가 후 ROAS 30% 하락

**왜 실패:**
```
$100 → $200 (100% 증가)
= 알고리즘이 "신규 캠페인"으로 인식
= Learning Phase 리셋 + 불완전한 입찰

Meta 2026 권장:
  Week 1: $100
  Week 2: $120 (20% 증)
  Week 3: $144 (20% 증)
  = 2개월에 2배 성장 가능
```

**교정:**
```
정규 스텝업:
├─ 3~5일마다 20% 이하 증가
├─ Meta: 일일 예산 조정
└─ Google: 주간 예산 조정

급격한 증가 필요 시:
→ 신규 캠페인으로 분리 (기존 유지)
```

---

## 4. LTV 무시하고 CAC만 보기

**증상:**
- CAC $50 (훌륭함) = 주간 확대
- 실제 재구매율 5% (매우 낮음)
- 3개월 후 LTV $52 (CAC:LTV = 1:1, 손실)

**왜 실패:**
```
단기 CPA 최적화 ≠ 수익성
저CAC 고객 = 저LTV 가능성 높음

다운마켓 고객의 특성:
├─ 가격 민감도 높음
├─ 재구매율 낮음
├─ 고객생애가치 제한적
```

**교정:**
```
CAC:LTV 비율 관리
├─ 최소 CAC:LTV = 1:3 (권장)
├─ 모니터링: 30일 이상 고객 추적
└─ 월간 LTV 업데이트 (위험 신호 감시)

전략:
  신규획득 추구 광고 (CAC 중시)
  + 리마케팅 (LTV 극대화)
  = 포트폴리오 균형
```

---

## 5. 크리에이티브 동일 반복 (Fatigue 무시)

**증상:**
- 같은 크리에이티브 8주 운영
- Frequency 4.2회/주
- CTR: Week 1 (3.5%) → Week 8 (1.2%)
- CPA 급등 (Week 1 $45 → Week 8 $98)

**왜 실패:**
```
Human Memory:
  7~14일 노출 = 최적 반응률
  14~21일 지나면 = Fatigue 시작
  30일+ = CTR -70%까지 가능

Frequency 3회/주 이상 = 피로 신호
```

**교정:**
```
로테이션 주기:
├─ 2주 단위: 신규 크리에이티브 1개 추가
├─ 4주 단위: 저성과 크리에이티브 제거
└─ 8주 이상: High Performer만 유지

신규 추가 기준:
  Frequency 3.0+ 또는 CTR 20% 급락
```

---

## 6. 어트리뷰션 창 맹신

**증상:**
- 7일 클릭 창만 신뢰
- 실제 고객 여정: 평균 18일
- 초기 Display 클릭의 기여도 0으로 계산
- Display 예산 삭감 → 실제 ROI 높은 채널 손실

**왜 실패:**
```
어트리뷰션 창 ≠ 실제 고객 여정

B2B 예시:
  Day 1: Google Display (인식)
  Day 5: 검색 (관심)
  Day 14: 이메일 (고려)
  Day 18: 웹사이트 (구매)

7일 클릭 창 → Day 1 Display 기여도 0 (오류)
```

**교정:**
```
창 확장:
├─ 기본: 7일 클릭 + 1일 View
├─ 권장: 14일 클릭 (B2C) / 28일 (B2B)
└─ 검증: Incrementality test로 확인

또는:
  Data-Driven Attribution (GA4)
  → Last Click 편향 제거
```

---

## 7. 브랜드 검색어 CPC 낭비

**증상:**
- "우리 회사명" 검색 → CPC $3.50 (일반 검색 $0.40)
- 월간 1,000 검색 × $3.50 = $3,500 낭비
- 자연 검색으로도 70% 전환 가능

**왜 실패:**
```
브랜드 검색 = 이미 고의도 사용자
유료 광고 = 불필요 (자연 검색으로 충분)

효율성:
  Natural Search (Organic): CVR 8%
  Paid Brand Search: CVR 8% (동일)
  → 예산 낭비
```

**교정:**
```
전략:
├─ 브랜드 검색은 "기존 고객만" 타겟
├─ 신규 고객은 제외 (자연 검색 유도)
└─ Branded PMax 금지 (위험)

구현:
  Search Campaign → Negative keywords: [자신의 브랜드]
  (경쟁사 광고 방지만 목표)
```

---

## 8. PMax에 브랜드 키워드 포함

**증상:**
- Google PMax에 모든 키워드 포함
- "삼성" / "LG" / "우리 회사" 혼재
- CPC 급등, ROAS 하락

**왜 실패:**
```
PMax = 광범위 자동 수집 (기본 설계)
브랜드 KW 추가 = "좁혔다고 생각" (착각)

실제:
  Meta PMax 특성: 신규 고객 발굴
  브랜드 KW: 높은 CPC + 낮은 ROI
  → 조합 = 비효율
```

**교정:**
```
Campaign 분리:
├─ Search Campaign (Branded Keywords)
│  └─ "삼성 TV" / "LG 에어컨"
│
└─ PMax Campaign (Category-level)
   └─ "TV 구매" / "에어컨 추천"

PMax에서:
  ✓ 제품 카테고리 추가
  ✓ 행동/관심사 Audience Signal
  ✗ 정확한 키워드 입력
```

---

## 9. Consent Mode v2 미설정 → 신호 70% 유실

**증상:**
- EU/UK 사용자 70% 추적 불가
- GA4 이벤트 부분 손실
- Google Ads Smart Bidding 약화

**왜 실패:**
```
Consent Mode v2 미설정:
  ad_user_data = denied (기본값)
  ad_personalization = denied
  
결과:
  ├─ 리타겟팅 불가 (-60% 채널 손실)
  ├─ GA4 데이터 25~40% 손실
  └─ Smart Bidding 최적화 불가
```

**교정:**
```
즉시 실행:
  Google Tag Manager
  → Consent Mode v2 컨테이너 배포
  → dataLayer 신호 확인
  
체크리스트:
  ✓ ad_storage (쿠키)
  ✓ analytics_storage (GA)
  ✓ ad_user_data (개인정보, 신규)
  ✓ ad_personalization (리타겟, 신규)
```

---

## 10. Pixel 중복 설치

**증상:**
- 동일 "Purchase" 이벤트 2회 기록
- Meta Pixel v1 + v2 동시 설치
- Conversions API 중복

**왜 실패:**
```
중복 이벤트:
  실제 전환 100건
  → 시스템 기록 200건
  → 알고리즘: "전환율 높음" 오판
  → 입찰 과도 → CPA 상승
```

**교정:**
```
검증:
  Meta Events Manager → Test Events
  → 같은 행동 2회 이상 나타나는가?

제거:
  ├─ Pixel v1 삭제 (v2만 유지)
  ├─ CAPI 이벤트 deduplication
  └─ 중복 추적 코드 제거
```

---

## 11. iOS 도메인 검증 누락

**증상:**
- iOS 17+에서 클릭 ID (fbclid) 스트립
- Conversions API 매칭 실패
- 전환 추적 불가 (iOS 광고주 50%)

**왜 실패:**
```
iOS 17.4+ Privacy Policy:
  Domain verification 없음
  → 써드파티 쿠키 및 ID 차단
  
CAPI 매칭 불가:
  fbc/fbp 없음 → 일반화된 이벤트만 추적
```

**교정:**
```
Step 1: Apple App Site Association 파일 업로드
  https://yourdomain.com/.well-known/apple-app-site-association
  
Step 2: Meta Events Manager에서 도메인 검증
  ✓ 상태: "검증됨"
  
Step 3: AEM (Aggregated Event Measurement) 업데이트
  → 최대 8개 우선순위 이벤트 선택
```

---

## 12. 이벤트 매칭율 낮은데 방치

**증상:**
- Pixel 신호 37% (기본)
- Conversions API 신호 없음 (0%)
- "전환 데이터 부족" 알림

**왜 실패:**
```
Pixel만의 한계:
  ├─ 광고 차단 30~50%
  ├─ 쿠키 거부 40~60%
  └─ 추적 신호 37~50%만 수집

결과:
  알고리즘이 "맹" → 의사결정 불가
  → Manual Bidding으로 강등
```

**교정:**
```
즉시 실행:
  Conversions API 배포 (서버 추적)
  
목표:
  Pixel 신호 50% + CAPI 신호 50%
  = 전체 신호 90%+ 수집
  
효과:
  Smart Bidding 활성화 → ROAS 20~30% 향상
```

---

## 13~24. 추가 안티패턴

**13. 캠페인 복제 남발**
- 같은 오디언스로 100개 캠페인
- 예산 분산, 경합 증가 → CPM 2배
- 해법: CBO로 통합

**14. 수동 입찰 고집**
- 기술 부족하다고 AI 입찰 거부
- 해법: tCPA로 시작 (간단)

**15. 시즈널리티 무시**
- Q4 전년도 40% 예산 필요
- 10월부터 테스트 필수
- 해법: 캘린더 기획

**16. 리마케팅 주력 (신규 없음)**
- 신규 고객 0 → 마진율 악화
- 권장: 신규 60% / 리마케팅 40%

**17. 랜딩페이지 최적화 무시**
- 훅 광고 → 평범한 LP → CVR 8%
- 해법: A/B test (제목, 폼)

**18. 오프라인 전환 업로드 안 함**
- 온라인 주문 후 픽업 미추적
- 해법: CRM data upload

**19. 1st-party Data 미수집**
- 3rd-party cookie 단종 → 손실 70%+
- 해법: 이메일 수집, 로그인 권장

**20. 크로스 플랫폼 중복 노출**
- Meta + Google + TikTok 동시
- 같은 유저 3회 노출 → 빈도 과다
- 해법: Frequency cap 설정

**21. B2B인데 LinkedIn 제외**
- 의사결정자 대부분 LinkedIn 활동
- 해법: B2B는 LinkedIn 필수

**22. TikTok에 Meta 광고 재사용**
- 성능 90% 저하 (네이티브 톤 차이)
- 해법: TikTok 전용 UGC 제작

**23. 한국인데 Naver·Kakao 제외**
- 한국 검색의 50~60% Naver 점유
- 해법: 플랫폼 다양화

**24. 자동화 블랙박스 방치 (가드레일 없음)**
- PMax 무한 자동화 → 브랜드 세이프티 위험
- 해법: Audience Signal, Negative keywords 추가

---

**참조**: 
- [측정·트래킹 일체](/sessions/exciting-happy-feynman/media-buying/references/measurement.md)
- [튜닝 플레이북](/sessions/exciting-happy-feynman/media-buying/references/tuning_playbook.md)
- [크리에이티브 설계](/sessions/exciting-happy-feynman/media-buying/references/creative.md)
- [안티패턴 20+](/sessions/exciting-happy-feynman/media-buying/references/antipatterns.md)
- [런칭 체크리스트](/sessions/exciting-happy-feynman/media-buying/references/launch_checklist.md)

