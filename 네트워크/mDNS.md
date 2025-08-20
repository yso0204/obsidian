# Multicast DNS
> 멀티캐스트 도메인 네임 시스템
> 쉽게 로컬 네트워크에서 기기들이 서로를 이름으로 찾을 수 있게 도와주는 기술

# mDNS란?
- 일반적으로 google.com 같은 도메인 이름을 DNS 서버에 물어봐서 IP 주소를 변환하고 접속한다
- 하지만, 집 내부 네트워크 같은 작은 **로컬 네트워크** 에서는 외부 DNS 서버에 매번 물어볼 필요가 없다
- 이때 mDNS를 사용하여 기기들이 **멀티캐스트 방식** 으로 서로 브로드캐스티을 하여 서로의 IP를 알 수 있다.

## Broadcast / Multicast
네트워크에서 "누구 있어?" 라고 물을 때는 여러 방식이 있다.
- **Unicast** : A to B (1:1)
	- PC에서 특정 서버에 직접 접속
- **Broadcast** : A to ALL (1:모두)
	- DHCP 요청(IP 주소 줄 사람?)
- **MultiCast** : A to 특정 그룹(1:선택된 여러 기기)
	- mDNS, IPTV 방송

> mDNS는 Multicast 방식을 사용한다.
> 즉, 네트워크 전체가 아닌 mDNS 듣고 싶은 기기들만 메세지를 받음

## mDNS 정의
- DNS 서버 없이, 로컬 네트워크에서 멀티캐스트를 사용해 이름 to IP를 변환하는 프로토콜
- 규격 : RFC 6762
- port : UDP 5353
- 멀티캐스트 주소 : 224.0.0.251(IPv4) / FF02::FV(IPv6)
- 네임스페이스 : 보통 `.local` 도메인 사용
	- ex ) `raspberrypi.local` , `mytv.local`



## mDNS 동작 과정
> 스마트폰이 `printer.local`을 찾고 싶다?

1. 스마트폰:
   UDP 5353 포트로 멀티캐스트 메세지 전송
   -> `printer.local`의 IP 아는 기기?
2. 네트워크에 있는 모든 기기가 메세지를 들음
3. 프린터:
   -> 자기의 IP는 `192.168.1.145` 라고 응답
4. 스마트폰:
   -> 이제 직접 `192.168.1.145`로 연결 (Unicast)

## mDNS의 장점
- DNS 서버 불필요 : **Zero-configuration Networking(Zeroconf)**
- IoT / 스마트홈 환경에서 **자동 발견(Auto-discovery)** 가능
- 운영체제에서 기본 지원

## 실제 사용 사례
- 스마트폰 <-> Chromecast TV 연결
  (App이 `chromecast.local` 같은 이름으로 찾음)
-  AirDrop, Airplay (Apple Bonjour 기반)
- 네트워크 프린터 자동 검색
- 스마트 전구, IoT 기기 제어

## 다른 기술 비교

| 기술        | 특징                        | **예시**          |
| --------- | ------------------------- | --------------- |
| **DNS**       | 전 세계 도메인 네임 관리(서버 필요)     | `google.com`    |
| **Broadcast** | 네트워크 전체에 쏘기(효율 낮음)        | DHCP            |
| **mDNS**      | 로컬에서 이름 <-> IP 변환(서버 불필요) | `printer.loacl` |
| **SSDP/UPnP** | 서비스 검색(기기 기능도 알림)         | 스마트TV , NAS     |
 
