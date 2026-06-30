---
title: Git
created: 2026-06-30
updated: 2026-06-30
type: entity
tags: [curriculum, project]
sources:
  - raw/Study/1. Java/2026.02.27(금)/깃허브 초기 설정.md
status: seed
confidence: medium
---

# Git

## 무엇인가

Git은 소스 코드와 프로젝트 파일의 변경 이력을 기록하는 분산 버전 관리 시스템이다. 언제 어떤 파일이 어떻게 바뀌었는지 남기고, 필요하면 이전 상태로 돌아가거나 여러 작업 흐름을 나눠 관리할 수 있다.

## 이 위키에서의 맥락

국비지원 과정 초반 Java 프로젝트를 만들면서 `D:/java_project/MyJava` 폴더를 Git으로 관리하고, GitHub 원격 저장소와 연결하기 위해 처음 등장했다.

## 핵심 기능 / 특징

- 변경 이력 관리: 파일 변경사항을 커밋 단위로 기록한다.
- 로컬 저장소: 내 컴퓨터의 프로젝트 폴더 안에서 버전 관리를 수행한다.
- 원격 저장소 연결: [[entities/github|GitHub]] 같은 서비스에 저장소를 올려 백업/공유할 수 있다.
- 설정 관리: `git config`로 사용자 이름, 이메일, 안전한 디렉터리 등을 설정한다.

## 관련 개념

- [[entities/github|GitHub]]
- [[summaries/2026-02-27-github-initial-setup|2026-02-27 GitHub 초기 설정]]
- 원격 저장소(remote repository)
- 커밋(commit)
- `git init`
- `git config`

## 학습 이력

- [[summaries/2026-02-27-github-initial-setup|2026-02-27]]: Git 설치 경로 확인, Java 프로젝트 폴더 이동, `safe.directory`, `user.name`, `user.email`, `git init` 흐름을 학습했다.

## 출처

- `raw/Study/1. Java/2026.02.27(금)/깃허브 초기 설정.md`
