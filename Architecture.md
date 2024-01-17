## 1. 안드로이드 클린 아키텍처
   ### 1.1 클린 아키텍처 개념
   ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/ba00acfb-b230-4ec7-8723-2096fe92a8ad)
   - 클린 아키텍처는 계층을 크게 나누어서 관심사를 분리하고 각 분리된 모듈 및 클래스가 한가지 역할만 할 수 있도록 구현하는 방식
   - 계층 구조에서 외부에서 내부로 의존성을 가지고 있기 때문에 내부로 갈 수록 의존성은 낮아지게 된다.
   - 외부에 있는 계층이 변화하는 것 때문에 내부의 계층이 변경 되면 안된다.

---

   ### 1.2 클린 아키텍처 구조   
  ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/051383c4-02cd-4d54-b452-b4a74bd0a5d9)
  - ### Domain Layer
       - 클린 아키텍처 핵심 계층 계층
       - 애플리케이션의 비즈니스 로직과 정책을 정의
         > 사용자의 요구 사항이나 정책을 반영한 로직 구현  
         > 독립적인 Use Cases 구현
      - 인터페이스 정의(계층간 의존성 제어)
         > UI 계층과 데이터 계층 사이의 인터페이스를 제공함으로써 각 계층은 서로에게 의존적이지 않고 독립적으로 작동
      - Domain Layer를 모듈화 하여 다른 플랫폼에서도 사용한다고 하면 안드로이드에 대한 종속성은 완전히 배제 하여야 한다.
      - Domain 모듈을 안드로이드 프로젝트에만 사용한다고 하면 안드로이드에 대한 종속을 추가하여 Hilt를 통한 DI 및 안드로이드 기능 사용 가능
      - Repository 인터페이스, UseCase, Model 등이 이곳에 정의 되어야 한다.

        
  - ### Data Layer
       - Database와 API 관련된 것들이 정의되어 있는 Layer
       - Domain 계층에 의존하며 Domain의 Repository 인터페이스를 구현
       - DataSource, DAO, Entity 등이 이곳에 정의 되어야 함
   
  - ### Presentation Layer
       - UI 및 각종 이벤트를 처리하는 레이어
       - viewModel도 이곳에 포함된다.

---

  
### 1.3 클린 아키텍처 예시 
