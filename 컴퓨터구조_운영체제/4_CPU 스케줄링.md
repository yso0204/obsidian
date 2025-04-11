# CPU 스케줄링 개요
> 운영체제가 process 들에게 합리적으로 CPU 작원을 배분하는 것을 CPU 스케줄링이라고 한다

### 프로세스 우선순위
> 프로세스마다 우선순위가 다른데, 대표적으로 입출력 작업이 많은 프로세스가 있다

프로세스마다 CPU 혹은 입출력 장치를 주로 사용하는 종류가 나뉜다
- 입출력 집중 프로세스(I/O bound process)
- CPU 집중 프로세스(CPU bound process)

#### CPU burst, I/O burst
> 쳬