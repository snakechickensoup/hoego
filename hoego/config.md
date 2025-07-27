# 회고 시스템 설정 ⚙️

## 🎯 설정 파일 위치

회고 시스템의 모든 설정은 `settings.json` 파일에서 관리됩니다.

```json
{
  "notion_review_database_id": "30391af6-a094-479b-8e92-b547ce661c79",
  "notion_daily_memo_database_id": "21eb5a0ca99680f9b9a8f149c1604448", 
  "sentence_cleanup": "normal"
}
```

## 📋 설정 항목 설명

### 1. Notion 데이터베이스 ID
- **notion_review_database_id**: 회고 문서가 저장될 데이터베이스
- **notion_daily_memo_database_id**: 일일 메모가 저장된 데이터베이스

### 2. 문장 정리 기능
- **"off"**: 사용자 말 그대로 보존
- **"light"**: 핵심만 간단히 정리  
- **"normal"**: 자세하지만 깔끔하게 정리

**예시**:
- 입력: "그때 뭐였지... 아 맞다 새 라이브러리 써봤는데 좀 복잡하더라고요..."
- "normal" 정리: "새로운 라이브러리를 사용해봤는데 복잡하게 느껴졌습니다."

## 🛠️ 설정 변경 방법

1. `review/settings.json` 파일 수정
2. 회고 시작 시 자동으로 적용
3. 실시간 변경도 가능: "문장 정리를 light로 바꿔줘"

## 🔍 Notion 데이터베이스 ID 찾기

데이터베이스 URL에서 확인:
```
https://www.notion.so/{DATABASE_ID}?v=...
```

## MCP 설정

Notion MCP 설정은 `../setup.md`를 참조하세요.