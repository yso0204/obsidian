>어플리케이션을 패킹할 수 있는 툴

- 배포를 하며 런타인 환경에서 필요로 하는 여러가지 설정, 라이브러리 등을 하나로 묶어서 container로 배포
	- app.js
	- node
	- assets
	- npm, configuration 등등

## VM vs Docker

- VM
![](https://i.imgur.com/ZHnKfSA.png)
  - 여러가지를 다 가지고 있기에 무거움
  - 무거운 운영체제를 포함

- Container
![](https://i.imgur.com/rDAIhzS.png)

  - VM에서 경량화 된 컨셉
  - 각각의 App들을 고립된 환경에서 구동 가능
  - 컨테이너는 운영체제를 가지지 않고, HOST의 OS를 공유함
  - Container Engine이 필요한 사항들을 HOST OS를 통해 실행해주는데, 이때 가장 많이 사용되는 것이 Docker Engine임

## Docker의 3대 구성 요소
![](https://i.imgur.com/nLvXdnR.png)
![](https://i.imgur.com/ZfdNAXq.png)

![](https://i.imgur.com/8rTvmLQ.png)

- Docker file
	> container를 어떻게  만들어야하나?

	순서나, 레시피 
	- copy files
	- install dependencies (어떤 프레임워크나 라이브러리를?)
	- set env variables (필요한 환경 변수 설정)
	- Run setuop scripts(어떻게 구동해야 하는지?)
- Image
	- 실행하는데 필요한 code
	- run time 환경
	- 시스템 툴, 라이브러리 등 모든 세팅
	- 그 당시의 상태를 snap shot 하는 느낌 
- container
	- container 안에서 application이 고립적으로 동작한다

## Shipping Containers
- local에서 image 를 container Registry에 push, 이걸 server에 pull
  ![](https://i.imgur.com/yopDzkL.png)
