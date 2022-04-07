> **Elice Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.

- [출처](https://pearlluck.tistory.com/119?category=854934)

# Docker - Intro

### 1. Docker란

'컨테이너' 기반의 오픈소스 가상화 플랫폼 (Paas)

### 2. Container란?

- 다양한 프로그램, 실행환경을 추상화하는 기술
- 프로그램을 빌드/실행할 때 어떤 기기에서 사용해도 똑같은 환경을 조성할 수 있도록 도와주는 패키징 서비스

### 2-1. VM vs Container

- VM: host OS 위에 '각각' 게스트 OS를 가상화해서 사용하는 방식
- Container: 하나의 커널내에서 환경을 격리시키고 host 하드웨어 자원을 '공유'해서 사용하는 방식

### 3. 이미지

컨테이너를 실행하기 위한 모든 파일과 설정값들을 포함하고 있는 것

### 3-1. 도커이미지 파일 생성

```
FROM 베이스이미지: 버전
ADD ./static_web 폴더에 있는 내용을 컨테이너 내에서 /var/www/html 위치에 추가

WORKDIR 앞으로 명령어를 실행할 디렉토리
CMD 실행할 명령어

EXPOSE 열어놓을 포트
```

### Docker 명령어

- docker container 목록 확인
  ` > docker ps`
- 내려간 container까지 확인
  ` > docker container ls-a`
- docker image 목록 확인
  ` > docker images`
- docker로 nginx 띄우기 (컨테이너 올리기)
  ` > docker run -d -p 80:80 nginx`
- docker container 내리기
  ` > docker kill <container_id>`
- 종료된 container 지우기
  ` > docker container rm <container_id>`
- 이미지를 지우는 명령
  ` > docker rmi nginx`
