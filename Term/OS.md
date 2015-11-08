### Dead Lock
> Wait 에서 Ready 로 갈수 있는 조건이 충족될 수가 없을 때

Dead lock 을 발생시키는 4가지. 모두를 만족한다면 데드락 가능성이 생긴다.
 하나라도 만족하지 않으면 절대 생기지 않는다!!!!
>1. Mutual exclusion : 하나의 자원을 한 프로세스만 접근 가능하다
2. Hold and wait  : 다른 프로세스가 공유 자원을 이용하려면 대기해야 한다
3. No preemption : 프로세스가 자원을 사용 후 자발적으로 반환한다
4. Circular wait : Hold and wait 관계의 프로세스들이 circle 을 이룬다다

데드락을 막기 위한 방법

>1. Prevent : 위의 4가지 조건 중 하나씩 붙잡아 조건이 발생하지 않도록 한다.
  1. Mutual exclusion : 꼭 같이 써야하는 리소스가 아니면 atomic 을 하지 않는다
  2. Hold and wait : 한 프로세스가 atomic 자원을 여러개 소유하지 않도록 한다
  3. No preemption : 지금 프로세스가 실행될 수 없으면 atomic 자원을 반환하고 wait에서 대기한다.
  4. Circular wait : atomic 자원에 우선순위를 두고 요청을 하나씩만 받는다


2. Avoidance
3. Detection and Recovery
