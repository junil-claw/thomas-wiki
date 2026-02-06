# gog (Google Workspace CLI)

## 설치 (ARM Linux)

```bash
# Go 설치
curl -fsSL https://go.dev/dl/go1.23.5.linux-arm64.tar.gz | sudo tar -C /usr/local -xzf -
export PATH=$PATH:/usr/local/go/bin

# gog 빌드
git clone https://github.com/steipete/gogcli.git
cd gogcli && git checkout v0.8.0
go build -o bin/gog ./cmd/gog
sudo cp bin/gog /usr/local/bin/
```

## 초기 설정

### 1. Google Cloud 프로젝트
1. https://console.cloud.google.com 에서 새 프로젝트 생성
2. Calendar API 활성화
3. OAuth 동의 화면 설정 (테스트 사용자 추가!)
4. OAuth 클라이언트 ID 생성 (데스크톱 앱)
5. JSON 다운로드

### 2. 인증

```bash
# 환경변수 (headless 서버용)
export GOG_KEYRING_PASSWORD="your_password"
export GOG_ACCOUNT="your@email.com"

# 자격증명 저장
gog auth credentials ~/client_secret.json

# 계정 추가 (--manual for headless)
gog auth add your@email.com --services calendar --manual
```

## 주요 명령어

### 캘린더

```bash
# 캘린더 목록
gog calendar calendars

# 이벤트 조회
gog calendar events <calendar_id> --from 2026-02-06 --to 2026-02-13

# 이벤트 생성
gog calendar create <calendar_id> --summary "회의" --from "2026-02-10T14:00:00" --to "2026-02-10T15:00:00"
```

## 트러블슈팅

- **accessNotConfigured**: Calendar API 활성화 필요
- **access_denied**: OAuth 동의 화면에서 테스트 사용자 추가 필요
- **no TTY for keyring**: `GOG_KEYRING_PASSWORD` 환경변수 설정

---
*마지막 업데이트: 2026-02-06*
