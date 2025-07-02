> 누가 ssh로 로그인 시도 계속 실패하면 IP를 차단

즉, 무작위 로그인 시도 brute force 공격으로 **SSH Nginx 로그인 페이지, 웹 앱 로그인**을 보호

# 설치 방법
```
sudo apt update
sudo apt install fail2ban
```
기본 설정으로도 SSH 로그인 시도 실패 5번 시 10분 차단

# 부팅 시 자동 실행
```
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```
- `enable` : 시스템 부팅 시 자동으로 켜지게 설정
- `start` : 지금 당장 실행

```
sudo systemctl status fail2ban
Active: active (running)
```
이렇게 나오면 실행 중인 것
로그는 `/var/log/fail2ban.log` 에서 확인 가능하다