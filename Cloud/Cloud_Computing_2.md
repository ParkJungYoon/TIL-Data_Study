> **Elice Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.

# Cloud Computing - 기술

### < 가상화 기술 >

- 하이퍼바이저

하이퍼바이저(hypervisor)는 호스트 컴퓨터에서 다수의 운영 체제(operating system)를 동시에 실행하기 위한
논리적 플랫폼(platform)을 말한다. 가상화 머신 모니터 또는 가상화 머신 매니저(virtual machine monitor 또는 virtual machine manager, 줄여서 VMM)

<br>

### < 관리 기술 >

- 리소스 관리

  - CPU/ Storage/ Ram/ Network/ GPU/ 이미지
  - 가상화 된 리소스를 VM 생성시 마다 할당하고 회수하는 역할

- 이미지 관리

  - VM 생성시 OS 이미지를 관리하는 기능

- 네트워크 관리

- 유저 관리

  - 클라우드 내 사용자에 대한 유저 정보 관리

- 데이터 관리
  - 오브젝트/ 블록/ 파일
  - 오브젝트 스토리지: 비정형 데이터

<br>

### < Private Cloud 기반의 클라우드 기능 >

### 1. OpenStack

OpenStack은 풀링된 가상 리소스를 사용하여 프라이빗 및 퍼블릭 클라우드를 구축하고 관리하는 오픈소스 플랫폼입니다.

- Core Project : Nova (compute)
- Core Project : Swift
  - 비정형성 데이터 저장하기 적합
- Core Project : Cinder (block Storage)
- Core Project : Glance
- Core Project : Keystone
- Core Project : Horizon
  - 오픈스택 대시보드 서비스
- Core Project : Neutron

### 2. Docker / Kubernetes

컨테이너 환경

### Docker

- 2013년 3월에 시작된 오픈 소스 프로젝트
- 컨테이너 기반의 오픈 소스 가상화 플랫폼

< 컨테이너 >

Isolated Server
(Same HW, Same Os)

- 장점: 하나의 OS에서 동작 하기 때문에 자원을 효율적으로 사용 가능하다. 빠르다, 가볍다, 이식성이 좋다.
- 단점: 컨테이너는 커널을 HOST OS와 공유해야 하기 때문에 HOST OS에 종속적이다. 자원의 분리가 정확하게 되지 않고 Guest가 나뉘지 않는다.

< VM vs 컨테이너 >

VM

• HOST OS 위에서 Hypervisor를 통해 자원을 가상화 하여 VM을 동작
• HOST OS 위에 Guest OS가 동작하는 구조

Container

• HOST OS에서 프로세스를 위한 공간을 별도로 제공
• 공통 부분만을 패키징 하여 컨테이너로 제공함

<br>

### Kubernetes

“Container Orchestrator”

쿠버네티스는 컨테이너화 된 응용 프로그램의 배포 , 확장 및 관리를 자동화 하는
오픈 소스 시스템입니다.

<br>

### Micro Service / Serverless

- Micro Service

기능 단위로 되어 있어 분산 작업 가능

- Serverless

서비스형 서버리스 : BaaS
다양한 기능들 (데이터베이스, 소셜 서비스, 연동, 파일 관리)을 제공하는 형태

FaaS (Function as a Service)
