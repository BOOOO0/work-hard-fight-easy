# WORK HARD FIGHT EASY

- ![image](./img/gon.jpg)

<details><summary>네트워크</summary>

<div markdown="1">

# TCP-IP 4계층

## Application layer

- 응용 계층은 네트워크를 통한 프로세스(호스트)간 통신을 위해 설계된 계층입니다.

- 각 호스트는 메세지를 주고 받기 위해 응용 계층 프로토콜을 사용하며 이 프로토콜들은 전송 계층의 TCP/UDP 프로토콜을 사용합니다.

- 웹에서의 요청, 응답의 경우 클라이언트는 HTTP 요청을 서버에 보내고 서버는 HTTP 응답을 클라이언트로 보내서 사용자에게 전달된 메세지를 볼 수 있도록 합니다.

### HTTP (80)

- HTTP는 hypertext transfer protocol의 약자로 응용 계층의 프로토콜입니다.

- HTTP는 TCP 프로토콜을 사용합니다. 클라이언트는 TCP 연결을 서버에 요청하고 서버가 연결을 수락하면 요청을 보내고 응답을 받습니다. 그 후 TCP 연결을 종료합니다.

- HTTP는 stateless하고 connectionless합니다. 그렇기 때문에 서버는 클라이언트의 이전 요청에 대해 기억하고 있지 않습니다.

- 이 부분을 보완하기 위해 웹에서 Authentication과 같은 기능을 구현할 때 쿠키, 세션 등을 이용해서 사용자를 확인할 수 있습니다.

#### Non-persistent HTTP vs Persistent HTTP

- Non-persistent의 경우 한번에 하나의 요청과 응답 쌍만을 받고 TCP 연결을 종료합니다.

- persistent의 경우 한번의 연결에 여러 쌍의 요청, 응답을 받고 TCP 연결을 종료합니다.

### HTTPS (443)

- HTTPS는 HTTP 프로토콜에 보안 소켓이 추가된 보안 버전입니다. SSL(보안 소켓 계층), TLS(전송 계층 보안)라고 불리기도 합니다.

- 요청과 응답의 내용을 암호화하여 통신을 합니다. 암호화된 내용은 키를 사용해서 복호화하는데 개인 키, 공개 키를 사용해서 개인 키로 암호화된 정보는 공개 키로 공개 키로 암호화된 정보는 개인 키로 복호화할 수 있습니다.

- 개인 키는 웹 사이트의 소유자가 관리하며 공개 키는 클라이언트에게 사용됩니다.

### telnet (23), SSH(22)

- telnet과 SSH는 원격 접속 프로토콜입니다. 차이점은 SSH는 보안성이 더 높아 호스트 사이의 모든 통신이 암호화됩니다.

- SSH는 접속을 위해 SSH 키를 사용하거나 사용자 패스워드를 사용해서 접속합니다.

- 호스트 사이의 통신이 암호화되기 때문에 전달되는 데이터가 유출되지 않습니다.

# OSI 7계층

# IP/CIDR

## IP

- IP는 네트워크 내 서로 연결된 장치들을 식별하기 위한 주소체계입니다.

- 마침표를 구분자로 하는 4개의 숫자로 구성되어 있으며 `255.255.255.255`와 같이 표현합니다.

- 종단 장치와 라우터를 포함해 모든 장치는 고유의 IP를 가지며 이를 통해서 서로 통신합니다.

### IP 버전

- IP는 32비트의 크기를 가지는 IPv4와 128비트의 크기를 가지는 IPv6가 있습니다. 일반적으로 버전을 생략하고 IP라고 한다면 IPv4를 의미합니다.

### IP 클래스

- IP는 많은 수의 주소를 표현할 수 있습니다. 그래서 그것을 관리하기 위해 IP 클래스로 구조화합니다.

- A, B, C, D, E의 5개 클래스가 있으며 주로 A, B, C 3개의 클래스를 사용합니다.

- ![image](./img/ipclass.PNG)

- A 클래스는 8비트의 prefix를 가지고 16,777,214개의 주소를 호스팅 할 수 있으며 B 클래스는 16비트의 prefix를 가지고 65,534개의 주소를 호스팅하고 C 클래스는 24비트의 prefix를 가지고 254개의 주소를 호스팅 할 수 있습니다.

### 네트워크 주소, 호스트 주소

- 그리고 여기서 prefix라 함은 네트워크 주소를 의미합니다.

- `10.0.6.0/24`라면 `10.0.6`까지는 장치들이 모인 네트워크의 주소이고 그다음 `0`부터의 주소가 호스트 주소로 각 장치들을 구분합니다.

### 사설 IP(Private IP)

- 사설 IP는 공개된 IP가 아닌 사설 네트워크에서만 사용 가능한 IP로 `10.x.x.x`, `172.16.x.x`, `192.168.x.x`의 형식을 가지고 클라우드 인프라를 구축할 경우 VPC 환경 내 서브넷 간 서버 간 통신을 할 때 사용되기도 합니다.

## CIDR

- 사이더는 Classless Inter-Domain Routing의 약자로 IP 클래스를 사용하면서 생기는 단점인 IP 주소의 낭비를 방지할 수 있습니다. 여기서 주소의 낭비란 주소가 할당될 디바이스가 300개인 경우 클래스 C 주소를 사용할 수 없기 때문에 클래스 B 주소를 사용합니다. 그렇게 될 때 65,234개의 주소 공간은 사용되지 않은 채로 남는 것을 의미합니다.

- CIDR는 IP 주소 뒤 prefix로 사용될 비트 수를 `/` 다음 표기하는 방식으로 표현됩니다.

- `10.0.6.0/24`와 같이 표기한다면 `10.0.6.0~10.0.6.255` 만큼의 주소 공간을 사용한다는 뜻입니다.

- CIDR는 1부터 32까지 표현할 수 있으며 `10.0.6.40/29`라면 `00001010.00000000.00000110.00101000`에서 29번째 비트까지 같은 주소를 그러니까 마지막 옥텟의 5번째 비트까지 같다면 하나의 네트워크 안의 장치들의 주소로 하는 것입니다.

- 이 네트워크는 `10.0.6.47/29`까지 8개의 주소 공간을 가집니다. 위 주소 `00001010.00000000.00000110.00101111` 다음 주소부터는 마지막 옥텟이 `00110000`으로 표현되기 때문에 포함되지 않습니다.

- 위에서 증명한 바 대로 쉽게 계산한다면 주소 공간의 크기는 `2 ^ (32 - [CIDR 블록 크기])`가 됩니다.

# DNS

# SUBNET

# VPC

# TCP

# UDP

# PROXY

# LOAD BALANCER

# NAT

</div>

</details>
