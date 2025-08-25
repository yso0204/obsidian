# DNS란?
> 인터넷의 전화번호부

사람이 기억하기 쉬운 도메인 이름 `www.google.com` 같은 것을 컴퓨터가 통신할 때 쓰는 IP주소로 변환하는 **분산 데이터베이스 + 프로토콜** 
- 사용자가 URL 입력 -> DNS가 이를 IP로 해석(Name resolution) -> 그 IP로 TCP/UDP/QUIC 같은 실제 통신 시작
- 게이트웨이는 밖으로 나가는 문 / DNS는 주소를 알려주는 시스템

# DNS의 계층 구조와 권한(Authority)
DNS는 트리 구조로 되어 있고, 각 노드를 **label** 이라 부름
- 맨 꼭대기 : **루트 도메인**  `.` 
- TLD(Top-Level Domanin) : `com`,`net`,`kr`,`org` ....
- SLD : `google` (`google.com`)
- 호스트명(서브 도메인) : `www.google.com.` 처럼 점으로 구분, 마지막 점은 루트를 의미
## 권위(Authoritative)
- 권한 있는 네임서버(Authoritative NS) : 특정 존(zone)의 정답을 최종 권위로 가지고 있는 서버
- 존(Zone) : 어떤 도메인 부분에 연속된 네임스페이스으 단위, 위임(delegation)으로 하위 존을 따로 운영할 수 있다.
  예) `example.com`을 운영하는 NS가 `api.example.com`을 다른 팀 NS로 위임
### 권위(Authoritative) 네임 서버란?
- DNS 서버는 '이 도메인이 어떤 IP를 가지는가?' 라는 질문에 답을 해줌
- 하지만, 모든 DNS 서버가 답을 아는 것은 아니며, 
  어떤 서버는 '그 서버가 직접 관리하는 존(Zone)에 대해서만 최종 답변을 줄 수 있음' -> 이걸 **권위있는 네임 서버** 라고 부름
- 반대로, 그냥 다른 서버에 물어봐서 알려주는 경우도 있는데, 이건 **캐싱 리졸버(Resolver)** 같은 역할, 얘는 정답을 보관만 하고, 실제 '최종 권위'는 아님

즉,
- Authoritative NS = '내가 운영하는 존의 공식 답변을 줄 수 있는 최종 서버'
- 캐시 서버 = '어디선가 들은 정보를 잠시 보관하다가 알려주는 서버'

### 존(zone) 이란?
- 도메인 네임스페이스는 트리구조
```
. (root)
 └── com
      └── example.com
           └── api.example.com
```
- 이때, '어떤 도메인 부분에 대해서 내가 책임지고 관리한다!' 라는 단위가 존(Zone)
	- `example.com` 존을 관리한다면, `www.example.com` , `mail.example.com` 같은 서브도메인의 레코드를 직접 넣을 수 있음
	- 하지만, 특정 서브 도메인(`api.example.com`)은 다른 팀에 맡기고 싶을 수 있는데, 이걸 위임(delegation) 이라고 한다.
- 예를 들어, A라는 회사가 `example.com` 도메인을 가지고 있고, A의 DNS 팀에서 `example.com` 존을 운영중 -> 이게 Authoritative NS
	- 하지만, API 서버는 별도 팀이 관리
	  그래서, `api.example.com` 이라는 서브 도메인은 A 메인 DNS가 아닌 다른 팀 네임서버에 위임할 수 있다.
	- 즉, `api.example.com` 의 IP를 누군가가 묻는다면 `example.com` Authoritative NS는 저쪽 팀 NS에게 물어보라고 위임정보를 주고, 해당 IP는 `api.example.com` Authoritative NS가 준다.
