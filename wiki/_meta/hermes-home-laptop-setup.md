---
title: 집 노트북에 LLM Wiki와 Hermes Agent 환경 복제하기
created: 2026-06-30
updated: 2026-06-30
type: meta
tags: [study-log]
sources: []
status: stable
confidence: high
---

# 집 노트북에 LLM Wiki와 Hermes Agent 환경 복제하기

## 목적

현재 학원/작업 컴퓨터에서 쓰는 다음 환경을 집 노트북에서도 최대한 똑같이 쓰기 위한 절차다.

- Obsidian LLM Wiki Vault
- GitHub 연동
- Hermes Agent 설정
- Hermes memory / user profile / skills / session 기록
- Hermes Desktop 테마와 UI 설정

핵심은 다음과 같다.

```text
LLM Wiki = GitHub로 복제
Hermes Agent 환경 = AppData의 Hermes 설정/기억/스킬 파일 복사
API 키/OAuth 토큰 = 복사하지 않고 집 노트북에서 새로 로그인
집 노트북에 D드라이브가 없으면 config.yaml의 cwd만 C드라이브 경로로 수정
```

## 전체 구조 이해

| 대상 | 현재 컴퓨터의 위치 | 집 노트북에서 처리 |
|---|---|---|
| LLM Wiki Vault | `D:\Study_LLM_Wiki` | GitHub에서 clone |
| Hermes 설정/기억/스킬 | `C:\Users\ICT02-006\AppData\Local\hermes` | 같은 위치 역할의 폴더로 복사 |
| Hermes Desktop UI 설정 | `C:\Users\ICT02-006\AppData\Roaming\Hermes` | 같은 위치 역할의 폴더로 복사 |
| GitHub 인증 | Git Credential Manager / Obsidian Git | 집 노트북에서 다시 로그인 가능 |
| API 키 / OAuth | `.env`, `auth.json` | 복사하지 않고 집 노트북에서 새로 연결 권장 |

## 1. 현재 컴퓨터에서 먼저 할 일

### 1.1 Obsidian Git으로 최신 상태 push

Obsidian Git 플러그인에서 다음 순서로 처리한다.

```text
stage all → commit → push
```

또는 Git Bash에서 Vault 폴더로 이동한 뒤 확인할 수 있다.

```bash
cd /d/Study_LLM_Wiki
git status
git push
```

GitHub 저장소에 최신 파일이 올라갔는지 확인한다.

```text
https://github.com/Jesuisben/Study_LLM_Wiki.git
```

### 1.2 Hermes Desktop 완전히 종료

설정 파일과 DB를 복사하기 전에 Hermes Desktop을 완전히 종료한다.

이유:

- `state.db` 같은 SQLite DB가 사용 중일 수 있음
- `Local Storage`, `Preferences` 같은 Desktop 설정이 쓰기 중일 수 있음
- 실행 중 복사하면 일부 파일이 빠지거나 손상될 수 있음

가능하면 시스템 트레이에 남아 있는 Hermes도 종료한다.

## 2. 현재 컴퓨터에서 백업할 폴더

### 2.1 필수 백업: Hermes 로컬 홈 중 인증 파일을 제외한 핵심 파일

OpenAI OAuth는 집 노트북에서 새로 연결할 예정이므로, Hermes 로컬 홈 전체를 무조건 통째로 복사하기보다 **인증 파일을 제외하고** 필요한 파일/폴더를 복사하는 방식을 권장한다.

원본 폴더 위치:

```text
C:\Users\ICT02-006\AppData\Local\hermes
```

이 안에서 우선 복사할 항목은 다음이다.

| 파일/폴더 | 복사 여부 | 의미 |
|---|---:|---|
| `config.yaml` | 권장 | 모델, provider, 작업 폴더, 표시 설정 |
| `state.db` | 권장 | memory, user profile, session_search용 대화 DB |
| `skills/` | 권장 | Hermes가 쓰는 스킬들 |
| `projects.db` | 권장 | Desktop Project 정보 |
| `sessions/` | 선택 | 세션 관련 파일. 있으면 과거 세션 보존에 도움 |
| `profiles/` | 선택 | 별도 프로필을 만들었다면 해당 프로필 정보 |
| `hermes-agent/` | 보통 불필요 | Hermes Agent 설치본 / 소스 / venv. 집 노트북에 새로 설치하면 굳이 옮기지 않아도 됨 |
| `.env` | 제외 권장 | API 키와 환경변수. 집 노트북에서 새로 설정 |
| `auth.json` | 제외 권장 | OAuth 로그인 정보. 집 노트북에서 새로 로그인 |

따라서 권장 복사 목록은 다음이다.

```text
C:\Users\ICT02-006\AppData\Local\hermes\config.yaml
C:\Users\ICT02-006\AppData\Local\hermes\state.db
C:\Users\ICT02-006\AppData\Local\hermes\skills\
C:\Users\ICT02-006\AppData\Local\hermes\projects.db
```

선택 복사 목록:

```text
C:\Users\ICT02-006\AppData\Local\hermes\sessions\
C:\Users\ICT02-006\AppData\Local\hermes\profiles\
```

복사하지 않을 항목:

```text
C:\Users\ICT02-006\AppData\Local\hermes\.env
C:\Users\ICT02-006\AppData\Local\hermes\auth.json
```

### 2.2 선택 백업: Hermes Desktop UI 설정

Desktop 앱의 화면, 테마, localStorage까지 최대한 맞추고 싶으면 다음 폴더도 복사한다.

```text
C:\Users\ICT02-006\AppData\Roaming\Hermes
```

이 폴더에는 대략 다음이 들어 있다.

| 파일/폴더 | 의미 |
|---|---|
| `Preferences` | Electron 앱 설정 |
| `Local Storage/` | Desktop 테마, UI localStorage 설정 가능성 |
| `window-state.json` | 창 위치/크기 |
| `native-theme.json` | 네이티브 테마 설정 |
| `composer-images/` | 채팅에 붙였던 이미지 캐시 |

## 3. 보안 주의사항

OpenAI OAuth와 API 인증은 집 노트북에서 새로 연결할 예정이라면 다음 파일은 **옮기지 않는다.**

```text
C:\Users\ICT02-006\AppData\Local\hermes\.env
C:\Users\ICT02-006\AppData\Local\hermes\auth.json
```

이 두 파일은 비밀번호처럼 취급한다.

주의:

- 절대 GitHub에 올리지 않는다.
- 공개 클라우드 폴더에 올리지 않는다.
- 집 노트북에서 OpenAI OAuth를 새로 연결할 거라면 복사하지 않는다.

다음 파일도 대화 기록과 memory가 들어 있을 수 있으므로 민감한 파일로 취급한다. 다만 현재 환경의 기억을 이어가려면 복사 대상이다.

```text
C:\Users\ICT02-006\AppData\Local\hermes\state.db
```

특히 `.env`, `auth.json`에는 API 키나 OAuth 토큰이 들어 있을 수 있다.

## 4. 집 노트북에서 설치할 것

집 노트북에 먼저 설치한다.

1. Git for Windows
2. Obsidian
3. Hermes Agent / Hermes Desktop

GitHub push/pull을 편하게 하려면 Git Credential Manager가 포함된 Git for Windows 설치를 권장한다.

## 5. 집 노트북에서 LLM Wiki clone

집 노트북에는 D드라이브가 없으므로 C드라이브 아래 원하는 위치에 둔다.

추천 위치:

```text
C:\Users\집노트북사용자명\Documents\Study_LLM_Wiki
```

Git Bash에서 예시는 다음과 같다.

```bash
cd ~/Documents
git clone https://github.com/Jesuisben/Study_LLM_Wiki.git
```

clone 후 폴더 구조는 다음처럼 되어야 한다.

```text
Study_LLM_Wiki/
├── AGENTS.md
├── raw/
├── wiki/
└── .git/
```

## 6. 집 노트북에서 Obsidian Vault 열기

Obsidian에서 다음 순서로 연다.

```text
Open folder as vault → C:\Users\집노트북사용자명\Documents\Study_LLM_Wiki 선택
```

Community Plugins가 꺼져 있으면 다음을 확인한다.

1. Settings
2. Community plugins
3. Restricted mode 끄기
4. Obsidian Git 플러그인 enable

GitHub 로그인이 필요하면 Obsidian Git이 push/pull할 때 로그인 창을 띄울 수 있다.

## 7. 집 노트북에 Hermes 설정 복사

### 7.1 Hermes 종료

집 노트북에서도 Hermes Desktop을 완전히 종료한다.

### 7.2 AppData 폴더에 복사

현재 컴퓨터에서 백업한 핵심 파일/폴더를 집 노트북의 사용자 폴더 아래로 복사한다.

현재 컴퓨터:

```text
C:\Users\ICT02-006\AppData\Local\hermes\config.yaml
C:\Users\ICT02-006\AppData\Local\hermes\state.db
C:\Users\ICT02-006\AppData\Local\hermes\skills\
C:\Users\ICT02-006\AppData\Local\hermes\projects.db
C:\Users\ICT02-006\AppData\Roaming\Hermes
```

집 노트북:

```text
C:\Users\집노트북사용자명\AppData\Local\hermes\config.yaml
C:\Users\집노트북사용자명\AppData\Local\hermes\state.db
C:\Users\집노트북사용자명\AppData\Local\hermes\skills\
C:\Users\집노트북사용자명\AppData\Local\hermes\projects.db
C:\Users\집노트북사용자명\AppData\Roaming\Hermes
```

이때 다음 파일은 복사하지 않는다.

```text
.env
auth.json
```

집 노트북에서는 Hermes 설치 후 OpenAI OAuth를 새로 연결한다.

이미 집 노트북에 같은 폴더가 있다면, 먼저 백업해두는 것이 안전하다.

예:

```text
hermes_backup_before_copy
Hermes_backup_before_copy
```

## 8. config.yaml에서 작업 폴더 경로 수정

가장 중요한 단계다.

현재 컴퓨터의 설정은 다음처럼 되어 있다.

```yaml
terminal:
  backend: local
  cwd: D:\Study_LLM_Wiki
```

집 노트북에는 D드라이브가 없으므로, 집 노트북의 실제 Vault 경로로 바꾼다.

예:

```yaml
terminal:
  backend: local
  cwd: C:\Users\집노트북사용자명\Documents\Study_LLM_Wiki
```

수정할 파일:

```text
C:\Users\집노트북사용자명\AppData\Local\hermes\config.yaml
```

`D:\Study_LLM_Wiki`가 다른 곳에도 들어 있을 수 있으므로, 설정 파일에서 `D:\Study_LLM_Wiki`를 검색해서 모두 집 노트북 경로로 바꾼다.

## 9. Git 사용자 정보 확인

집 노트북 Git Bash에서 확인한다.

```bash
git config --global user.name
git config --global user.email
```

비어 있으면 설정한다.

```bash
git config --global user.name "Jesuisben"
git config --global user.email "rktngusals@gmail.com"
```

Vault 폴더에서 Git 상태를 확인한다.

```bash
cd ~/Documents/Study_LLM_Wiki
git status
git pull
```

`git pull` 또는 `git push` 중 GitHub 로그인이 뜨면 브라우저에서 로그인한다.

## 10. Hermes 실행 후 확인

Hermes Desktop을 실행한 뒤 새 채팅에서 이렇게 말한다.

```text
이 컴퓨터에서는 LLM Wiki 경로가 C:\Users\집노트북사용자명\Documents\Study_LLM_Wiki야.
AGENTS.md, wiki/index.md, wiki/log.md 읽고 현재 상태 확인해줘.
```

정상이라면 Hermes는 다음 규칙을 다시 따를 수 있다.

- `raw/`는 원본 자료라 수정하지 않음
- `wiki/`는 LLM이 생성/수정하는 지식 베이스
- 작업 시작 시 `AGENTS.md`, `wiki/index.md`, `wiki/log.md` 확인
- 새 페이지 생성 시 `wiki/index.md` 업데이트
- 의미 있는 작업 후 `wiki/log.md` 기록

## 11. 옮겨진 기억과 스킬 확인

Hermes 설정 폴더를 제대로 복사했다면 다음이 따라올 수 있다.

| 항목 | 따라오는 조건 |
|---|---|
| memory / user profile | `state.db` 또는 관련 memory 저장소 복사 |
| 과거 session 검색 | `state.db`, `sessions/` 복사 |
| skills | `skills/` 복사 |
| 모델/provider 설정 | `config.yaml` 복사 |
| OAuth/API 인증 | 복사하지 않고 집 노트북에서 새로 로그인 권장 |
| Desktop 테마/UI | `AppData\Roaming\Hermes` 복사 |

집 노트북에서는 OAuth/API 인증을 새로 설정한다.

```bash
hermes auth
```

또는 모델/provider 설정을 다시 연다.

```bash
hermes setup
hermes model
```

## 12. 문제 상황별 해결

### Hermes가 여전히 D드라이브를 찾는 경우

`config.yaml`에서 `D:\Study_LLM_Wiki`가 남아 있는지 다시 검색한다.

바꿀 값:

```text
D:\Study_LLM_Wiki
```

새 값 예시:

```text
C:\Users\집노트북사용자명\Documents\Study_LLM_Wiki
```

### Git push가 안 되는 경우

1. GitHub 로그인 창이 뜨는지 확인
2. Obsidian Git 플러그인 enable 확인
3. Git Bash에서 직접 확인

```bash
git status
git pull
git push
```

### Hermes memory가 안 따라온 것 같은 경우

다음 파일/폴더가 복사되었는지 확인한다.

```text
AppData\Local\hermes\state.db
AppData\Local\hermes\skills\
AppData\Local\hermes\sessions\
```

그래도 안 되면 집 노트북에서 새로 작업하면서 `AGENTS.md`와 `wiki/`를 기준으로 이어가면 된다. LLM Wiki 운영 규칙 자체는 Vault 안에 보존되어 있다.

### 테마가 다르게 보이는 경우

Desktop UI 설정까지 맞추려면 다음 폴더도 복사되어야 한다.

```text
AppData\Roaming\Hermes
```

또는 Hermes 채팅창에서 다음을 사용한다.

```text
/skin list
/skin 테마이름
```

## 13. 최종 체크리스트

집 노트북에서 아래 항목을 확인한다.

- [ ] Git 설치 완료
- [ ] Obsidian 설치 완료
- [ ] Hermes 설치 완료
- [ ] GitHub에서 `Study_LLM_Wiki` clone 완료
- [ ] Obsidian에서 clone한 폴더를 Vault로 열었음
- [ ] `config.yaml`, `state.db`, `skills/`, `projects.db` 복사 완료
- [ ] `.env`, `auth.json`은 복사하지 않았음
- [ ] 집 노트북에서 OpenAI OAuth 새로 연결 완료
- [ ] 필요하면 `AppData\Roaming\Hermes` 복사 완료
- [ ] `config.yaml`의 `cwd`를 C드라이브 Vault 경로로 수정 완료
- [ ] GitHub pull/push 테스트 완료
- [ ] Hermes에서 새 채팅 열고 `AGENTS.md`, `wiki/index.md`, `wiki/log.md` 확인 요청 완료

## 한 줄 요약

```text
집 노트북에서는 Wiki는 GitHub에서 clone하고, Hermes는 인증 파일을 제외한 설정/기억/스킬 파일을 복사한 뒤, OpenAI OAuth는 새로 연결하고, config.yaml의 D:\Study_LLM_Wiki만 C드라이브의 실제 Vault 경로로 바꾸면 된다.
```

## 관련 페이지

- [[../index|Wiki Index]]
- [[../log|Wiki Log]]

## 출처

- 현재 컴퓨터의 Hermes 설정 확인 결과
- 현재 Vault 구조와 GitHub remote 확인 결과
- Hermes Agent 설정/스킬/세션 저장 구조 설명
