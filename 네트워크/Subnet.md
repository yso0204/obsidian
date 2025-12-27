# subnet이란?
기존 class 기반의 IP주소 체계는 주소의 낭비가 심했다.
예를 들어 class C는 254개의 host를 할당할 수 있는데, 50개의 호스트의 할당만 필요한 경우 204개의 주소가 낭비되고, 255개의 host가 필요한 경우 Class C 두 개를 받아야 하는데, 이 경우 254개의 주소가 낭비된다.

그리고 network가 커질 경우 broadcast 의 traffic도 커지는데, 1000개가 하나의 network에 있다면 하나의 device가 broadcast를 할 경우 999개의 device가 이를 받아야하고, 이는 network가 느려지고 장비에 부하가 생길 수 있다.

subnet은 이러한 문제를 해결하기 위해 