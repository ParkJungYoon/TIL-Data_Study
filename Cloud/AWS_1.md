> **Elice Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.

# AWS - Intro

### 1. 개념

1. 데이터 센터
2. 가상화 - 논리 서버 (가상머신)
3. 클라우드

< 웹 어플리케이션 기본 구성 >

- 3-Tier Architecture

: Web server (정적 컨텐츠), API server (동적 컨텐츠), Database

- AWS에서 제공하는 서비스로 손쉽게 웹 서버를 만들 수 있다.

<br>

### 2. 글로벌 인프라

1. 리전 (Regions)

물리적인 <u>데이터센터 클러스터 단위</u>

2. 가용 영역 (Availability Zone: AZ)

지리적으로 분리된 1개 이상의 <u>데이터센터</u>

```
AZ를 분리한 이유: 내결함성과 고가용성을 유지하기에 적합한 구조
```

3. 엣지 로케이션 (Edge Location)

전 세계적으로 통신사와 협업하여 빠른 네트워크 서비스를 제공하기 위한 지역

해외 서비스 제공에서 유용하다

<br>

### 3. IAM (Identity & Access Management)

접근 권한을 가진 담당자. 즉, 개인이나 팀을 대상으로 권한을 부여하고 관리할 수 있는 서비스이다.

< **접근 제어 서비스** >

1. Identity: 나는 A이다.

   - **Root 계정** : 사용자 계정 생성, 모든 서비스에 대한 권한을 가지고 있다. MFA로 보안 강화 필요
   - **사용자** : AWS 서비스를 실질적으로 사용하는 유저, 사용자는 필요한 최소한의 권한을 가져야 한다.
   - **사용자 그룹** : 팀 단위로 동일한 접근 권한 정책을 가질 때 사용

2. Permissions (권한 정책)

   - Access Management: A는 무엇을 할 수 있다.
   - Permission JSON Format

- Role: AWS 서비스를 대상으로 적용할 수 있는 Permission이다.

AWS 서비스에만 적용할 수 있다.

< 보안 강화 >

- password 정책
- **MFA**(Multi Factor Authentication) 인증

<br>

### 4. 서비스 사용법

- AWS 엑세스 키 (=ID) & 비밀 엑세스 키 (=Password)
- 외부로 절대 노출하면 안된다!!
