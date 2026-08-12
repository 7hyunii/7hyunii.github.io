---
title: "AGENTS.md 제대로 사용하는 법"
date: "2026-08-12"
categories: "AI"
tags: ['llm', 'agent']
math: true
---

## AGENTS.md란?
> "AI 코딩 에이전트를 위한 README"

- `AGENTS.md`에 AI 코딩 에이전트가 작업하는 데 필요한 지침을 담는다.
- 덕분에 `README.md`는 사람을 위한 내용에만 집중할 수 있다 (빠른 시작, 프로젝트 설명, 기여 지침 등)


## AGENTS.md 사용법
> [AGENTS.md 공식 사이트](https://agents.md/) 참고

### 권장 항목
| 항목 | 예시 |
| --- | ---------- |
| 프로젝트 개요 | "Spring Boot 주문 API" |
| 코드 스타일 지침 | "생성자 주입, @Data 금지" |
| 금지 구역 | "migration 기존 파일 수정 금지" |
| 빌드•테스트 명령 | "./gradlew build, ./gradlew test" |
| 테스트 지침 | "통합 테스트: Testcontainers" |
| 보안 고려 사항 | "로그에 토큰·주민번호 금지" |
| 커밋•PR 지침 | "Conventional Commits, PR에 관련 이슈 기재" |

### 계층 구조 예시
- 하위 패키지의 AGENTS.md는 상위 AGENTS.md 뒤에 이어붙어 함께 적용된다
- AGENTS.md 끼리 충돌 시에는 작업 파일에 가까운 AGENTS.md가 이긴다.
```
repo/
├── AGENTS.md                   [루트] 프로젝트 공통 규칙
├── apps/
│   ├── web/
│   │   └── AGENTS.md           [패키지] web 전용 규칙만 담기
│   └── admin/
│       └── AGENTS.md           [패키지] admin 전용 규칙만 담기
...
```

### 관리 원칙
- 핵심만 담아 짧게 써야한다. (어차피 Codex 기준 지침 체인 전제가 32KiB로 제한된다.)
- AGENTS.md는 세션 시작 시 1회 로드된다. 세션 도중 파일을 수정해도 자동 반영되지 않는다.
    - 규칙 추가: `"AGENTS.md 파일을 다시 읽고 이후 작업에 반영해줘"`
    - 규칙 삭제·변경: 새 세션 시작 권장(기존 컨텍스트가 남아 섞일 수 있음)
- 내 지시와 AGENTS.md 지침이 충돌할 수 있다.
    - 원칙: 지금 한 지시가 우선. 단 보장은 아니며 확률적이다.
    - 특히 충돌을 언급하지 않으면 조용히 AGENTS.md를 따를 수 있다.
        - 해결 1) 충돌을 명시한다
            - `"AGENTS.md에 타입 명시 필수라고 돼있는데, 이 파일은 예외로 추론에 맡겨줘"`
        - 해결 2) AGENTS.md에 탈출구를 넣어둔다
            - `"단, 사용자가 이번 작업에 한해 다르게 지시하면 그 지시를 따른다"`



