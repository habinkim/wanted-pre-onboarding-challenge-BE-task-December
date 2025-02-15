## 1-1) 사전과제 진행 가이드

- 아래 총 5 문제에 대한 해설을 작성한 뒤 Pull Request를 날려주세요.
- 문제 해설에 대한 정해진 양식은 없으며, 최대한 자세히 해설해주시면 좋습니다.
- 문제 유형은 해당 코스에서 다룰 주제들을 포함하고 있으니 완벽히 이해하시면 코스를 수강하는데 큰 도움이 될 것입니다.

**문의 사항은 사전 과제 Repository의 Issue로 등록해 주세요.*



## 1-2) 사전 과제

- (1) 동기와 비동기 프로그래밍에 대한 차이점을 설명해주세요.

  - 결과값 대기 : A 함수에서 B 함수를 호출했을 때, A 함수가 B 함수의 결과값을 기다리느냐의 여부를 의미한다.
  - 동기(Synchronous) 프로그래밍과 비동기(Asynchronous) 프로그래밍은 태스크의 수행 순서 보장에 대한 매커니즘이다.
  - 호출되는 함수의 작업 여부를 신경쓰나에 따라, 함수 실행/return 순차적인 흐름을 따르느냐, 안 따르느냐 관심사이다.

  

  - 동기(Synchronous) 프로그래밍
    - 태스크를 직렬적으로 수행하는 방식이다. 
    - 호출하는 함수 A가 호출되는 함수 B의 작업 완료 후 return을 기다리거나, 바로 return 받더라도 미완료 상태라면 여부를 스스로 계속 확인하며 신경쓴다.

  - 비동기(Asynchronous) 프로그래밍
    - 태스크를 병렬적으로 수행하는 방식이다.
    - 태스크가 종료되지 않은 상태라 하더라도 대기하지 않고 다음 태스크를 실행한다.



- (2) 블로킹과 논블로킹의 차이점을 설명해주세요.

  - 제어권 : 자신(함수)의 코드를 실행할 권리이다. 제어권을 가진 함수는 자신의 코드를 끝까지 실행한 후, 자신을 호출한 함수에게 return한다.
  - 블로킹(blocking)과 (non-blocking)은 프로세스의 유휴 상태에 대한 개념이다.
  - 제어권이 누구한테 있느냐가 관심사이다.

  

  - 블로킹(Blocking) : 자신의 작업을 진행하다가 다른 주체의 작업이 시작되면 다른 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 방식
    1. A함수가 B함수를 호출하면 B에게 제어권을 넘긴다.
    2. 제어권을 넘겨받은 B는 열심히 함수를 실행한다. A는 B에게 제어권을 넘겨주었기 때문에 함수 실행을 잠시 멈춘다.
    3. B함수는 실행이 끝나면 자신을 호출한 A에게 제어권을 돌려준다.
  - 논블로킹(Non-Blocking) : 다른 주체의 작업에 관련없이 자신의 작업을 하는 방식
    1. A함수가 B함수를 호출하면, B 함수는 실행되지만, **제어권은 A 함수가 그대로 가지고 있는다.**
    2. A함수는 계속 제어권을 가지고 있기 때문에 B함수를 호출한 이후에도 자신의 코드를 계속 실행한다.



- (3) 본인이 주로 사용하는 언어에서 비동기 프로그래밍을 사용하는 방법을 설명해주세요.

  - Future (비동기 프로그래밍)
    - Future는 비동기적인 연산의 결과를 표현하는 클래스이다. Future를 이용하면 멀티쓰레드 환경에서 처리된 어떤 데이터를 다른 쓰레드에 전달할 수 있다
    - Future 내부적으로 Thread-Safe 하도록 구현되었기 때문에 `synchronized block`을 사용하지 않아도 된다.
  - CompletableFuture
    - 비동기로 처리할 작업이 두 가지 이상이며, 작업들 간의 의존성이 존재할 경우 Future만으로 처리하기가 어려워진다.
    - 이럴 경우에 CompletableFuture을 사용해서 해결할 수 있으며, CompletableFuture를 이용하면 비동기 처리 중 발생한 Exception을 전달하는 것도 가능하게 된다.
  - RxJava
    - RxJava는 자바에서 리액티브 프로그래밍을 구현하는 데 사용하는 라이브러리다.
    - 이벤트 처리와 같은 비동기 처리에 최적화됐으며, 2.0 버전부터 Reactive Stream 사양을 구현한다.
    - 리액티브 프로그래밍은 데이터가 통지될 때마다 관련 프로그램이 반응(reaction)해 데이터를 처리하는 프로그래밍 방식이다.
    - Futures와 유사하게 RxJava는 여러 동기식 또는 비동기식 작업을 함께 연결하여 처리 파이프라인을 생성하는 데 사용할 수 있다.
    - 일회용인 Futures와 달리 RxJava는 0개 이상의 항목 스트림 에서 작동한다.
    - 많은 연산자 세트 덕분에 훨씬 더 유연하고 강력하다.
    - Java 8의 스트림과 달리 RxJava에는 배압(backpressure) 메커니즘이 있어 처리 파이프라인의 다른 부분이 다른 스레드에서 다른 속도로 작동하는 경우를 처리할 수 있다.

  - Reactor
    - Reactor는 RxJava와 마찬가지로 Reactive Stream 표준 사양을 구현한 리액티브 프로그래밍에서 구현하는 데 사용하는 라이브러리다.
    - Reactor에는 스트림 전체에서 흐름 트리거에 사용되는 모든 신호를 추적하는 데 도움이 되는 `Hooks.onOperatorDebug()` 표준 라이브러리가 포함되어 있기 때문에 디버깅 기능이 RxJava에 비해 상당히 향상되었고 효율적이다.

  

- (4) 메세지 큐를 쓰는 이유에 대하여 2가지 예시를 서술해주세요.
  - 주문 시스템과 같은 MSA(MicroService Architecture)에서 사용한다.
    - 결제 서비스가 사용자가 많아져서 컨테이너 오케스트레이션 툴에 의해서 Scale-out을 하게 되고 다음과 같이 두 개의 컨테이너가 생성되었다.
    - 동일한 서비스의 데이터가 분산되어 저장되기 때문에 Client는 API Gateway가 보내는 요청에 따라서 다른 데이터를 가져올 가능성이 존재한다.
      - 동일한 데이터베이스를 사용 -> 여러 컨테이너가 동일한 DB를 보고 작업을 하게 된다면 트랜잭션과 Isolation Level에 관한 문제가 발생하게 된다.
      - Message Queue를 사용 -> Apache Kafka, RabbitMQ 등의 메시지 브로커를 사용해서 메시징을 구현하고, 인스턴스 각각의 데이터베이스를 운영하여 큐잉 서버를 구독(Subscribe)
  - 이미지 처리, 비디오 인코딩, 빅데이터 등 서버 부하가 많은 작업에서 사용한다.
    - 동시에 처리할 수 있는 양이 한정적이어서 무작정 요청을 처리를 할 수 없다.
    - Message Queue를 사용하면 서버가 처리할 수 있는 양을 Message Queue에서 가져와 처리하면 된다.



- (5) 본인이 작성한 서버 코드가 있는 github repo 주소를 제출해주세요. (CRUD 기능을 모두 포함하여야 하며, 서버에 대한 설명을 README에 작성해주시면 더욱 좋습니다.) 
  - https://github.com/habinkim/SPRING_DEMO



- (6 - Optional) 해당 수업을 통해 꼭 배우고 싶은 주제 또는 지식이 있다면 자유롭게 서술해주세요.
