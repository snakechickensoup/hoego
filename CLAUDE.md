# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

Hoego는 Claude AI를 활용한 대화형 회고 시스템입니다.
사용자가 Claude와 체계적인 대화를 통해 주간/월간 회고를 작성할 수 있도록 도와주며,
Notion 연동 또는 독립적 사용이 모두 가능합니다.

## 프로젝트 구조

- `setup.md` - Notion 연동과 Claude Code MCP 설정을 위한 초기 설정 가이드
- `hoego/` 폴더 - 회고 시스템 핵심 파일들
  - `guide.md` - Notion 기반 회고 작성 프로세스 가이드
  - `settings.json` - 회고 시스템 설정 (Notion DB ID, 문장 정리 옵션)
  - `weekly/` - 주간 회고 전용 폴더
    - `template.md` - 주간 회고 템플릿
    - `prompts.md` - 주간 회고용 질문 패턴
  - `monthly/` - 월간 회고 전용 폴더
    - `template.md` - 월간 회고 템플릿
    - `prompts.md` - 월간 회고용 질문 패턴
  - `backup/` - 백업 파일 저장소

## Notion 연동 설정

프로젝트에는 MCP를 통한 Notion 연동 설정 방법이 포함되어 있습니다:

1. https://www.notion.so/profile/integrations 에서 통합 생성
2. Notion 서버 URL과 API 키로 Claude Code MCP 설정
3. API 키는 환경변수 `NOTION_API_KEY`로 설정해야 함

## Claude 작업 가이드라인

### 설정 파일 확인
- 회고 작업 시 `hoego/settings.json` 파일을 먼저 읽어서 설정 확인
- `sentence_cleanup` 설정에 따라 문장 정리 수준 조절:
  - "off": 사용자 원문 그대로 보존
  - "light": 핵심만 간단히 정리  
  - "normal": 자세하지만 깔끔하게 정리
- Notion 연동 시 설정된 database_id 사용

### 문서 준수
- 각 기능별 문서들을 정확히 따를 것
- 임의로 프로세스를 변경하지 말고 기존 문서의 패턴 사용
- 특히 해당 기능의 가이드, 프롬프트, 템플릿 구조를 준수

### 회고 작성 프로세스 (필수 준수)

#### 슬래시 커맨드 사용 (권장)
- `/주간회고`: 주간 회고 자동 시작 (hoego/weekly/ 폴더 사용)
- `/월간회고`: 월간 회고 자동 시작 (hoego/monthly/ 폴더 사용)

#### 수동 진행 시 프로세스
1. **시작**: backup.md 자동 확인 → 있으면 이어서 할지 물어보기
2. **메모리 리콜**: 해당 회고 타입의 prompts.md 패턴 사용
   - 주간: hoego/weekly/prompts.md (전체 주를 한번에, 요일별 분할 금지)
   - 월간: hoego/monthly/prompts.md (한 달 전체 흐름과 패턴 중심)
3. **체계적 진행**: 해당 회고 타입의 template.md 구조 정확히 따르기
4. **완성**: 해당 template.md 형식으로 최종 문서 작성

### 질문 방식
- 자연스러운 대화로 기억 되살리기
- 표면적 답변을 구체적 질문으로 확장
- 사용자 말투 그대로 보존 (과도한 정제 금지)

### 백업 관리
- 회고 시작시 backup.md 자동 확인하여 이어서 할지 물어보기
- 중단시 "백업에 저장할까요?" 물어보고 backup.md에 저장
- 새 백업시 기존 파일 덮어쓰기
- backup.md는 .gitignore에 포함되어 로컬에서만 관리

## 개발 참고사항

- 모든 내용은 한국어로 작성
- package.json에 빌드, 테스트, 린트 명령어가 현재 정의되지 않음
- 기능별로 독립적인 가이드와 프롬프트를 관리하는 구조
