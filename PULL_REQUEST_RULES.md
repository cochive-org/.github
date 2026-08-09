# Pull Request Rules

이 문서는 `subup-org` 저장소에서 PR 자동화 요청과 Prow 명령을 해석하는 공통
기준을 정의한다. 개별 저장소에 더 구체적인 규칙이 있으면 그 문서를 우선한다.

## Kind와 self-approve

PR을 만든 직후 주된 변경 목적에 맞는 `/kind ...`를 댓글로 작성한다.

| 변경 유형 | Prow 명령 |
| --- | --- |
| 버그 수정 | `/kind bug` |
| 신규 기능 | `/kind feature` |
| 기존 기능 개선 | `/kind enhancement` |
| 리팩터링 | `/kind refactor` |
| 문서 | `/kind documentation` |
| 테스트 | `/kind test` |
| 설정·의존성·유지보수 | `/kind chore` |

사용자가 "적절한 PR을 작성하고 Prow 규칙에 맞게 self-approve"를 요청하면 PR
작성자는 다음 두 Prow 명령만 댓글로 작성한다.

1. PR 주제에 맞는 `/kind ...`
2. `/approve`

- 작성자는 자신의 PR에 `/lgtm`을 작성하지 않는다. Prow는 self `/lgtm`을
  인정하지 않는다.
- `/cc`와 `/auto-cc`는 사용자가 reviewer 지정이나 재선정을 명시적으로 요청한
  경우에만 사용한다. self-approve 요청만으로 reviewer 요청을 추론하지 않는다.
- GitHub Review의 Approve는 Prow `/approve`를 대신하지 않는다.

## 병합 확인

- 저장소가 요구하는 기본 브랜치, 검증과 필수 상태를 확인한다.
- `do-not-merge/*`, `needs-kind`, `status/blocked` 라벨이 있으면 병합하지 않는다.
- 새 커밋을 추가했다면 Prow 라벨과 상태를 다시 확인한다.
