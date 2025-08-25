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
