> **Elice Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.

# AWS - Storage, DB CDN 서비스

< 스토리지 종류 비교 >

1. S3 (Simple Storage Service) : 오브젝트 스토리지
   - REST
   - 용량 무한
   - 분산저장
2. EBS (Elastic Block Store) : 블록 스토리지
3. EFS (Elastic File system) : 파일 스토리지

## 1. AWS RDS

AWS에서 RDBMS 구성하는 방식

1. EC2 인스턴스에서 설치형으로 구성
2. AWS 완전 관리형 DB 서비스 : **RDS**

- 특징
  - 자유롭게 확장 및 축소 가능
  - 여러 AZ(Available Zone)에 거친 고가용성 구성
  - 백업 기능으로 안전하게 데이터 보호
  - 읽기 전용 복제본 **(Read Replica)** 기능 -> 읽기 성능 확장

### Read Replica

원본 데이터 : Master
읽기 전용 복제 데이터 : Slave

### Auto Scaling

- 조건
  - 사용 가능한 여유 공간이 할당된 스토리지의 10% 미만일 때
  - 용량이 부족한 스토리지 상태가 5분 이상 지속될 때
  - 마지막 스토리지 수정 이후 최소 6시간이 경과했을 때

### AWS Aurora

AWS에서 클라우드 환경에서
적합하도록 커스터마이징 된 관리형 데이터베이스 서비스

<br>

## 2. AWS S3

Simple Storage Service

데이터를 저장, 수집, 분석을 하기위한 대표적인 **오브젝트 스토리지**

- 객체는 버킷(Bucket) 이라는 리소스에 저장

### S3 Object 와 bucket

- `S3 Object` : 데이터를 담기 위한 단위
  - 각각의 Object 는 Key 를 가짐 (`Key-Value 구조`)
- `S3 Bucket` : Bucket 은 Object 를 담기 위한 데이터 보관 단위
  - Bucket은 Region 단위로 배포 가능
