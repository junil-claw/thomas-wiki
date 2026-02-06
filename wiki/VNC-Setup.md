# VNC 원격 데스크탑 설정

## 설치
```bash
sudo apt install -y xfce4 xfce4-goodies tigervnc-standalone-server
```

## VNC 서버 설정

### 비밀번호 설정
```bash
vncpasswd
```

### 원격 접속 허용 (중요!)
기본값은 localhost만 허용. 외부 접속을 위해 설정 변경 필요:

```bash
# ~/.vnc/tigervnc.conf 생성
cat > ~/.vnc/tigervnc.conf << 'EOF'
$localhost = "no";
$SecurityTypes = "VncAuth,TLSVnc";
1;
EOF
```

### VNC 서버 시작
```bash
vncserver :1 -geometry 1920x1080 -depth 24
```

### VNC 서버 종료
```bash
vncserver -kill :1
```

## 접속 정보
- **주소**: `<Tailscale IP>:5901`
- **비밀번호**: vncpasswd로 설정한 값

## 트러블슈팅

### localhost만 바인딩되는 문제
`ss -tlnp | grep 5901`로 확인:
- `127.0.0.1:5901` → localhost만 (외부 접속 불가)
- `0.0.0.0:5901` → 모든 인터페이스 (정상)

해결: `~/.vnc/tigervnc.conf`에 `$localhost = "no";` 추가

### 한글 깨짐
```bash
sudo apt install -y fonts-noto-cjk fonts-nanum
```
설치 후 브라우저 새로고침

---
*마지막 업데이트: 2026-02-06*
