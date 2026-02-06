# OpenClaw 멀티 에이전트 설정

## 개념
하나의 Gateway에서 여러 독립 에이전트 운영 가능:
- 각 에이전트: 별도 workspace, 세션, 페르소나
- 전문화된 팀 구성 (코딩, 리서치, 글쓰기 등)

## 에이전트 추가
```bash
# 인터랙티브 모드
openclaw agents add <name>

# 비인터랙티브 모드
openclaw agents add <name> --workspace ~/.openclaw/workspace-<name> --non-interactive
```

## 에이전트 목록 확인
```bash
openclaw agents list --bindings
```

## 에이전트 커스터마이징
각 에이전트의 workspace에서:
- `IDENTITY.md` - 이름, 이모지, 전문분야
- `SOUL.md` - 성격, 스타일, 전문지식

## 에이전트 간 통신
main 에이전트에서 다른 에이전트에게 작업 위임:
```
sessions_spawn(agentId="coder", task="Python 코드 작성해줘")
```

## 팀 구조 예시
```
main (토마스 🦉) - 매니저/라우터
├── coder (💻) - 코딩 전문
├── researcher (🔍) - 리서치 전문
└── writer (✍️) - 글쓰기 전문
```

## 바인딩 (채널 라우팅)
특정 채널/그룹을 특정 에이전트에게 연결:
```bash
openclaw agents add work --bind telegram:work-bot
```
