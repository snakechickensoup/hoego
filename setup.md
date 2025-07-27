# 초기 설정 가이드

## Notion Integration 만들기

1. https://www.notion.so/profile/integrations 접속
2. "New Integration" 클릭
3. 이름 설정 (예: "MCP")
4. API 토큰 복사

## Claude Code MCP 설정

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

## 페이지 연결

통합을 생성한 후 사용할 Notion 페이지에 연결해야 합니다:

1. 통합의 "Access" 탭에서 페이지 선택, 또는
2. 개별 페이지에서 메뉴 → "Connect to integration" 클릭
