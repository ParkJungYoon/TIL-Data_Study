> **T 아카데미**에서 제공하는 강의를 바탕으로 작성하였습니다.

## CI/CD - Jenkins

### 1. 젠킨스 기본 개념과 동작 방식

**기본개념**

- Java Runtime Environment에서 동작
- 다양한 플러그인들을 활용해서 각종 자동화 작업을 처리

**Plugin**

- 대표적인 플러그인
  - `Credentials Plugin`: 각종 리소스 접근을 위한 중요한 정보들을 저장해 주는 플러그인.
  - `Git Plugin`
  - `Docker Pipeline`

**Pipeline**

CI/CD 파이프라인을 젠킨스에 구현하기 위한 일련의 플러그인들의 집합이자 구성.

**Pipeline Syntax**

1. Agent Section

- 젠킨스는 많을 일을 해야 하기 때문에 혼자 하기 버겁다.
- 여러 slave node 를 두고 일을 시킬 수 있는데, 이처럼 어떤 젠킨스가 일을 하게 할 것인지를 지정한다.
- 젠킨스 노드 관리에서 새로 노드를 띄우거나 혹은 docker이미지를 통해 처리할 수 있다.

2. Post section

- 스테이지가 끝난 이후의 결과에 따라서 후속 조치를 취할 수 있다.
- 성공 시에 성공 이메일, 실패하면 중단 혹은 건너뛰기 등등, 작업 결과에 따른 행동을 취할 수 있다.

  Ex) success, failure, always, cleanup

3. Stages Section

- 어떤 일들을 처리할 건지 일련의
  stage 를 정의함.
- 일종의 카테고리라고 보면 됨.

4. Steps Section

- 한 스테이지 안에서의 단계로
  일련의 스텝을 보여줌.
- Steps 내부는 여러 가지 스텝들로 구성되며 여러 작업들을 실행 가능.
- 빌드를 할 때 디렉터리를 옮겨서 빌드를 한다던가, 다른 플러그인을 깔아서 해당 플러그인의 메서드를 활용해서 일을 처리한다던지 하는 작업들을 할 수 있음.

* 예시

```
pipeline {
    agent any

    stages {
        stage(‘Build’) {
        steps {
        echo ‘Building..’
            }
        }
        stage(‘Test’) {
            steps {
            echo ‘Testing..’
            }
        }
        stage(‘Deploy’) {
            steps {
            echo ‘Deploying....’
            }
        }
    }
}
```
