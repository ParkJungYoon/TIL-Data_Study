> **Elice Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.

# Docker - 실습

## Docker로 Flask App 띄우기

### 1. flask로 app.py 파일 만들기

1. 정말 간단한 flask app.py

```py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def hello_world():
  return 'hello world'

if __name__ == '__main__':
  app.run(host='0.0.0.0', port=5000)
```

2. venv 생성

`python –m venv venv`

3. `venv\Scripts\activate.bat`

4. `pip3 install flask`

5. `python app.py `

-> 터미널 명령어를 dockerfile 이미지로

<br>

### 2. Dockerfile 작성하기

[Python - Official Image | Docker Hub](https://hub.docker.com/_/python)

```
FROM python:3.10-alpine
COPY . /app
WORKDIR /app
RUN pip3 install flask
RUN chmod +x /app/app.py
CMD ["python3", "app.py"]
```

(flask 라이브러리를 설치하고
app.py의 권한을 바꿔주는 명령이
실행)

- `FROM` : 어떤 리눅스를 사용할
  것인지에 대한 것
- `COPY` : 파일 복사
  - 현재 디렉토리 밑에 /app에 복사 (/app은 컨테이너의 디렉토리)
- `WORKERDIR` : 컨테이너에서 명령어가 실행되는 디렉토리
- `RUN` : 컨테이너를 구성할 파일을
  만들 때 사용
- `CMD` : 컨테이너가 실행된 후에 실행할 명령어

<br>

### 3. Docker build 후 Container로 띄우기

작성한 Dockerfile이 .txt면 ` > move Dockerfile.txt Dockerfile` 명령 입력

1. 작성한 Dockerfile로 Build 한다.

`docker build –t flask-app .`

이때 `flask-app:v2 .` 을 달아주면 `v2`라는 태그가 생긴다.

2. image가 잘 만들어졌는지 확인

`docker images`

3. 아직 컨테이너를 실행하지 않아서 컨테이너 목록은 비어있다.

`docker ps`

4. docker run으로 컨테이너를 실행

`docker run –d –p 5000:5000 flask-app`

- flask app을 만들 때 port를 5000번으로 넣었으면 -p 5000:5000 옵션으로 띄움
  (5001:5000으로 바꿀 수도 있음)

<br>

### < Docker Hub에서 Image Pull하기 >

직접 Docker File을 직접 작성하고 활용하는 것은 어려울 수 있다.

그래서 Docker Image를 받아 사용하는 것도 좋은 방법이다.

### Docker Hub란?

[Docker Hub 사이트](https://hub.docker.com/)

Docker Hub는 Docker 컨테이너 이미지를 위한 세계 최대 라이브러리 및 커뮤니티이다.

특히, Docker Hub에는 사전 빌드된 이미지들이 있어, 직접 구성할 필요 없이 Docker Hub에서 Pull해온 이미지들을 바로 사용할 수 있다.

### 사용 방법

1.  Docker Hub에서 원하는 이미지 이름을 검색
2.  우측 상단에 해당 이미지를 가져오기 위한 명령어를 복사

- 특정 태그를 붙이지않으면, 가장 최신 버전의 이미지를 가져온다.

3. docker가 실행된 터미널에서 복사한 명령어를 붙여넣기

(Error)

`Got permission denied while trying to connect to the Docker daemon socket at...`

-> 사용자가 /var/run/docker.sock 을 접근하려고 하였지만 권한이 없어 발생하는 문제로, 사용자가 root:docker 권한을 가지고 있어야 하기 때문이다.

(해결방법)

`sudo usermod -a -G docker $USER`

-> 사용자를 docker group에 포함시키도록 변경하면, 정상적으로 실행되는 것을 확인할 수 있다.
