# 초기 설정 가이드

## 🎯 설정 파일 설정

### 1. 설정 파일 생성
```bash
cp settings.example.json settings.json
```

### 2. 설정 파일 수정
회고 시스템의 모든 설정은 `settings.json` 파일에서 관리됩니다.

```json
{
  "notion_review_database_id": "your-review-database-id-here",
  "notion_daily_memo_database_id": "your-daily-memo-database-id-here", 
  "sentence_cleanup": "normal"
}
```

## 📋 설정 항목 설명

### 1. Notion 데이터베이스 ID

#### notion_review_database_id (회고 보관함)
- **역할**: Claude가 작성한 최종 회고 문서를 자동으로 저장하는 곳
- **구조**: 제목, 날짜, 회고 내용, 태그 등이 포함된 데이터베이스
- **사용법**: 
  - 회고 완성 시 Claude가 자동으로 새 페이지 생성
  - 주간/월간 회고를 체계적으로 관리
  - 검색과 필터링으로 과거 회고 쉽게 찾기

#### notion_daily_memo_database_id (일일 메모 수집)
- **역할**: 평소 기록한 메모들을 Claude가 회고 재료로 활용 (선택사항)
- **사용법**:
  - 메모가 있으면: Claude가 자동 수집해서 회고 시작점으로 활용
  - 메모가 없으면: 일반적인 메모리 리콜로 진행 (전혀 문제없음)
  - 어떤 형태든 상관없음: 긴 글, 짧은 메모, 감정, 링크, 생각 조각 등 자유롭게

#### 독립 사용
- 두 ID를 모두 빈 문자열("")로 설정 시 독립 사용 모드
- Notion 없이도 Claude와 대화만으로 회고 작성 가능

### 2. 문장 정리 기능
- **"off"**: 사용자 말 그대로 보존
- **"light"**: 핵심만 간단히 정리  
- **"normal"**: 자세하지만 깔끔하게 정리

**예시**:
- 입력: "그때 뭐였지... 아 맞다 새 라이브러리 써봤는데 좀 복잡하더라고요..."
- "normal" 정리: "새로운 라이브러리를 사용해봤는데 복잡하게 느껴졌습니다."

## 🛠️ 설정 변경 방법

1. `settings.json` 파일 수정
2. 회고 시작 시 자동으로 적용
3. 실시간 변경도 가능: "문장 정리를 light로 바꿔줘"

## 🔍 Notion 데이터베이스 ID 찾기

데이터베이스 URL에서 확인:
```
https://www.notion.so/{DATABASE_ID}?v=...
```

---

## Notion Integration 설정 (선택사항)

Notion 연동을 원하는 경우에만 아래 설정을 진행하세요.

### 1. Notion Integration 만들기

1. https://www.notion.so/profile/integrations 접속
2. "New Integration" 클릭
3. 이름 설정 (예: "MCP")
4. API 토큰 복사

### 2. Claude Code MCP 설정

Claude Code에서 Notion MCP를 사용하려면 `claude_desktop_config.json`에 다음과 같이 설정하세요:

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer your_notion_api_token_here\", \"Notion-Version\": \"2022-06-28\"}"
      }
    }
  }
}
```

**중요**: `your_notion_api_token_here`를 실제 Notion API 토큰으로 교체하세요.

### 3. 페이지 연결

통합을 생성한 후 사용할 Notion 페이지에 연결해야 합니다:

1. 통합의 "Access" 탭에서 페이지 선택, 또는
2. 개별 페이지에서 메뉴 → "Connect to integration" 클릭