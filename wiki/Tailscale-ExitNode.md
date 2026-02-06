# Tailscale Exit Node 사용법

## Exit Node란?
서버의 모든 인터넷 트래픽을 다른 기기(예: 모바일)를 통해 라우팅.
IP 차단 우회에 유용 (예: 쿠팡은 클라우드 IP 차단)

## 모바일에서 Exit Node 활성화
1. Tailscale 앱 → 설정
2. "Run exit node" 또는 "Exit node 허용" 켜기
3. [Admin Console](https://login.tailscale.com/admin/machines)에서 승인 필요할 수 있음

## 서버에서 Exit Node 사용
```bash
# Exit node 설정
sudo tailscale set --exit-node=<device-name>

# Exit node 해제
sudo tailscale set --exit-node=

# 현재 상태 확인
sudo tailscale status
```

## 현재 IP 확인
```bash
curl -s https://ifconfig.me
```

## ⚠️ 주의사항

### Exit Node가 꺼지면 서버 인터넷 끊김!
- SSH는 Tailscale 내부망이라 유지됨
- 하지만 `apt update`, `npm install` 등 외부 통신 불가
- **해결**: 평소에는 exit node 해제, 필요할 때만 사용

### 크론 작업 실패 원인
Exit node 설정된 상태에서 모바일이 오프라인 → API 호출 timeout → 작업 실패
