## 1. 안드로이드 클린 아키텍처
   ### 1.1 클린 아키텍처 개념
   ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/ba00acfb-b230-4ec7-8723-2096fe92a8ad)
   - 클린 아키텍처는 계층을 크게 나누어서 관심사를 분리하고 각 분리된 모듈 및 클래스가 한가지 역할만 할 수 있도록 구현하는 방식
   - 계층 구조에서 외부에서 내부로 의존성을 가지고 있기 때문에 내부로 갈 수록 의존성은 낮아지게 된다.
   - 외부에 있는 계층이 변화하는 것 때문에 내부의 계층이 변경 되면 안된다.

---

   ### 1.2 클린 아키텍처 구조   
  ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/d59f42a6-59b0-44aa-9d94-04413520a519)

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
       - 로컬 데이터 베이스, 원격 데이터 소스, 파일 시스템 등 다양한 데이터 소스로부터 데이터를 추출하고 저장하는 과정을 추상화 한다.
       - DataSource, DAO, Entity 등이 이곳에 정의 되어야 함
       - 원격 서버와의 통신을 관리하며, API의 호출을 통해 데이터를 가져오는 곳
            
  - ### Presentation Layer
       - UI 및 각종 이벤트를 처리하는 레이어
       - viewModel도 이곳에 포함된다.
       - Domain Layer나 Data Layer로부터 받은 데이터를 UI 컴포넌트에 바인딩 한다.
       - 사용자 인터페이스의 로딩 상태, 에러 메시지 표시, 데이터 표시 상태 등을 관리한다.
       - 다른 화면으로의 전환을 관리한다.

---

  
### 1.3 클린 아키텍처 예시 
   - ### 모듈 구조
     다음 과 같이 모듈 구조를 만들어 준다.
     기존에 생성된 app 모듈은 제거해도 상관 없고 위의 3가지 모듈 중 하나로 생각하고 Refactor의 Rename을 통해 변경해주어도 무관하다.
     
     ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/1e855a9f-a75f-4de4-8ec8-1fbbf092d92c)

   - ### Domain Layer
     Domain Layer에서는 실제로 UI 작업에 사용할 모델이 필요하며, 해당 모델을 통해 원하는 데이터를 가져오기 위한 Repository의 interface와 Usecase 등을 선언한다.

     ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/81810dd8-7d17-47f1-87a5-bbd8371562fa)

     Usecase는 해당 VM에서 어떤 것을 실행 하고자 하는지 직관적으로 파악 할 수 있으며 의존성을 줄일 수 있다는 장점을 가지고 있다.

     ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/d1b8cbc4-c3ea-439c-80ba-aed2cf3dbc74)

   - ### Data Layer
     Data Layer는 로컬 DB 데이터와 서버 API 데이터를 모두 가져와서 사용하기 때문에 해당 패키지를 만들어 구분지어 준다.

     ![image](https://github.com/kstappmanager/ksmartech/assets/152848192/45ee36da-801c-41f3-b596-6e182d47e638)

   - ### Presentation Layer

