# recall-forge

<p align="center">
  <img src="https://img.shields.io/badge/RecallForge-Self%20Hosted%20Study%20Tool-00d8d6?style=flat-square" />
  <img src="https://img.shields.io/badge/Focus-Flashcards%20%26%20Wrong%20Notes-2f81f7?style=flat-square" />
  <img src="https://img.shields.io/badge/Direction-Personal%20Learning%20OS-8b5cf6?style=flat-square" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Backend-Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white" />
  <img src="https://img.shields.io/badge/Frontend-React%20%7C%20TypeScript-3178C6?style=flat-square&logo=react&logoColor=white" />
  <img src="https://img.shields.io/badge/Database-PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/OCR-Tesseract%20%7C%20Vision%20API-FFB000?style=flat-square" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Auth-Yule%20Auth-111827?style=flat-square" />
  <img src="https://img.shields.io/badge/Infra-Docker%20%7C%20Nginx-2496ED?style=flat-square&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/Storage-S3%20Compatible-569A31?style=flat-square" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" />
</p>

# RecallForge

RecallForge는 노트, 문서, 문제 이미지를 플래시카드와 오답노트, 반복 학습 세션으로 변환하는 셀프호스팅 학습 도구입니다.

단순히 카드를 만들고 외우는 앱이 아니라, 사용자가 틀린 문제를 다시 학습 가능한 형태로 정리하고, 약점 개념을 반복 복습할 수 있도록 돕는 개인 학습 시스템을 목표로 합니다.

소스 코드는 공개하지만, 실제 배포 환경은 `Yule Auth`를 통해 허용된 사용자만 접근할 수 있도록 설계합니다.

---

## Core Features

- 덱 기반 학습 주제 관리
- 낱말 카드 학습 모드
- 객관식 / 주관식 문제 풀이
- 오답노트 자동 저장
- 문제 이미지 업로드
- OCR 기반 문제 텍스트 추출
- OCR 결과 검수 후 문제 저장
- 약점 카드 분류
- 반복 학습 스케줄 관리
- 개인 인증 서비스 연동

---

## Learning Flow

```text
문제 이미지 / 노트 / 직접 입력
        ↓
카드 또는 문제로 변환
        ↓
낱말 카드 학습
        ↓
문제 풀이
        ↓
오답노트 저장
        ↓
약점 카드 복습
        ↓
반복 학습 일정 등록
````

---

## Architecture

```text
[Client]
   |
   v
[RecallForge Frontend]
   |
   v
[RecallForge API]
   |
   ├── Deck Module
   ├── Card Module
   ├── Question Module
   ├── Wrong Answer Module
   ├── Review Schedule Module
   └── OCR Module
          |
          ├── Tesseract OCR
          ├── Google Vision API
          └── OpenAI Vision

[RecallForge API]
   |
   ├── PostgreSQL
   ├── Redis
   ├── S3 Compatible Storage
   └── Yule Auth
```

---

## Tech Stack

| Area     | Stack                                                    |
| -------- | -------------------------------------------------------- |
| Backend  | Java 17, Spring Boot 3, Spring Security, Spring Data JPA |
| Frontend | React, TypeScript, Vite, Tailwind CSS                    |
| Database | PostgreSQL                                               |
| Cache    | Redis                                                    |
| OCR      | Tesseract OCR, Vision API Provider                       |
| Storage  | Local Storage, S3 Compatible Storage                     |
| Auth     | Yule Auth, JWT                                           |
| Infra    | Docker, Nginx, GitHub Actions                            |

---

## Domain Overview

```text
Deck
 └── Card
 └── Question
       └── QuestionChoice
       └── WrongAnswerNote

QuestionImage
 └── OcrResult

ReviewSchedule
 └── Card or Question
```

---

## MVP Scope

### v0.1

* 덱 생성
* 카드 생성
* 낱말 카드 학습
* 객관식 문제 풀이
* 주관식 문제 풀이
* 기본 오답노트

### v0.2

* 문제 이미지 업로드
* OCR 텍스트 추출
* OCR 결과 수정
* 문제로 저장
* 오답노트와 원본 이미지 연결

### v0.3

* 반복 학습 스케줄
* 약점 카드 자동 분류
* 오늘의 학습 세션
* 학습 통계

### v0.4

* AI 문제 생성
* AI 해설 생성
* 유사 문제 생성
* Markdown / PDF Import

---

## Authentication Strategy

RecallForge는 자체적으로 복잡한 로그인 시스템을 가지지 않고, 공통 인증 서비스인 `Yule Auth`와 연동합니다.

```text
User
 ↓
Yule Auth
 ↓
JWT
 ↓
RecallForge
```

배포된 서비스는 허용된 사용자만 접근할 수 있습니다.

```text
Public Source Code
Private Deployed Service
Self-hosted Access Control
```

---

## Related Repositories

| Repository     | Description                                       |
| -------------- | ------------------------------------------------- |
| `yule-auth`    | 개인 프로젝트 전반에서 공통으로 사용하는 셀프호스팅 인증 및 접근 제어 서비스       |
| `recall-forge` | 플래시카드, 오답노트, OCR 기반 문제 수집을 지원하는 개인 학습 서비스         |
| `yule-infra`   | Docker, Nginx, GitHub Actions 기반 개인 서비스 배포 설정 저장소 |

---

## Project Direction

RecallForge는 Quizlet 스타일의 플래시카드 학습 경험을 참고하되, 개인 오답노트와 셀프호스팅 학습 환경에 초점을 둡니다.

특히 자격증 공부, 개발 이론 정리, 언어 학습, 기술 면접 준비처럼 반복 암기가 필요한 학습 흐름을 개인이 직접 관리할 수 있도록 설계합니다.

````

공통 로그인 레포는 README에 이렇게 두면 깔끔합니다.

```md
# Yule Auth

Yule Auth는 개인 프로젝트 전반에서 공통으로 사용하는 셀프호스팅 인증 및 접근 제어 서비스입니다.

소스 코드는 공개하되, 실제 배포된 개인 서비스는 허용된 사용자만 접근할 수 있도록 JWT 기반 인증과 서비스별 접근 권한을 제공합니다.
````

레포 설명 한 줄은 이걸 추천합니다.

```text
Self-hosted authentication and access control service for personal Yule projects.
```

