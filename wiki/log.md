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
