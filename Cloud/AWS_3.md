## EC2 접속 환경 구성하기

EC2 인스턴스를 생성하고 접속

EC2를 원격접속 하기 위해서는 SSH라는 프로토콜을 사용해서 원격접속을 하게 된다. 이때 key pair 파일 필요.

<br>

### < 인스턴스 생성하기 >

`EC2 접근권한을 가진 IAM 사용자에서 실습`

#### 1. 키 페어 생성

`네트워크 및 보안 > 키 페어 > 키 페어 생성`

- 파일 형식
  - .pem: 리눅스, 맥 OS
  - .ppk: windows OS -> PuTTY를 사용해서 접속해야함.

#### 2. 인스턴스 생성

`대시보드 > 인스턴스 시작`

- 단계 1) AMI 선택
- 단계 2) 인스턴스 유형 선택
- 단계 3) 인스턴스 세부 정보 구성
  - 퍼블릭 IP 자동 할당: 활성화
  - 사용자 데이터: OS가 부팅될 때 최소로 실행할 수 있는 스크립트
- 단계 4) 스토리지 추가
- 단계 5) 태그 추가
  - 인스턴스를 구분하는 용도
- 단계 6) 보안 그룹 구성
  - SSH: 원격 접속을 위한 포트 허용 (22)
  - HTTP: 웹 port (80)
- 단계 7) 인스턴스 시작 검토
- 키 페어 선택
  - 해당 키 페어가 있어야 접속할 수 있도록 체크박스 설정

<br>

### < EC2 원격 접속 >

- 필요한 것: 퍼블릿 IPv4 주소, 키 페어 파일

### 1. Mac, 리눅스 환경에서는 터미널에서 진행

#### 1단계 : key pair 파일이 있는 폴더에서 터미널 실행

#### 2단계 : 키페어 파일 권한 변경 (읽기 전용 파일)

```
chmod 400 elice-keypair01.pem
```

#### 3단계 : ssh 프로토콜로 접속

```
ssh -i elice-keypair01.pem ec2-user@<ip주소>
```

AWS EC2에서 OS를 어떤 것을 사용했는지에 따라 SSH 로그인 계정이 다르다. ex) ubuntu, ec2-user

- 아마존 리눅스 환경 접속 완료

<br>

### 2. Windows에서 EC2 접속

#### 1단계 : [PuTTY 다운로드](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

#### 2단계 : .pem 파일을 .ppk 파일로 변환

- `PuTTY gen` 실행
- `file > private key load > 파일 유형 all로 해서 .pem 선택`
- `Actions > Save private key`로 저장

#### 3단계 : PuTTY를 통해서 원격접속

- `PuTTY` 실행
- `SSH > Auth > private key file 업로드`
- `Section > Host Name for IP address` 에 `ec2-user@<ip주소>`
- `saved-sections에 입력 > save`
- `open > Accept`
- 리눅스 환경으로 접속 완료
