---
name: media-buying
description: |
  광고 매체 집행·예산 배분·입찰·소재 테스트 운영 스킬. 한국 디폴트로 네이버·카카오·메타·구글 집행안을 만든다. 트리거: 미디어바잉, media buying, 매체집행, 예산배분, 입찰전략, 집행해줘, 예산 나눠줘, 튜닝해줘, optimize spend. NOT: 상위 광고전략(→ads-playbook), 카피(→copywriting-skill), 브랜드기획(→brand-campaign).
---

# Media Buying

## §0 원칙


## Skill Boundaries

- **하는 것** — "광고 매체 집행·예산 배분·입찰·소재 테스트 운영 스킬.
- **안 하는 것** — 상위 광고전략(→ads-playbook), 카피(→copywriting-skill), 브랜드기획(→brand-campaign)."

한국 디폴트: 별도 지정이 없으면 한국 시장, 원화, 네이버·카카오·메타·구글을 기본 후보로 둔다.

1. 예산은 테스트, 학습, 확장, 리타겟팅으로 나눈다.
2. 입찰은 전환 이벤트 품질과 학습량을 기준으로 조정한다.
3. 채널별 성과 비교는 같은 전환 정의로만 한다.
4. 상위 전략은 ads-playbook으로 넘기고, 본 스킬은 집행 운영에 집중한다.

## When to Use

- 사용자가 "집행해줘", "예산 나눠줘", "튜닝해줘", "optimize spend." 같은 표현으로 발동
- 도메인 작업이 필요한 시점
- **안 쓸 때** — 상위 광고전략(→ads-playbook), 카피(→copywriting-skill), 브랜드기획(→brand-campaign)."


## Prerequisites

| # | 체크 | 미충족 시 |
|---|------|-----------|
| 1 | 대상·입력 명확 (스킬 발동 의도 확인) | 1줄 확인 후 진입 |
| 2 | references/ 폴더 접근 가능 | inline fallback |
| 3 | scripts/ 실행 권한 | 권한 보정 후 재시도 |


## §1 입력

| 항목 | 필요 내용 |
|---|---|
| Budget | 총액·기간·일예산 |
| Channel | 후보 매체와 우선순위 |
| Funnel | 신규·전환·재구매·리타겟팅 |
| Signal | 픽셀, SDK, CRM, 오프라인 전환 |
| Constraint | 소재 수, 승인 리드타임, 법무 제한 |

## §2 예산 배분

- 테스트: 신규 채널·소재 검증
- 학습: 전환 이벤트 안정화
- 확장: 검증된 세트 증액
- 방어: 리타겟팅·브랜드 검색

## §3 입찰

| 상황 | 처방 |
|---|---|
| 전환 적음 | 더 얕은 이벤트로 학습 시작 |
| CPA 불안정 | 예산 변동폭 축소 |
| 소재 피로 | 신규 소재 투입 후 비교 |
| 특정 채널 과집중 | 증분성과 기준으로 재배분 |

## §4 운영 리듬

1. D0: 세팅, 태그, 이벤트 검증.
2. D1-D3: 학습량과 승인 이슈 확인.
3. D4-D7: 소재·타깃·입찰 1차 조정.
4. Week 2: 증액 또는 중단 판단.

## §5 출력

| 구분 | 내용 |
|---|---|
| 배분안 | 채널·퍼널별 예산 |
| 입찰안 | 이벤트·전략·조정폭 |
| 테스트안 | 소재·타깃·기간 |
| 리스크 | 학습량, 추적, 승인 문제 |

## Output Path

| 산출물 | 경로 |
|---|---|
| 주 산출물 | `mnt/outputs/media-buying_{topic}_{YYYY-MM-DD}.md` |
| 형식 | 집행안으로, .md로. |
| 리서치 결과 (해당 시) | `{VAULT}/_skills research/media-buying/{YYYY-MM-DD}_{topic}.md` |

## Reference Index

| 파일 | 내용 | 언제 |
|---|---|---|
| `references/antipatterns.md` | antipatterns | 해당 단계 진입 시 |
| `references/creative.md` | creative | 해당 단계 진입 시 |
| `references/glossary.md` | glossary | 해당 단계 진입 시 |
| `references/latest_2026q2.md` | latest 2026q2 | 해당 단계 진입 시 |
| `references/launch_checklist.md` | launch checklist | 해당 단계 진입 시 |
| `references/measurement.md` | measurement | 해당 단계 진입 시 |
| `references/objective_app.md` | objective app | 해당 단계 진입 시 |
| `references/objective_brand.md` | objective brand | 해당 단계 진입 시 |
| `references/objective_commerce.md` | objective commerce | 해당 단계 진입 시 |
| `references/objective_lead.md` | objective lead | 해당 단계 진입 시 |
| `references/objective_matrix.md` | objective matrix | 해당 단계 진입 시 |
| `references/platform_google.md` | platform google | 해당 단계 진입 시 |
| `references/platform_meta.md` | platform meta | 해당 단계 진입 시 |
| `references/platform_naver_kakao.md` | platform naver kakao | 해당 단계 진입 시 |
| `references/platform_tiktok_asa.md` | platform tiktok asa | 해당 단계 진입 시 |


## Next Phase

본 스킬 작업 후 자연스럽게 이어지는 흐름:

- 후속 작업 → `ads-playbook`
- 후속 작업 → `copywriting-skill`
- 후속 작업 → `brand-campaign`

## Failure Modes (Gotchas)

| 함정 | 대응 |
|---|---|
| 하루 성과로 중단 | 최소 학습량과 기간 확보 |
| 채널별 다른 전환 기준 | 이벤트 정의 통일 |
| 증액 폭 과다 | 20~30% 단위로 단계 조정 |
| ❌ 저렴한 CPA만 보고 예산 집중 | ✅ 증분성과와 전환 품질을 함께 본다 |
