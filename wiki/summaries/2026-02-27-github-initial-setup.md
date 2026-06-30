---
title: 2026-02-27 GitHub 초기 설정
created: 2026-06-30
updated: 2026-06-30
type: summary
tags: [java, curriculum, study-log]
sources:
  - raw/Study/1. Java/2026.02.27(금)/깃허브 초기 설정.md
status: seed
confidence: medium
---

# 2026-02-27 GitHub 초기 설정

## 한 줄 요약

Java 프로젝트를 Git으로 관리하고 GitHub 원격 저장소와 IntelliJ IDEA를 연결하기 위한 초기 설정 흐름을 정리했다.

## 배운 내용

### Git 설치 경로 확인

수업에서는 Windows 환경에서 [[entities/git|Git]]이 설치된 경로를 확인했다.

- 설치 경로 예시: `C:\Program Files\Git\bin`
- Git 명령을 쓰려면 터미널 또는 IDE가 이 Git 실행 파일을 찾을 수 있어야 한다.

### 프로젝트 폴더로 이동

명령 프롬프트에서 Java 프로젝트 폴더로 이동한 뒤 Git 설정을 진행하는 흐름이 소개되었다.

1. D 드라이브로 이동
2. `D:/java_project/MyJava` 프로젝트 폴더로 이동
3. 해당 폴더를 Git이 신뢰할 수 있는 작업 디렉터리로 등록

`safe.directory` 설정은 Git이 특정 폴더를 안전한 저장소로 취급하도록 등록하는 설정이다. 다른 사용자 권한이나 소유권 문제로 Git이 저장소 사용을 막을 때 필요할 수 있다.

### Git 사용자 정보 설정

GitHub에 자료를 올릴 때 커밋 작성자를 식별하기 위해 전역 사용자 이름과 이메일을 설정한다.

- `user.name`: 커밋 작성자 이름
- `user.email`: 커밋 작성자 이메일

이 설정은 GitHub 계정과 연동될 때 커밋 기록의 작성자 표시와 관련된다.

### GitHub 원격 저장소 연결

[[entities/github|GitHub]]에서 `MyJava` 저장소를 만들고, 원격 저장소 URL을 프로젝트에 연결하는 흐름이 언급되었다.

- GitHub 웹사이트: `https://github.com`
- 저장소 이름: `MyJava`
- 원격 저장소 URL 형식: `https://github.com/<사용자명>/<저장소명>.git`

### IntelliJ IDEA와 Git 연동

IntelliJ IDEA에서 Git 및 원격 저장소를 연결해 프로젝트 변경사항을 IDE 안에서 관리할 수 있게 하는 과정이 포함되어 있다.

원본에는 IntelliJ에서 `Manage Remotes`가 보이지 않을 때 명령 프롬프트에서 프로젝트 폴더로 이동해 `git init`을 실행하는 해결 흐름도 적혀 있다.

## 실습 / 예제

원본에 나온 작업 흐름은 다음처럼 요약할 수 있다.

1. Git 설치 경로 확인
2. 명령 프롬프트에서 Java 프로젝트 폴더로 이동
3. `git config --global --add safe.directory ...`로 안전한 디렉터리 등록
4. `git config --global user.name ...` 설정
5. `git config --global user.email ...` 설정
6. GitHub에서 `MyJava` 원격 저장소 준비
7. IntelliJ IDEA에서 Git과 원격 저장소 연동
8. 필요하면 `git init`으로 프로젝트 폴더를 Git 저장소로 초기화

## 핵심 개념

- [[entities/git|Git]] — 프로젝트 변경 이력을 저장하고 되돌릴 수 있게 해 주는 버전 관리 도구
- [[entities/github|GitHub]] — Git 저장소를 원격으로 보관하고 공유하는 웹 서비스
- 원격 저장소(remote repository) — 내 컴퓨터가 아닌 GitHub 같은 외부 위치에 있는 Git 저장소
- `git init` — 현재 폴더를 Git 저장소로 초기화하는 명령
- `git config` — Git의 사용자 정보, 저장소 신뢰 설정 등을 등록하는 명령

## 헷갈린 점 / 질문

- `git init`은 이미 Git 저장소인 폴더에서 반복적으로 실행할 필요가 없다. 프로젝트가 아직 Git 저장소가 아닐 때 처음 한 번 실행하는 명령으로 이해하면 된다.
- `user.name`과 `user.email`은 GitHub 로그인 자체가 아니라 커밋 작성자 정보다.
- `safe.directory`는 모든 프로젝트마다 항상 필요한 설정은 아니며, Git이 안전하지 않은 저장소라고 경고할 때 주로 사용한다.

## 관련 페이지

- [[summaries/2026-02-26-orientation|2026-02-26 오리엔테이션과 개발 환경 준비]]
- [[summaries/2026-02-27-java-basic-types-operators|2026-02-27 Java 기본 자료형과 연산자]]
- [[entities/git|Git]]
- [[entities/github|GitHub]]

## 출처

- `raw/Study/1. Java/2026.02.27(금)/깃허브 초기 설정.md`
