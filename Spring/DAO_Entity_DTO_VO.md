# DAO
> Data Access Object : Repository Package

``DAO`` 는 프로젝트의 서비스 모델과 실제 데이터베이스를 연결하는 역할을 하며, JPA에서는 DB에 데이터를 CRUD하는 ``Repository`` 객체들이 DAO라고 볼 수 있습니다.

- SQL을 사용(개발자가 직접 코딩)하여 DB에 접근한 후 적절한 CRUD API를 제공합니다.
    - JPA 대부분의 기본적인 CRUD method를 제공하고 있습니다.
# 1. Entity 란?

- Entity 클래스는 **실제 Database의 테이블과 1:1 로 매핑되는 클래스**로, **DB의 테이블내에 존재하는 컬럼만을 속성(필드)으로** 가져야 합니다.
- Entity 클래스는 상속을 받거나 구현체여서는 안되며, 테이블내에 존재하지 않는 컬럼을 가져서도 안됩니다.

Entity 클래스 또는 가장 Core한 클래스라고 부릅니다.

# 1.1 Entity, DTO Class 분리 이유

**Entity와 DTO를 분리해서 관리해야 하는 이유**는 **DB Layer와 View Layer 사이의 역할을 분리 하기 위해서**입니다. 

**Entity 클래스**는 **실제 테이블과 매핑**되어 변경되게 되면  

여러 다른 클래스에 영향을 끼치고, **DTO 클래스는 View와 통신하며 자주 변경되므로 분리** 해주어야 합니다.

결국 DTO는 Domain Model 객체를 그대로 두고, 복사하여 다양한 Presentation Logic을 추가한 정도로 사용하여 **Domain Model 객체는 Persistent만을 위해서 사용**해야 한다.

# 1.2 Entity Setter 금지 및 생성자, 접근 제어

엔티티를 작성할 때 Setter를 무분별하게 사용하면 객체(Entity)의 값을 변경할 수 있으므로 객체의 일관성을 보장할 수 없다. 객체의 일관성을 유지할 수 있어야 유지 보수성이 올라가기 때문에 Setter를 사용해서는 안되며, 객체의 생성자에 값들을 넣어줌으로써 Setter 사용을 줄일 수 있습니다.

- ``@Entity``

    테이블과 링크될 클래스임을 나타낸다.

    **기본값**으로 **카멜케이스 이름을 언더 스커어 네이밍(_)으로** 테이블 이름을 매핑합니다.

    - ``@GeneratedValue``

    PK 생성 규칙

    스프링 부트 2.0에서는 GenerationType.IDENTITY 옵션을 추가해야만 auto_increment가 됩니다.

    - ``@Id``

    **해당 테이블의 PK 필드**를 나타냅니다.

    - ``@Column``

    테이블의 컬럼을 나타내며 굳이 **선언하지 않더라도 해당 클래스의 필드는 모두 컬럼**이 됩니다.

    사용 이유 : **기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용**합니다.

    - ``@Builder``

    해당 클래스의 빌더 패턴 클래스를 생성해 줍니다.

    생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함해 줍니다.

    # 2. DTO(Data Transfer Object)

    - DTO(Data Transfer Object)는 데이터 전송(이동) 객체라는 의미를 가지고 있습니다.
    - DTO는 주로 비동기 처리를 할 때 사용합니다.
    - **계층간 데이터 교환을 위한 객체(Java Beans)** 입니다.
    - **DB의 데이터를 Service나 Controller 등으로 보낼 때 사용하는 객체**를 말합니다.

    **DB의 데이터가 Presentation Logic Tier로 넘어올 때는 DTO로 변환되어 오고가는 것**입니다.

    - 로직을 갖고 있지 않은 수수한 데이터 객체이며, getter/setter 메서드만을 갖는다.
    - **Controller Layer에서 Response DTO 형태로 Client에 전달**합니다.

    # 3. VO(Value Object)

    - VO는 말 그대로 **값 객체라는 의미**를 가지고 있습니다.
    - **VO의 핵심 역할은 equals()와 hashcode()를 오버라이딩 하는 것** 입니다.
    - VO 내부에 선언된 **속성(필드)의 모든 값들이 VO 객체마다 값이 같아야, 똑같은 객체라고 판별**합니다.

    VO는 Getter와 Setter를 가질 수 있으며, VO는 테이블 내에 있는 속성 외에 추가적인 속성을 가질 수 있으며, 여러 테이블(A, B, C)에 대한 공통 속성을 모아서 만든 BaseVO 클래스를 상속받아서 사용할 수도 있습니다

    # 🙆‍♂️ 참고 🙇‍♂️

    [GiLog](https://velog.io/@gillog/Entity-DTO-VO-%EB%B0%94%EB%A1%9C-%EC%95%8C%EA%B8%B0)