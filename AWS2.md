# 보안 - IAM
### 용어
- AWS 서비스 : AWS에서 제공하는 서비스
- AWS 인스턴스 : AWS 서비스를 이용하여 사용자가 생성한 실제 서비스 객체, 서비스 인스턴스
   - 인스턴스(instance) : 메모리(컴퓨터)에서의 객체
  - 객체(object) : 현실 세계의 모든 것
    - 속성(attribute) : 객체 상태 정보
    - 행위(behavior) : 객체 상태 정보를 이용하거나 변경하는 동작
- AWS 리소스 : AWS 서비스가 사용하는 자원(resource)

### IAM(Identity and Access Management)
- AWS 리소스에 대한 ***엑세스를 안전하게 제어***하기 위한 역할, 권한 설정 서비스
- IAM을 사용하여 AWS 리소스를 사용하도록 인증(로그인) 및 권한 부여 대상 제어
- IAM 글로벌 서비스
- AWS console -> 서비스 -> 보안, 자격 증명 및 규정 준수 -> IAM  
  https://us-east-1.console.aws.amazon.com/iamv2/home?region=ap-northeast-2#/home


### IAM root(관리자) 계정
- 전체 AWS 서비스 및 계정 리소스에 대한 ***완전한 엑세스 권한*** 부여
- email 주소와 암호로 로그인
- MFA 적용을 통한 이중 인증 가능

### IAM user(사용자) 계정
- AWS에서 생성된 엔티티(entity)로 ***AWS와 상호 작용하기 위한 사람 또는 애플리케이션***
- ***최소 권한 원칙 적용*** : 필요한 AWS 리소스에 대한 엑세스 권한 부여
- 각 IAM 사용자별로 자체 자격 증명을 갖고 있다.
  - AWS console 우측 상단 사용자 선택 => 보안 자격 증명 메뉴 선택  
  
  https://us-east-1.console.aws.amazon.com/iam/home?region=ap-northeast-2#/security_credentials
    - CLI/SDK 사용시 별도 엑세스키 필요 
  - IAM 대시보드에서 MFA 추가 항목 선택
    - 가상 MFA 디바이스 사용
  - MFA 적용을 통한 이중 인증
- 기본적으로 주어진 권한 X
- 각 IAM 사용자에게 필요한 권한 부여
- 권한 부여는 정책을 통하여 부여
- 정책은 권한을 설명한 JSON 문서를 의미
  - JSON 문서 포맷(https://www.json.org/json-en.html)
  - 해당 정책에 대한 허용(Allow) / 거부(Deny)에 대한 내용 기술
- 사용자 생성
  - IAM 메뉴 -> 사용자 -> 사용자 추가
    - 사용자 이름
    - AWS 자격 증명 유형 선택
    - 콘솔 비밀번호
    - 비밀번호 재설정    
  
  https://us-east-1.console.aws.amazon.com/iamv2/home?region=ap-northeast-2#/users
  -  -> 권한 부여 
     -  그룹에 사용자 추가
     -  기존 사용자에서 권한 복사
     -  기존 정책 직접 연결
  -  -> 태그부여
     -  Name 키
     -  Value 값 : 임의의 값 부여
  - 태그(tag) : AWS 인스턴스 식별 목적의 값, 항상 부여하는게 차후 AWS 인스턴스 식별시 도움이 된다.

- IAM 그룹
  - IAM 사용자 모임
  - 그룹에 IAM 정책을 할당하면 해당 그룹의 모든 사용자에게 지정된 정책의 권한 부여
- IAM 정책
  - AWS 리소스 및 리소스에 대한 권한을 허용(Allow) / 거부(Deny) 하는 문서
  - IAM 정책을 사용하여 사용자가 리소스에 엑세스
  - Json 형식의 문서로 작성
- IAM 역할
  - IAM 역할은 특정 작업을 허용하거나 거부하는 권한이 연결되어 있으면 임시로 권한에 엑세스 하기 위한 자격을 증명
  - IAM 사용자, 애플리케이션 또는 서비스가 IAM 역할을 가지려면 먼저 역할로 전환할 수 있는 권한 필요
  - IAM 역할을 수행한다는 것은 이전 역할의 모든 권한을 포기하고 새 역할에 지정된 권한 수행

# 네트워크 서비스 - VPC
### 네트워크 구성 요소
- 포트 번호
  - 네트워크 통신을 수행하는 프로세스에 부여된 번호
- IP Address 
  - 네트워크에 연결된 compute(host)에 부여된 번호
  - AWS에서는 IPv4를 기본으로 사용
  - AWS에서는 CIDR 방식으로 host 식별
- 서브넷(subnet)
  - 네트워크에 연결된 호스트를 관리하기 위한 부분 네트워크
- 게이트웨이(gateway)
  - 외부 네트워크(인터넷)과 통신을 수행하기 위한 연결점
  - IPv4에서는 마지막 옥텟의 1번을 게이트웨이로 사용
- 라우터(router)
  - 네트워크에 연결된 host의 경로를 탐색하는 역할수행
  - 라우팅 테이블(routing table)에 연결된 host 경로 정보 관리

### Amazon VPC
- Virtual Private Cloud
- ***AWS 전용 가상 네트워크 서비스***
- 리전 단위 서비스
  - 하나의 리전을 대상으로 VPC생성 
    - AWS는 Default VPC를 미리 생성
  - 동일 리전에 여러 VPC 생성 가능
  - ***여러 리전에 걸쳐 VPC 생성은 불가능***
- VPC 생성
  - VPC 메뉴 -> VPC 생성
    - VPC 설정
      - 생성할 리소스 : VPC만 선택
      - 이름 태그
      - IPv4 CIDR 설정 : 사설 네트워크 IP Address 범위에서 지정
    - VPC 생성 이후 설정 내용
      - 작업 메뉴 => DNS 호스트 이름 편집 => 활성화
      - DNS 확인 => 활성화되어 있어야 함
    - VPC를 생성하면 기본 routing table을 자동 생성
    - VPC 생성은 사설 네트워크 구성을 의미한다

### Subnet
- VPC내에 구성되는 가상 네트워크 서비스
- 가용 영역 단위 서비스 
- 네트워크를 사용하는 개별적인 서비스 제공
- ***AWS 리소스는 항상 subnet에 소속***되어 있어야 함
- 원하는 IP 범위를 갖는 subnet 네트워크 구성, VPC 네트워크 범위 내에서 subnet 구성
- IPv4 CIDR 표기법으로 네트워크 범위 설정, 5개의 IP는 AWS에서 미리 예약
- subnet 유형
  - public subnet
    - 인터넷에 연결되어 외부와 직접 통신이 가능한 subnet
    - 인터넷 게이트웨이(Internet Gateway)를 통하여 인터넷과 연결
    - 양방향 통신
  - private subnet
    - 인터넷에 연결되어 있지 않은 subnet
    - VPC 내부 네트워크에서만 통신 가능, 외부와 불가능
    - NAT Gateway를 사용하면 인터넷을 통한 외부 단방향 통신 가능  
  
![image](https://github.com/pyungpyang/sundries/blob/main/3333.png?raw=true)  

- subnet 생성
  - VPC메뉴 -> 서브넷 메뉴 -> 서브넷 생성
    - VPC 선택
    - 서브넷 설정
      - 서브넷 이름
      - 가용 영역 선택
      - IPv4 CIDR 설정
      - Name 태그 부여  
&nbsp;
- 라우팅 테이블
  - 네트워크 환경에서 호스트를 검색하는 경로 정보를 가지고 있는 네트워크 요소
  - 라우팅 테이블 내용을 이용하여 연결 정보 구성
  - ***VPC 생성시 자동으로 하나의 라우팅 테이블 자동 생성***
  - subnet 수에 따라서 필요한 라우팅 테이블 생성
  - 라우팅 테이블 생성
    - VPC 메뉴 => 라우팅 테이블 => 라우팅 테이블 생성
      - 이름 설정
      - VPC 결정
  - 라우팅 테이블에 명시적 서브넷 연결
    - VPC 메뉴 => 라우팅 테이블 => 원하는 라우팅 테이블 선택 => 작업 메뉴 => 서브넷 연결 편집 => 명시적으로 연결할 서브넷 선택
  - public subnet을 위한 라우팅 테이블에 인터넷 통신을 위한 라우팅 추가
    - public subnet 연결된 라우팅 테이블의 라우팅 편집
      - 라우팅 테이블 선택 => 라우팅 => 라우팅 편집 => 라우팅 추가
        - 라우팅 편집의 대상(통신할 대상) : 0.0.0.0/0
        - 두번째 대상 : 인터넷 게이트웨이  
&nbsp;
- 인터넷 게이트웨이
  - 인터넷과 연결을 수행하는 서비스
  - 인터넷과 양방향 통신 수행
  - 인터넷 게이트웨이는 VPC와 연결되어 있어야 한다.
  - 인터넷 게이트웨이 생성
    - VPC 메뉴 => 인터넷 게이트웨이 => 인터넷 게이트웨이 생성
      - 이름 태그
    - 생성된 인터넷 게이트웨이는 VPC와 연결
      - 작업메뉴 => VPC 연결
        - 사용 가능한 VPC에서 연결할 VPC 선택
          - 상태 : Attached로 변경

# 컴퓨팅 서비스 - EC2(Elastic Compute Cloud)

참고 :  
https://aws.amazon.com/ko/ec2/?nc2=h_ql_prod_fs_ec2  
https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html

### Amazon EC2
- 가상화 기술을 이용하여 AWS에서 관리하는 물리적인 Server에 생성되는 가상 computer 서비스(가상 머신)
- EC2 요금은 사용량에 따라 요금 부과(on-demand)
  - 여러 형태의 할인 요금제 제공 
  - EC2 인스턴스 유형에 따른 사용 시간 + 보조기억장치(EBS) 사용량 + 네트워크 송신량 
&nbsp;
- EC2 인스턴스 생성시 결정할 사항
  - 가상 H/W 구성
    - CPU type
    - Memory 크기
    - 보조 기억 장치 종류/크기/IO 속도
  - 설치할 O/S
  - EC2가 위치할 네트워크
  - 보안 그룹
  - EC2에 접속할 때 사용할 공개키 정보  
&nbsp;
- EC2 인스턴스 생성 : 가상 server 생성
  - EC2 메뉴 선택 => 인스턴스 => 인스턴스 시작
    - 이름 및 태그 설정
    - 애플리케이션 및 OS 이미지
    - 인스턴스 유형
      - CPU
      - Memory
      - 보조 기억 장치
      - 네트워크 대역
    - 키페어(로그인)
      - EC2 인스턴스에 대한 접속(Linux) : SSH 프로토콜을 이용한 접속
    - 네트워크 설정 편집
      - VPC 선택
      - subnet 선택
      - 퍼블릭 IP 자동 할당 => 활성화(인터넷 사용시 필요)
      - 보안 그룹
        - 인스턴스 수준 방화벽
        - Inbound 규칙 : 모든 포트에 대하여 막혀있는 설정
        - Outbound 규칙 : 모든 포트에 대하여 열려있는 설정
  - AMI(Amazon Machine Image)
    - 즉시 사용가능한 OS와 패키지를 가지고 있는 이미지
    - 별도 OS 설치 과정 없이 AMI를 이용하여 EC2를 바로 사용할 수 있도록 해주는 이미지