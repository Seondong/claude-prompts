# Notion API 연동 가이드

논문 요약을 Notion 페이지에 자동으로 추가하는 방법입니다.

---

## 1. Notion Integration 생성

1. [Notion Developers](https://www.notion.so/my-integrations) 접속
2. **"New integration"** 클릭
3. 설정:
   - Name: `Paper Summary Bot` (원하는 이름)
   - Associated workspace: 사용할 워크스페이스 선택
   - Capabilities: **Read content**, **Insert content** 체크
4. **Submit** → **Internal Integration Secret** 복사 (이것이 API 키)

---

## 2. Notion 페이지에 Integration 연결

1. 논문 요약을 저장할 Notion 페이지/데이터베이스 열기
2. 우측 상단 `...` → **Add connections** → 방금 만든 Integration 선택
3. 페이지 URL에서 **Page ID** 확인:
   ```
   https://www.notion.so/My-Page-{32자리_페이지_ID}
   ```

---

## 3. 환경 변수 설정

```bash
# ~/.zshrc 또는 ~/.bashrc에 추가
export NOTION_API_KEY="your_integration_secret_here"
export NOTION_PAGE_ID="your_page_id_here"
```

---

## 4. Claude Code에서 사용

논문 요약 후 Notion에 저장하려면:

```
이 논문을 explain-paper 스킬로 설명하고, 결과를 Notion에 저장해줘
```

또는 수동으로 저장하고 싶다면:

```
방금 요약한 내용을 Notion API로 저장해줘
```

---

## 5. API 호출 예시 (참고용)

```bash
curl -X POST 'https://api.notion.com/v1/blocks/{PAGE_ID}/children' \
  -H 'Authorization: Bearer {NOTION_API_KEY}' \
  -H 'Notion-Version: 2022-06-28' \
  -H 'Content-Type: application/json' \
  -d '{
    "children": [
      {
        "object": "block",
        "type": "heading_2",
        "heading_2": {
          "rich_text": [{"type": "text", "text": {"content": "논문 제목"}}]
        }
      },
      {
        "object": "block",
        "type": "paragraph",
        "paragraph": {
          "rich_text": [{"type": "text", "text": {"content": "요약 내용..."}}]
        }
      }
    ]
  }'
```

---

## 주의사항

- Integration Secret은 절대 공개 저장소에 커밋하지 마세요
- Notion API는 한 번에 100개 블록까지만 추가 가능
- 긴 요약은 여러 번 나눠서 전송됩니다
