# Cloud 개요
### ***On-Premise*** 환경
- IT 서비스 운영을 위하여 직접적인 인프라를 구축하는 방식
- 이전 또는 현재 주로 사용하는 환경
- Client-Server 구조
  - Client : service 요청
  - Server : service 제공
  
  - Client-Server 구조에서 동작하는 프로그램 유형
    - Front-end 
      - end user가 사용
      - client에서 동작하는 프로그램
    - Back-end
      - server program
      - client 에게 service를 제공하는 프로그램

### ex. Web Service 제공 On-Premise 환경 구축
- Back-end 구성
    - Web Server 프로그램 설치 : Apache, NginX, Node.js, Django ... 
- Front-end 구성 
  - Web Browser 설치

# On-premise 환경에서의 Server 구성
- H/W 구성
  - 처리속도
  - 최대 용량에 맞춰 구축
  - CPU : 처리 능력
  - Memory : 기억 능력
  - I/O Device : 입/출력 능력(속도)
- S/W 구성
  - O/S (운영체제) : H/W 제어
    - Linux
      - RedHat 계열 배포판
      - Debian 계열 배포판
    - MS Windows Server
    - MacOS
  - Service 구성을 위한 S/W
    - Server 구성 프로그램
      - ex : Web Server, DB Engine, Main Server
    - Server 구성 Framework : Server 프로그램이 동작할 수 있는 환경
      - Library : 함수(function) 집합
      - Framework : 프로그램 Library와 프로그램 구조(Template)를 포함하고 있는 Library
      - Node.js, JSP, ASP, Django, Flask
    - Application 개발 환경 구축

### On-premise 환경 단점
- 구축에 대한 초기 비용이 많이 발생
- 확장성이 떨어짐
- 관리에 대한 어려움

### Cloud 환경
- cloud service 제공 업체의 H/W, S/W 환경을 빌려서 사용 : 초기 비용 x
- 사용한 만큼 비용 지불
- service 형태로 제공하므로 자유롭게 확장 및 축소 가능
- Network 사용이 기본
- web 기반 이용 : client 프로그램으로 web browser 사용

# AWS 개요
### AWS(Amazon Web Service)
- Amazon 내부 운영 시스템을 발전시켜 외부 서비스 형태로 제공하는 ***public cloud service***
- AWS 장점
  - 자본 비용을 가변 비용으로 대체 - 사용한 만큼 비용 지불
  - 규모의 경제에 따른 혜택
  - 필요 용량에 대한 별도 추정 불필요
  - 속도 및 민첩성 개선
  - 별도의 데이터 센터 운영에 따른 비용 x
  - 전 세계 배포에 대한 편의성 제공

### cloud service 유형
- cloud service를 사용하는 대상/목적
- Iaas(Infrastructure as a Service)
  - server 환경(Infrastructure)만 빌려서 사용
  - Cloud Service 업체에서 제공하는 Infrastructure와 Platform 활용
    - H/W 환경
    - O/S 환경
    - Network 환경  
  &nbsp;  
- Paas(Platform as a Service)
  - Platform을 빌려서 사용
    - Application을 개발하고 동작할 수 있는 환경
  - H/W 환경
  - O/S 환경
  - Network 환경
  - Service 제공을 위한 환경 : Library, Framework 등  
  &nbsp;
- SaaS(Service as a Service)
  - 사용자가 원하는 service 관련 application을 빌려서 사용
  - Cloud Service 업체에서 제공하는 Infrastructure와 Platform, Service 활용
    - H/W 환경
    - O/S 환경
    - Network 환경
    - Service 제공을 위한 환경 : Library, Framework 등
    - Service 제공을 위한 Application

### cloud 책임 모델
- 공동 책임 모델 적용
  - cloud 서비스 제공 업체와 cloud 서비스 사용자 각각의 책임 영역을 구분하여 책임을 나누어 관리하는 모델
- cloud 배포 형태
  - public cloud
    - 공개된 형태의 cloud
    - 일반적인 cloud 형태
  - private cloud 
    - on-premise 환경을 cloud 형태로 제공
  - hybrd cloud
    - public + private

### 가상화(Virtualization)
- S/W적으로 Computer System을 구성
- 가상화 종류

![image](https://github.com/pyungpyang/sundries/blob/main/hypervisor.png?raw=true)  
  - bare metal 형식 가상화
    - 기존 O/S(Host O/S)와 별개로 가상화 S/W를 이용하여 가상 H/W를 구성, 제공하는 가상화 방법
    - 가상화 S/W
      - VMWare
      - VirtualBox
      - Hypervisor를 지원하는 CPU 환경에서만 가능
      - Host O/S와 Guest O/S를 별도로 설치하여 사용, 자원 관리 측면에서 많은 자원 소모 발생
      - 가상 머신의 크기가 S/W적으로 하나의 컴퓨터에 대한 자원들을 관리하므로 용량이 큰 편
  - O/S 가상화
    - 기존 O/S(Host O/S) kernel 을 수정하여 가상화 기능 제공(KVM)
    - 가상의 H/W 생성없이 물리적인 H/W를 가상화 기술을 이용하여 공유
    - 자원 관리 측면에서 bare metal보다 효과적이고 크기도 작음
    - ***public cloud 제공 업체에서 주로 활용***
    - public cloud의 모든 서비스는 가상 환경을 이용하여 제공
  - Applicaion 가상화
    - Application 실행 환경을 가상화하여 배포 및 운영에 편의성 제공
      - docker

### AWS Login
- 루트 사용자
  - ID : email 사용
  - AWS 계정 생성시 사용한 email주소
  - 하나의 ID만 부여되고 모든 AWS service 를 사용할 수 있는 사용자
  - 과금 대상자
- IAM 사용자
  - ID : 숫자 12자리
  - 사용자 별명
  - 일반 사용자가 주로 사용
  - ***역할에 따른 제한된 service만 사용***할 수 있음.
  - 루트 사용자나 일반 사용자에 의해서 생성
- AWS 서비스 이용 방법
  - AWS Console 이용
    - 일반적인 AWS service 이용 방법 : GUI방식
    - dashboard를 통해 개별 서비스 현황 파악 가능
    - 시스템 운영자, application 개발자
  - AWS CLI 이용
    - 명령 프롬프트(터미널)에서 명령어 기반으로 AWS 서비스 관리 
    - 명령을 통해 세세한 관리 수행
    - ***별도의 설치 프로그램으로 AWS CLI설치 후 사용***
    - CLI 사용을 위한 프로그램
      - Windows 
        - AWS 가상 컴퓨팅 사용시 : ssh client 프로그램(putty, xshell등), 명령 프롬프트
        - Windows에 직접 CLI 설치시 : 프롬프트, windows terminal, power shell 사용
      - Linux/MacOS : 터미널 프로그램 
    - 시스템 운영자(관리자), application 개발자
  - AWS SDK(Software Development Kit, SW 개발 환경) 이용
    - application program에서 API, 함수(function)를 이용하여 AWS 서비스 사용
    - 별도 설치 필요
    - ***application 개발자***
  - IaC(Infrastructure as a Code) 이용
    - IaC : Infra 구축을 코드를 이용하여 관리하는 방법
    - AWS 서비스 생성 및 운영에 대한 내용을 Code 형식을 사용하여 일괄적으로 관리
    - 복잡한 Infra를 일관성을 유지하면서 관리하기 위한 목적
    - IaC Utility
      - AWS CloudFormation
      - Ansible
      - Terraform
    - 시스템 운영자(관리자)
### 글로벌 인프라
- 참고 : https://aws.amazon.com/ko/about-aws/global-infrastructure/?nc2=h_ql_le_int_gi
- AWS 글로벌 인프라 특징
  - 보안
  - 가용성
  - 성능
  - 국제적 입지
  - 확장성
  - 유연성

- 리전(Region)
  - AWS 서비스를 제공하는 물리적인 위치(장소)
  - ***리전별로 제공되는 서비스 및 비용 차이 발생***
  - 리전 선택시 고려사항
    - 규정 준수
    - 근접성 속도
      - https://cloudping.info/
    - 기능 가용성
      - AWS 서비스는 리전별로 다르다.
    - 요금
  - ***AWS 서비스를 사용하기 전에 사용할 리전을 결정해야 한다.***

- 가용 영역(Availability Zone, AZ)
  - 리전 내 격리된 공간
  - 실제 데이터 센터 의미
  - 각 리전은 2 ~ 4 개의 가용 영역 운영
  - AWS 서비스는 리전의 가용 영역을 지정하여 제공하는 경우가 많음
- AWS 서비스 사용시 고려사항
  - 리전 선택
  - 가용 영역 선택

### AWS 서비스 유형 - IaaS
- Computing SErvice (가상 computer, Server)
  - ***Amazon EC2(Elastic Compute Cloud) 서비스***
- Network Service (가상 Network)
  - ***Amazon VPC (Virtual Private Cloud) 서비스***
- Storage Service (보조 기억 장치, 데이터/객체 저장)
  - ***Amazon EBS(Elastic Block Storage) 서비스***
  - Amazon EFS(Elastic File Storage) 서비스
  - ***Amazon S3(Simple Storage Service)***
- Relational DataBas Service
  - ***Amazon RDS(Relational Datebase Service)***
- 사용자 관리 Service
  - ***IAM (Identity and Access Management Service)***