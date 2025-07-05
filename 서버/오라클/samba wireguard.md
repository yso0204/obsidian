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

# 클라이언트
서버에서 아래 명령으로 클라이언트 키 생성
```
wg genkey | tee client1_privatekey | wg pubkey > client1_publickey
```