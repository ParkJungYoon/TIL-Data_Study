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
