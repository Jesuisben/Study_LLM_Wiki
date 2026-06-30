# Wiki Log

> 이 파일은 위키 작업의 시간순 기록이다.  
> append-only로 운영한다. 과거 기록을 임의로 삭제하지 않는다.  
> 형식: `## [YYYY-MM-DD] action | subject`  
> action 예시: `create`, `ingest`, `update`, `query`, `lint`, `archive`, `delete`

## [2026-06-29] create | LLM 위키 기본 골격 생성

- 목적: 국비지원 웹서비스 풀스택 개발자 과정 학습 내용을 장기적으로 추적하고, 새 세션에서도 위키를 통해 맥락을 복원할 수 있게 하기 위함.
- 생성한 구조:
  - `raw/` — 사용자가 넣는 원본 자료 폴더. LLM은 읽기만 하고 수정하지 않음.
  - `raw/assets/` — 원본 자료에 딸린 이미지/첨부파일.
  - `wiki/` — LLM이 정리한 지식 베이스.
  - `wiki/summaries/` — 수업/자료 요약.
  - `wiki/concepts/` — 개념 정리.
  - `wiki/entities/` — 기술/도구/프레임워크 정리.
  - `wiki/comparisons/` — 비교 분석.
  - `wiki/queries/` — 보존 가치 있는 질문 답변.
  - `wiki/_meta/` — 운영 보조 문서와 점검 리포트.
- 생성한 파일:
  - `AGENTS.md` — 위키 운영 규칙과 사용자/목적/커리큘럼 맥락.
  - `wiki/index.md` — 전체 위키 목차 골격.
  - `wiki/log.md` — 작업 일지 골격.

## [2026-06-30] create | 집 노트북 Hermes/LLM Wiki 환경 복제 가이드

- 목적: 현재 컴퓨터의 Obsidian LLM Wiki와 Hermes Agent 설정, memory, skills, Desktop UI 설정을 집 노트북에서도 최대한 동일하게 복제할 수 있도록 절차를 문서화함.
- 생성한 파일:
  - `wiki/_meta/hermes-home-laptop-setup.md` — GitHub clone, AppData Hermes 설정 복사, `config.yaml`의 `cwd` 경로 수정, GitHub 인증, 확인 체크리스트를 정리한 가이드.
- 수정한 파일:
  - `wiki/index.md` — Meta 섹션에 새 가이드 문서를 등록하고 페이지 수/업데이트 날짜를 갱신함.

## [2026-06-30] update | 집 노트북 Hermes 인증 파일 제외 방식 반영

- 목적: 집 노트북에서 OpenAI OAuth를 새로 연결할 예정이므로, API 키/OAuth 토큰 파일을 복사하지 않는 더 안전한 이전 방식을 문서에 반영함.
- 수정한 파일:
  - `wiki/_meta/hermes-home-laptop-setup.md` — `.env`, `auth.json`은 복사하지 않고, `config.yaml`, `state.db`, `skills/`, `projects.db` 중심으로 옮기는 권장 절차와 체크리스트를 추가/수정함.
