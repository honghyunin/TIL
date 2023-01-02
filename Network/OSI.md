# 네트워크 - OSI 7계층

우리가 평소에 사용하는 인터넷은, 이 OSI 7계층, 7개의 단계를 통해 원활하게 사용할 수 있는 것이다.

# Physical Layer

Physical Layer는 컴퓨터와 컴퓨터가 연결되어 있을 때(전선 혹은 와이파이) 교환되는 디지털 신호를 말한다.

컴퓨터가 아예 인터넷에 연결되지 않았을 때(LAN선 연결X, 와이파이 연결X) 인터넷이 작동하지 않는다면 Physical Layer의 문제이다.


# Data-Link Layer

MAC 주소는 모든 컴퓨터에 있는 LAN 카드의 주소를 의미하고, 이 주소를 통해 틎겅 컴퓨터를 찾아갈 수 있다.

이 Layer에서 데이터 전송이 실패한 것은 랜선은 꼽혀있으나 랜카드가 고장났다는 뜻이다

# Network Layer
IP 주소가 결정되는 계층으로, IPv4와 IPv6든 IP가 컴퓨터에 할당되면 전체 지구의 네트워크에서 우리 집의 네트워크 주소가 결정되었다는 것이다.

이 Layer에서 데이터 전송이 실패한 것은, 컴퓨터가 네트워크를 할당받지 못했다는 의미이다.

# Transport Layer
TCP/UDP 가 결정되는 계층이다

이 Layer에서 실패한 것은, TCP handShake가 실패했거나 checksum 검증이 실패했다는 소리입니다. 데이터 전송이 불안정해져, 데이터 오염, 잘못된 값 전송, 값 전송 체크

# Session Layer

포트를 열고 세션을 유지하는 계층입니다.
실제로 현대 인터넷에서 사용하고 있지 않는 계층입니다.

# Presentation Layer

Application Layer를 위해 데이터를 유지하거나 암호화하는 계층
실제 현대 인터넷에서 사용하고 있지 않은 계층

# Application Layer

소프트웨어가 알아들을 수 있는 HTTP, FTTP, WS 등으로 해석해주는 계층
이 Layer에서 데이터 전송이 실패했다는 것은, HTTP나 FTP 등의 프로토콜이 잘못 해석되었다는 뜻이다.
