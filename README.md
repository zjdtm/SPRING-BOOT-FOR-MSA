1. 마이크로서비스 아키텍처
모든 시스템은 하나 이상의 컴포넌트로 구성되어 있다. 즉, API 컴포넌트나 저장소 컴포넌트처럼 각자 역할이 분리되어 있다.
시스템 컴포넌트를 나누고 합치는 디자인을 하는 사람은 아키텍트, 컴포넌트와 컴포넌트의 관계를 정리한 것을 소프트웨어 아키텍처라고 한다.
여기서 서비스 기능을 하나의 API 컴포넌트에서 처리하는 구조를 모놀리식 시스템 아키텍처, 기능을 분리하여 두 개 이상의 API 컴포넌트에서 처리하는
구조를 분산 처리 시스템 아키텍처라고 한다.

모놀리식 아키텍처란?
하나의 시스템이 서비스 전체 기능을 처리하도록 설계한 것으로, 즉 하나의 WAS에서 모든 기능을 처리하도록 구성한다.

모놀리식 아키텍처의 장점은 이러한 간단한 구조 덕분에 시스템 운영과 개발이 편리한 장점이 있고, 네트워크로 인한 지연이나 데이터 유실 등을 걱정할 필요가 없으며 버그나 장애가 생긴다면 하나의 애플리케이션에서 원인을 파악하면 되기 때문에 쉽게 파악할 수 있다.

하지만 하나의 애플리케이션 서버에서 여러 기능을 제공하기 때문에 서비스 기능이 많아지면 더 복잡해질수 있어 개발 속도나 생산성이 낮아질 수 있다는 단점이 있다. 
- 클라이언트 요청이 점점 많아지는데 로드 밸런서로 확장해도 한계가 있을 때
- 데이터베이스 성능을 높여도 더 이상 성능 개선의 여지가 없을 때
- 기능 확장 요구가 많지만 현재 시스템 구조로 불가능 할 때
- 소스 코드가 너무 복잡해서 리펙터링이 필요할 때
- 기능 중 하나라도 변경되면 전체 QA를 해야 할 때
- 기능을 수정하면 다른 기능에 연쇄적으로 버그가 발생할 때
- 개발자는 늘었는데, 개발 속도는 이전 같지 않을 때

위와 같은 상황에 처하면 마이크로서비스 아키텍처로 전환을 고려해 볼수 있다고 한다.

마이크로 서비스 아키텍처란?
기능 위주로 나뉜 여러 애플리케이션이 있고, 각각 독립된 데이터 저장소를 사용한다. 기능으로 분리된 애플리케이션들은 미리 정의된 인터페이스를 통해 서로 유기적으로 동작한다. 이렇게 기능별로 쪼개긴 작은 서비스 혹은 시스템을 마이크로서비스라고 한다. 마이크로서비스들이 서로 의존하면 복잡도는 더욱 증가하고, 하나에 장애가 발생하면 연쇄적으로 장애가 발생하기 때문에 서로의 의존성을 최소화 해야 한다. 즉, 느스하게 결합되어 있어야 한다. 
마이크로서비스 아키텍처의 특징은 대규모 시스템, 분산 처리 시스템, 컴포넌트들의 집합 그리고 시스템 확장 등이 있다.

마이크로 서비스의 장점은 첫번째 독립성이다. 하나의 마이크로서비스는 독립된 데이터 저장소를 갖고 있으므로 데이터 간섭에 자유롭다.
두번째는 대용량 데이터를 저장하고 처리하는데 비교적 자유롭다. 샤딩을 통해 데이터를 분산해서 저장한다 [샤딩 링크]
세번째는 시스템 장애가 견고하다. 마이크로서비스는 서로 느슨하게 연결되어 있고, 독립되어 있기 때문에 서로 간에 미치는 영향이 적다.
네번째는 서비스 배포 주기가 빠르다. 모놀리식 아키텍처는 모든 기능이 하나의 코드베이스에서 개발되기 때문에 배포 일정으로 정하고 한 번에 모든 기능을 배포한다. 하지만 마이크로서비스 환경에서는 필요한 기능만 먼저 배포할 수 있다.
다섯번째는 마이크로서비스 단위로 확장할 수 있어 서비스 전체적으로 확장성이 좋아진다.
여섯번째는 사용자의 반응에 민첩하게 대응할 수 있다. 

이렇게만 보면 모놀리식 아키텍처보다는 마이크로서비스 아키텍처를 쓰는게 더 좋은거 같지만 아쉽게도 단점이 있다.
첫번째는 개발하기 어려운 아키텍처이다. 데이터가 분산되어 있기 때문에 DB 트랜잭션을 사용할 수가 없다. 분산 트랜잭션을 사용할 수는 있지만
시스템의 리소스를 많이 사용하므로 권장하지는 않는다고 한다.
두번째는 운영하기가 어렵다. 
세번째는 설계하기 어려운 아키텍처이다.
네번째는 마이크로서비스 아키텍처로 설계된 서비스 운영에는 여러 가지 자동화된 시스템이 필요하다. 
마지막으로 개발자의 기술력이 좋아야 한다.

마이크로서비스 아키텍처 설계
마이크로서비스를 설계하는 과정에서 다음 어려움을 겪는다.
1. 전체 서비스 관점에서 보았을 때, 어느 정도 크기로 마이크로서비스를 분리해야 할까?
2. 너무 작게 분리하는 것은 아닐까? 혹은 너무 크게 분리하는 것은 아닐까?
3. 분리된 마이크로서비스 사이의 표문 인터페이스 통신은 어떻게 할까?
4. 새로운 서비스가 추가되면 어떤 마이크로서비스가 처리하면 좋을까?

이러한 아키텍처 설계의 원칙과 체계를 정해서 기준을 잡을 수 있는데 이 원칙들을 분류하자면,
- 서비스 세분화 원칙 : 비즈니스 기능, 성능, 메시지 크기, 트랜잭션 총 네 개의 구성 요소를 기반으로 서비스를 나누도록 제안하는 원칙
- 도메인 주도 설계와 바운디드 컨텍스트 : 다시 공부
- 단일 책임 원칙 : 모든 클래스는 하나의 책임을 가지며, 그 클래스의 기능은 이 책임을 기반으로 개발되어야 한다.
- 가벼운 통신 프로토콜 : 마이크로서비스 사이에 네트워크 통신은 가벼워야 하며, 프로토콜은 특정 기술이나 언어에 의존성이 없어야 한다.
- 외부 공개 인터페이스 : 마이크로서비스들은 네트워크를 이용하여 서로 통신하는데, 이때 시스템 운영 중에는 즉각적인 수정이나 변경이 힘들기 때문에 
외부에공개하는 인터페이스를 설계할 때는 신중해야 한다.
- 마이크로서비스마다 독립된 데이터 저장소 : 서비스 복잡성을 낮추기 위해 마이크로서비스로 분리했는데, 저장소를 같이 사용하면 독립성이 위배되면서 복잡해진다.

2. 프레임워크와 스프링 부트
스프링프레임워크의 특징
- POJO 기반의 경량 컨테이너 제공 : POJO 객체는 특정 기술에 종속되지 않는 순수한 자바 객체를 의미하며 모든 스프링 애플리케이션은 POJO 객체와 스프링 컨테이너를 포함한다. 스프링 컨테이너는 이 POJO 객체들의 생명주기를 관리한다. 이를 통해 개발자가 개발하는 클래스는 프레임워크의 코드와 분리되어 있고 비즈니스 로직을 구현하는 데 집중되어 있어 복잡도가 낮아진다.
- 복잡한 비즈니스 영역의 문제를 쉽게 개발하고 운영하기 위한 철학 : 스프링 프레임워크의 핵심 요소는 의존성 주입, 관점 지향 프로그래밍, 서비스 추상화다. 이를 통해 개발자는 도메인 영역의 문제에 집중할 수 있도록 환경을 만들어 준다.
- 여러 개의 개별 단위로 구성되어 있는 모듈식 프레임워크 : 스프링 프레임워크는 엔터프라이즈 애플리케이션을 개발할 수 있는 여러 기능을 포함하고 있다. 기능들은 성격에 따라 분류하여 모듈이라는 단위로 관리한다. 개발자는 필요한 모듈들을 레고 블록처럼 조합하여 필요한 기능만 사용할 수 있다.
- 높은 확장성 및 범용성, 광범위한 생태계 시스템 : 스프링 프레임워크는 여러 형태로 확장할 수 있는 범용적인 애플리케이션을 만들 수 있고, 여러 가지 기술과 연동 및 확장할 수 있는 다양한 형태의 프로젝트를 제공한다. 배치 프로세스를 위한 배치 프레임워크를 제공하거나, 인증가 인가를 쉽게 구현할 수 있는 스프링 시큐리티 프레임워크 등이 있다.
- 엔터프라이즈 애플리케이션에 적합한 경량급 오픈 소스 프레임워크 : 스프링 프레임워크는 외형적으로는 모듈 방식과 높은 확장성 덕분에 여러 형태의 애플리케이션을 개발할 수 있어 엔터프라이즈 애플리케이션의 요구 사항에 적합하다.

스프링 부트의 특징
모든 스프링 프로젝트는 스프링 프레임워크를 반드시 포함한다. 스프링 부트는 스프링 프로젝트와 목적이 다른데, 가능한 빠르게 애플리케이션을 개발하고 서비스하는 것을 우선시하는데, 그 특징으로는 설정 없이 바로 애플리케이션을 개발할 수 있다는 것이다. 이러한 특징 덕분에 설정하는 데 많은 시간을 쓸 필요가 없다.








