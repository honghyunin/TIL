
# VPC(Virtual Private Cloud)

**VPC** : 사용자가 정의하는 IP 주소 범위 선택, 서브넷 생성, 라우팅 테이블 및 네트워크 게이트웨이 구성 등 가상 네트워크 환경을 VPC라고 한다.

Amazon VPC는 인터넷에 액세스할 수 있는 웹 서버를 위한 퍼블릭 서브넷, 인터넷 액세스가 없는 프라이빗 서브넷에 DB나 애플리케이션 서버 같은 백엔드 시스템을 배치하고, 보안 그룹 및 네트워크 액세스 제어 목록을 포함한 다중 보안 계층을 사용하여 각 서브넷에서 Amazon EC2 인스턴스의 액세스를 제어할 수 있다.

![no vpc.png](..%2F..%2Fimages%2Fno%20vpc.png)

VPC가 없다면 EC2 인스턴스들이 서로 거미줄처럼 연결되고 인터넷과 연결된다. 이런 구조는 시스템의 복잡도를 엄청나게 끌어올릴 뿐만 아니라 하나의 인스턴스만 추가되도 모든 인스턴스를 수정해야하는 불편함이 생긴다. 마치 인터넷 전용선을 다시 까는 것과 같다.

그러나 VPC를 이용하면 이를 통해 리소스를 쉽게 관리할 수 있다.

![vpc.png](..%2F..%2Fimages%2Fvpc.png)

VPC를 적용하면 위 그림과 같이 VPC 별로 네트워크를 구성할 수 있고 각각의 VPC에 따라 다르게 네트워크 설정을 줄 수 있다. 또한 각각의 VPC는 완전히 독립된 네트워크처럼 작동하게 된다.

## VPC 를 구축하는 과정

![private ip.png](..%2F..%2Fimages%2Fprivate%20ip.png)

VPC를 구축하기 위해 VPC의 아이피범위를 RFC1918 라는 사설 아이피대역에 맞추어 구축해야 한다. 

사설 아이피는 인터넷을 위해 사용하는 것이 아닌 우리끼리 사용하는 아이피주소 대역이다.

예를 들어 누군가 "안방에서 리모컨좀 가져다달라" 하면 나는 옆집을 가는 게 아닌 우리집에 있는 "안방"으로 찾아간다. 안방이 프라이빗아이피(사설아이피)우리집 주소가 퍼블릭 아이피이다.

옆집도 안방이 있고 우리집도 안방이 있지만 서로 안방을 들었을 때 헷갈리지 않는다. "안방", "작은방", "큰방" 처럼 내부에서 쓰는 주소를 사설 아이피 대역이라고 부르며 내부 네트워크 내에서 위치를 찾아갈 때 사용한다. 물론 내 친구나 혹은 동생의 친구가 찾아올 때는 도로명주소(퍼블릭아이피)를 알려주면 되고 같은 집(우리집)에 사는(동일한 네트워크 상에 존재하는) 내가 동상한테 갈 때는 동생방(사설아이피)로 찾아간다.

VPC에서 사용하는 사설 아이피 대역은 아래와 같다.

- 10.0.0.0 ~ 10.255.255.255(10/8 prefix)
- 172.16.0.0 ~ 172.31.255.255(182.16/12 prefix)
- 192.168.0.0 ~ 192.168.255.255(192.168/16 prefix)

한번 설정된 아이피대역은 수정할 수 없으며 각 VPC는 하나의 리전에 종속된다. 각각의 VPC는 완전히 독립적이기 때문에 만약 VPC간 통신을 원한다면 VPC 피어링 서비스를 고려해볼 수 있다.

## 서브넷

![subnet.png](..%2F..%2Fimages%2Fsubnet.png)

VPC를 만들었다면 이제 서브넷을 만들 수 있다. 서브넷은 VPC를 잘개 쪼개는 과정이다. 서브넷은 VPC안에 있는 VPC보다 더 작은 단위이기 때문에 연히 서브넷 마스크가 더 높게 되고 아이피범위가 더 작은 값을 갖게 된다. **서브넷을 나누는 이유는 더 많은 네트워크망을 만들기 위해서이다.**

각각의 서브넷은 가용영역안에 존재하며 서브넷안에 RDS, EC2와 같은 리소스들을 위치시킬 수 있다.

## 라우팅 테이블과 라우터

![router.png](..%2F..%2Fimages%2Frouter.png)

네트워크 요청이 발생하면 데이터는 우선 라우터로 향하게 된다. 라우터란 목적지이고 라우팅테이블은 각 목적지에 대한 이정표이다. 데이터는 라우터로 향하며 네트워크 요청은 각각 정의된 라우팅 테이블에 따라 작동한다. 서브넷 A의 라우팅테이블은 172.31.0.0/16 즉 VPC안의 네트워크 범위를 갖는 네트워크 요청은 로컬에서 찾게 되어있다.

## 인터넷 게이트웨이

![router.png](..%2F..%2Fimages%2Frouter.png)

인터넷게이트웨이는 VPC와 인터넷을 연결해주는 하나의 관문이다. 서브넷B의 라우팅 테이블을 잘보면 0.0.0.0/0 으로 정의되어 있다. 이뜻은 모든 트래픽에 대해 IGA(인터넷 게이트웨이) A로 향하라는 뜻이다. 라우팅 테이블은 가장 먼저 목적지의 주소가 172.31.0.0/16에 매칭되는 지를 확인한 후 매칭되지 않는 IGA A로 보낸다.

인터넷과 연결되어 있는 서브넷을 퍼블릭 서브넷, 인터넷과 연결 되어 있지 않은 서브넷을 프라이빗 서브넷이라고 한다.

네트워크 ACL과 보안그룹

![securitygroup.png](..%2F..%2Fimages%2Fsecuritygroup.png)

네트워크 ACL과 보안그룹은 방화벽과 같은 역할을 하며 인바운드 트래픽과 아웃바운드 트래픽 보안 정책을 설정할 수 있다.
먼저 보안 그룹은 Stateful한 방식으로 동작하는 보안그룹은 모든 허용을 차단하도록 기본설정 되어 있으며 필요한 설정은 허용해주어야 한다. 또한 네트워크 ACL과 다르게 각각의 보안 그룹별로도 별도의 트래픽을 설정할 수 있으며 서브넷에도 설정할 수 있지만 각각의 EC2 인스턴스에도 적용할 수 있다.

네트워크 ACL은 Stateless하게 작동하며 모든 트래픽을 기본설정되어 있기 때문에 불필요한 트래픽을 막도록 적용해야 한다.

서브넷 단위로 적용되며 리소스별로 설정할 수 없다. 네트워크 ACL과 보안그룹이 충돌한다면 보안그룹이 더 높은 우선순위를 갖는다.

## NAT 게이트웨이

![natgateway.png](..%2F..%2Fimages%2Fnatgateway.png)

NAT 게이트웨이는 프라이빗 서브넷이 인터넷과 통신하기 위한 아웃바운드 인스턴스이다. 프라이빗 네트워크가 외부에서 요청되는 인바운드는 필요없더라도 인스턴스의 펌웨어나 혹은 주기적인 업데이트가 필요하여 아웃바운드 트래픽만 허용되어야 할 경우가 있다. 이때 퍼블릭 서브넷상에서 동작하는 NAT 게이트웨이는 프라이빗 서브넷에서 외부로 요청하는 아웃바운드 트래픽을 받아 인터넷 게이트웨이와 연결한다.

# VPN(Virtual Private Network)

VPN은 가상사설망.

실제 사설망이 아닌 가상의 사설망이다.

![vpn1.png](..%2F..%2Fimages%2Fvpn1.png)

만약 위 그림과 같이 회사의 네트워크가 구성되어 있고 보안상의 이유로 직원간 네트워크를 분리하고 싶다면 기존 인터넷 선공사도 다시해야하고 건물의 내부선을 전부 뜯어고쳐야 하며 다시 전용선을 깔아주어야 한다. 이를 위해 가상의 망 VPN 을 사용하게 된다.

![vpn2.png](..%2F..%2Fimages%2Fvpn2.png)

VPN은 네트워크A와 네트워크B가 실제로 같은 네트워크상에 있지만 논리적으로 다른 네트워크인 것처럼 동작한다. 이를 우리는 '가상사설망' 이라고 한다.
