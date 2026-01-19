# Claude Prompts

개인용 Claude 프롬프트/스킬 모음

## 사용 방법

### Claude 웹 인터페이스
1. [claude.ai](https://claude.ai) 접속
2. Projects → 새 프로젝트 생성 (또는 기존 프로젝트 선택)
3. Project Knowledge에 원하는 `.md` 파일 업로드
4. 대화에서 "explain-paper 스킬을 활용하여 이 논문을 설명해줘" 형태로 사용

### Claude Code CLI
```bash
# ~/.claude/commands/에 심볼릭 링크 생성
mkdir -p ~/.claude/commands
ln -s ~/Documents/claude-prompts/explain-paper.md ~/.claude/commands/explain-paper.md
```

## 스킬 목록

| 스킬 | 설명 |
|------|------|
| [explain-paper.md](./explain-paper.md) | 논문을 비유와 예시로 상세하게 설명 |

## 라이선스

개인 사용 목적
