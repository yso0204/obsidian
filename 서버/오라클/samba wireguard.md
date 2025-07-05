# 서버
wiredguard 설치
```
sudo apt update && sudo apt install wireguard -y
```
키 쌍 생성
```
wg genkey | tee privatekey | wg pubkey > publickey
```
- 서버, 클라이언트 간 암호화 통신에 사용
wireguard 서버 설정 파일 만들기
```
cat privatekey
```
- 여기서 나온 privatekey 복사 해두고
```
sudo nano /etc/wireguard/wg0.con
```
아래 내용 입력(추후 클라리언트 정보 추가 예정)
```
[Interface]
PrivateKey = <privatekey>
Address = 10.0.0.1/24
ListenPort = 51820
SaveConfig = true
```

포트열기
ufw
```
sudo ufw allow 51820/udp
```
iptables
```
sudo iptables -A INPUT -p udp --dport 51820 -j ACCEPT
```

wireguard 서비스 시작
```
sudo systemctl start wg-quick@wg0

확인
sudo systemctl status wg-quick@wg0
```

서버 부팅 시 자동실행 설정
```
sudo systemctl enable wg-quick@wg0
```

서버에서 작동 확인
```
sudo wg
```

오라클 서버 수신 규칙 추가

| 항목           | 설정 값                  | 설명                |
| ------------ | --------------------- | ----------------- |
| **소스 CIDR**  | `0.0.0.0/0`           | 전 세계 어디서나 접속 허용   |
| **IP 프로토콜**  | `UDP`                 | WireGuard는 UDP 사용 |
| **소스 포트 범위** | `모두` 또는 비워두기          | 기본값               |
| **대상 포트 범위** | `51820`               | WireGuard 서버 포트   |
| **설명**       | `WireGuard VPN 포트 허용` | 식별을 위한 설명         |

| 항목           | 설정 값           | 설명                   |
| ------------ | -------------- | -------------------- |
| **소스 CIDR**  | `10.0.0.0/24`  | VPN 네트워크 대역          |
| **IP 프로토콜**  | `모든 프로토콜`      | TCP, UDP, ICMP 전부 허용 |
| **대상 포트 범위** | `모두` 또는 비워두기   | 기본값                  |
| **설명**       | `VPN 내부 통신 허용` | 클라이언트 <-> 서버 통신 허용   |

# 클라이언트
서버 설정 파일 수정
```
[Peer]
PublicKey = (client1_publickey 내용)
AllowedIPs = 10.0.0.2/32
```
추가해주기

서버에서 아래 명령으로 클라이언트 키 생성
```
wg genkey | tee client1_privatekey | wg pubkey > client1_publickey
```

클라이언트 config(`client1.conf) 생성
```
[Interface]
PrivateKey = 클라이언트_PRIVATE_KEY
Address = 10.0.0.2/24
DNS = 1.1.1.1

[Peer]
PublicKey = 서버 퍼블릭 key
Endpoint = [서버 퍼블릭 IP]:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
```
- `PrivateKey` → 클라이언트의 개인키
-  `PublicKey` → 서버의 공개키
-  `Endpoint` → 서버의 퍼블릭 IP (`158.x.x.x:51820`)
- `AllowedIPs = 0.0.0.0/0` → 전체 트래픽을 VPN으로 보냄
- `PersistentKeepalive = 25` → NAT 뚫을 때 유용

서버에 클라이언트 등록
```
sudo wg set wg0 peer 클라이언트_PUBLIC_KEY allowed-ips 10.0.0.2/32
```
wireguard 재시작
```
sudo systemctl restart wg-quick@wg0
```