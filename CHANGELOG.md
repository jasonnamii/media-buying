# Changelog — media-buying

이 파일은 ads-playbook의 변경 이력을 기록합니다.
[Keep a Changelog](https://keepachangelog.com/) 형식 준수.

## [1.1.0] - 2026-04-21

### Added
- `evals/cases.json` — 5개 회귀 테스트 케이스 (진단·설계·운영·용어·B2B 리드)
- `scripts/validate.py` — self-check 자동 검증 스크립트
- 허브 §4.5 "조건부 로딩 매트릭스" — references 18개 과부하 방지 (1차/2차/금지 스포크 가이드)
- 허브 Self-Check 섹션
- frontmatter `version` 필드
- `CHANGELOG.md`

### Changed
- §3-② 플랫폼 조합 룰 표를 `objective_matrix.md`로 완전 위임 (허브 크기 축소 9.3KB → 9.9KB, 중복 제거)

### Rationale
- skill-doctor 진단 결과 🟠 70/100 → 🔴 3건(evals·self-check·references 과부하) + 🟠 다수 해결 목표
- 본질 보존: §0 7대 원칙·4모드 라우터·한국 디폴트·용어 주석 규칙 불변

## [1.0.0] - 2026-04-17 (initial)

- 8플랫폼 × 10광고목적 × 4모드(진단·설계·운영·용어) 초안
- 17개 references 스포크 + Gotchas
