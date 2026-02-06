# 서버 설정 (Oracle ARM)

## 환경

| 항목 | 값 |
|------|-----|
| Provider | Oracle Cloud Infrastructure (OCI) |
| Instance | VM.Standard.A1.Flex |
| Arch | ARM64 (aarch64) |
| vCPU | 4 |
| RAM | 24GB |
| Disk | 200GB |
| OS | Ubuntu 24.04 LTS |

## Tailscale 설정

```bash
# 설치
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up --ssh --hostname=openclaw

# Serve 활성화 (웹 UI 노출)
# 먼저 https://login.tailscale.com/f/serve 에서 활성화 필요
```

## 방화벽

OCI VCN에서 UDP 41641 (Tailscale)만 열어둠.
SSH(22)는 Tailscale SSH로 대체.

## 보안 점검

```bash
openclaw security audit --deep
```

### 알려진 이슈
- 자격증명 폴더 권한: `chmod 700 ~/.openclaw/credentials` 필요

---
*마지막 업데이트: 2026-02-06*
