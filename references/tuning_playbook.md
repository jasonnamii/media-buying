# 운영 튜닝 플레이북 (러닝·예산·입찰·크리에이티브)

## 1. 러닝 페이즈 관리

### 1.1 플랫폼별 러닝 임계값

| 플랫폼 | 임계값 | 기간 | 주의사항 |
|--------|-------|------|---------|
| **Meta** | 50 전환 / 7일 / ad set | 7~14일 | 변경 금지 (리셋) |
| **Google PMax** | 학습 기간 2~3주 | 14~21일 | Audience signal 공급 |
| **TikTok Smart+** | 50 전환 / 7일 | 10~14일 | Early indicator 신호 양호 |

### 1.2 러닝 중 금지 사항

```
❌ 예산 20% 이상 변경
❌ 타겟팅 수정
❌ 최적화 이벤트 변경
❌ 크리에이티브 스왑
❌ 입찰 전략 변경

⚠️ 모든 변경 = 신호 폐기 + 7일 리셋
```

### 1.3 러닝 실패 원인 5가지

1. **신호 부족**: CPA 높은데 전환 50개 미달
2. **오디언스 부적절**: 인구통계·관심사 맞지 않음
3. **크리에이티브 약함**: Hook rate 15% 미만
4. **랜딩페이지 이슈**: CVR < 1%
5. **가격·제품 문제**: "너무 비쌈" 피드백

**진단 플로우**:
```
러닝 7일 후 50 전환 미달?
├─ CPA 정상 → 신호 충분, 유지
├─ CPA 높음 + CTR 낮음 → 크리에이티브 변경
├─ CTR 높은데 CVR 낮음 → 랜딩페이지 최적화
└─ 트래픽 자체 적음 → 오디언스 확대
```

---

## 2. 입찰 전략 선택 트리

```
전환량 많은가?
├─ 아니오 → Max Conversions 금지
│          └─ Budget Cap 또는 Cost Cap 선택
│
├─ 예 (충분) → 가치 추적 가능?
│  ├─ 아니오 → tCPA (전환당 목표가)
│  │          └─ Meta: 50 conversions/7d 필요
│  │
│  └─ 예 → tROAS (수익 기반)
│          └─ Google: Target ROAS 권장
│
└─ 저전환 단기 테스트 → Manual Bidding 또는 Bid Cap
```

### 2.1 세 가지 입찰 한도 비교

| 입찰 방식 | 성질 | 사용 시기 | 유연성 |
|---------|------|---------|-------|
| **Cost Cap** | 평균 목표 | 예산 여유·변동성 OK | 높음 |
| **Bid Cap** | 최대값 보호 | 프리미엄 배치·과입찰 방지 | 중간 |
| **Target CPA** | 정확도 | 충분한 데이터·안정적 | 낮음 |

---

## 3. 예산 스텝업 규칙

### 3.1 Meta 20% Rule (2026 유효)

```
$100 → $120 (20% 증가, OK)
$100 → $150 (50% 증가, ❌ 학습 리셋)

주기: 3~5일마다
누적: 월간 60% 정도 성장 가능
```

**예시 스케줄**:
```
Week 1: $100/day × 7 = $700
Week 2: $120/day × 7 = $840 (20% 증)
Week 3: $144/day × 7 = $1,008 (20% 증)
Week 4: $173/day × 7 = $1,210 (20% 증)
Month: ~$3,758 (월 5배 성장)
```

### 3.2 Google PMax 스텝업

- 15~20% 증분, 7~14일 간격
- 급격한 2배 증가 → 1~2주 성능 급락
- 현실적 스케일링: 8~10주에 2배

### 3.3 스케일 실패 신호

```
CPA 50% 이상 상승 (1주)
└─→ 오디언스 포화 또는 경합 증가
└─→ 해법: 오디언스 확대 또는 크리에이티브 변경
```

---

## 4. CPA 급등 대응 프로토콜 (4단계)

### Stage 1: 시그널 점검 (당일)

- [ ] Pixel/CAPI 신호 정상? (Pixel 37%+ ?)
- [ ] 어트리뷰션 창 변경? (7일 vs 28일)
- [ ] iOS 옵트인율 급락? (38% → 20%)

**결과**: 신호 정상 → Stage 2로

### Stage 2: 크리에이티브 점검 (1~2일)

- [ ] Hook rate 25% 이상?
- [ ] 최근 3주 내 신규 크리에이티브 추가?
- [ ] Top performer 제거됨?

**결과**: 신규 크리에이티브 추가 필요 → 신규 3~5개 제작 시작

### Stage 3: 타겟 범위 점검 (2~3일)

- [ ] 오디언스 남은 규모? (<100K 위험)
- [ ] 이전주 예산 증가분? (20% rule 준수?)
- [ ] Frequency 상승? (3.5회/주 이상 위험)

**해법**: 오디언스 확대 또는 예산 감소

### Stage 4: 경쟁 점검 (3~5일)

- [ ] Google Trends: 관심사 트렌드 변화?
- [ ] 경합사 캠페인 증가?
- [ ] 계절성 영향? (특정 시간대 피크)

**해법**: 입찰 전략 조정 (Bid Cap 인상) 또는 채널 분산

---

## 5. 빈도 관리 & 피로도

### 5.1 Healthy Frequency Benchmarks (주당)

| 오디언스 타입 | 권장 범위 | 경고 | 피로 시작 |
|------------|---------|------|---------|
| 콜드 신규 | 1.5~2.5회 | 3.0+ | 4.0+ |
| 따뜻한 잠재고객 | 2.5~4.0회 | 5.0+ | 6.0+ |
| 리타겟팅 | 5~10회 | 12+ | 15+ |
| 고관여 (B2B) | 3~7회 | 8+ | 10+ |

### 5.2 피로도 신호

```
Frequency 3+ → CTR 급락 (-15~20%)
             → CPM 상승 (+20~30%)
             → ROAS 악화

해법: 신규 크리에이티브 즉시 추가
```

### 5.3 Frequency Cap 설정

```
Meta: Ads Manager → Ad Set → Frequency Cap
└─ 추천: 콜드 2회/7일, 리마케팅 8회/7일

Google: Campaign → Frequency Capping
└─ 추천: 콜드 3회/7일, 리마케팅 10회/7일
```

---

## 6. 크리에이티브 로테이션 주기

### 6.1 운영 주기

```
2~4주마다 신규 3~5개 추가
├─ High Performer: 6~8주 유지
├─ Mid Performer: 4주 모니터링
└─ Low Performer: 2주 후 중단

"Diversity Score" 목표:
Meta: 6~8/10 (다양성 양호)
```

### 6.2 Evergreen vs. Seasonal 구분

| 유형 | 생명주기 | 로테이션 |
|------|--------|---------|
| **Evergreen** | 3~6개월 | 월 1회 신규 추가 |
| **Seasonal** | 4~8주 | 주 1회 신규 추가 |
| **Trending** | 1~2주 | 거의 매일 |

---

## 7. A/B 테스트 원칙

### 7.1 Meta Experiments

**실험 시작 기준**:
- 최소 7~14일 운영
- 일일 예산 $100+/variant
- 95% 신뢰도 목표

**Best Practice**:
- 단일 변수만 테스트
- 최소 100 전환/variant
- 고위험: 300~400 전환

### 7.2 Google Experiments (PMax)

**기간**: 4~6주 (표준)
**표본**: 최소 100 전환/variant (기본) / 300~400 (고위험)

### 7.3 A/B vs. Incrementality 차이

| 방법 | 측정 | 신뢰도 | 비용 |
|------|------|-------|------|
| **A/B Test** | 상대 성능 | 70% | 낮음 |
| **Incrementality** | 순증가 (인과) | 90% | 높음 |

**선택**: 신뢰도 중요 → Incrementality / 빠른 피드백 → A/B

---

## 8. Incrementality vs. A/B Testing

### 8.1 차이점

```
A/B Test:
  실험군 vs 대조군 비교 (상대값)
  예: 광고 A vs 광고 B (CTR 비교)

Incrementality Test:
  광고 노출군 vs 미노출군 (절대값)
  예: 광고 노출 1000명 vs 미노출 100명
  └─→ 순증가 측정 (인과)
```

### 8.2 Meta "Incremental Attribution Optimize" (2026)

- 순증가 전환에만 최적화
- 기존 A/B보다 5~10% 정확도 향상

---

## 9. 세그먼트 병합·분할 기준

### 9.1 병합 (Consolidation)

```
상황:
├─ Ad set 수 > 10개 (동일 오디언스)
├─ 각 ad set CPA 차이 < 10%
└─ 예산 분산으로 학습 방해

해법: CBO로 통합 → 알고리즘이 자동 최적화
```

### 9.2 분할 (Segmentation)

```
상황:
├─ Frequency 5회/주 (피로 신호)
├─ 특정 오디언스 성과 60% 우수 (Lookalike vs Custom)
└─ CPA 차이 > 30%

해법: 분리 ad set + 각각 크리에이티브 최적화
```

---

## 10. PMax·Advantage+ 가드레일

### 10.1 Brand Exclusion (필수)

```
PMax에 절대 포함 금지:
├─ 자사 브랜드 검색어
├─ 자사 제품 명칭
├─ 경쟁사 브랜드 명칭
└─ 일반명사 ("좋은 제품")

이유: CPC 10배 상승, ROI 악화
```

### 10.2 Audience Signal 공급

```
Google PMax:
├─ 최소 3개 Custom Audience 추가 (구매자·관심사·유사)
├─ Remarking List 정기 갱신
└─ Search Theme 추가 (선택, 안내용)

효과: 학습 가속 50% (7주 → 3.5주)
```

### 10.3 Search Themes (Google Search Ads)

```
추가 가능:
├─ "여름 휴가 패키지"
├─ "럭셔리 워치"
└─ 광고주가 제어하는 테마

효과: 관련성 높은 검색어만 타겟
```

---

## 11. 주간 운영 루틴 (월~금)

### Monday (성과 검토)

```
[ ] 지난주 KPI 정리 (ROAS, CPA, CVR)
[ ] 크리에이티브별 Hook rate 확인 (25% 목표)
[ ] Frequency 급증? (3.5회/주 이상?)
[ ] 예산 조정 필요? (20% rule 준수)
```

**의사결정**:
- Hook rate < 25% → 신규 크리에이티브 우선
- Frequency > 3.5 → 로테이션 즉시

### Wednesday (최적화 점검)

```
[ ] 러닝 페이즈 진행도 (50 conversions 추적)
[ ] 어트리뷰션 데이터 정합성 (Meta vs GA4)
[ ] Pixel/CAPI 신호 (37%+ ?)
[ ] 신규 리마케팅 오디언스 생성 (CRM 갱신)
```

**의사결정**:
- 신호 부족 → CAPI 매칭율 점검
- 오디언스 신규 → Audience segment 생성

### Friday (다음주 계획)

```
[ ] 크리에이티브 로테이션 일정 (Fatigue 신호 재확인)
[ ] 신규 크리에이티브 큐 (디자인 팀과 협의)
[ ] 예산 스텝업 스케줄 (월요일부터 시작?)
[ ] 경합사 모니터링 (CPM 변동)
```

**의사결정**:
- Frequency cap 조정 필요?
- 채널 분산 (Meta 편중 위험?)

---

## 12. CBO vs. ABO 선택 기준

| 상황 | 선택 | 이유 |
|------|------|------|
| 신규 캠페인 테스트 | ABO | 각 ad set 데이터 격리 |
| 승리 크리에이티브 스케일 | CBO | 자동 효율화 |
| 정확한 테스트 | ABO | 동등한 예산 배분 |
| 일일 모니터링 불가능 | CBO | 자동 최적화 |

**최고 Practice Flow**:
```
Week 1~2: ABO로 테스트 → 승리 식별
Week 3+: 승리 ad set 복제 → 새 CBO 캠페인
Week 4+: CBO가 자동 스케일링 (예산 20% rule 준수)
```

---

**참조**: 
- [측정·트래킹 일체](/sessions/exciting-happy-feynman/media-buying/references/measurement.md)
- [튜닝 플레이북](/sessions/exciting-happy-feynman/media-buying/references/tuning_playbook.md)
- [크리에이티브 설계](/sessions/exciting-happy-feynman/media-buying/references/creative.md)
- [안티패턴 20+](/sessions/exciting-happy-feynman/media-buying/references/antipatterns.md)
- [런칭 체크리스트](/sessions/exciting-happy-feynman/media-buying/references/launch_checklist.md)

