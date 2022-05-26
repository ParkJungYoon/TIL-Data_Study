## CI/CD - Intro

- CI: Continuous Integration (지속적인 통합)
- CD: Continuous Delivery (지속적인 제공), Continuous Deployment (지속적인 배포)

애플리케이션 개발 단계를 **자동화**하여 애플리케이션 개발을 보다 **짧은 주기**로 고객에게 제공하는 방법이며, 새로운 코드 통합으로 인해 개발 및 운영팀에서 발생하는 문제(일명 통합지옥(Integration hell))를 해결하는 솔루션이다.

### CI

1. 코드 변경사항을 주기적으로 빈번하게 merge해야 한다.

2. 통합을 위한 단계 (빌드, 테스트, 머지)의 **자동화**

이를 통해 여러명의 개발자가 동시에 프로그램을 개발할 경우 **서로 충돌할 수 있는 문제를 해결**할 수 있다.

즉, CI는 빌드/테스트 자동화

<br>

### CD

CI를 통해 release 준비를 하고 그 다음 최종 배포를 거치게 된다.

이를 통해 애플리케이션 수동 배포 프로세스로 인한 프로세스 과부하 문제를 해결해준다.

즉, CD는 배포 자동화

<br>

### 예시 (CircleCI)

```
# .circleci/config.yml

version: 2.1

orbs:
  node: circleci/node@4.1

jobs:
  test: # test job
    docker:
      - image: <아이디>/node_app:0.0.1 # test를 실행할 node image
    steps:
      - checkout
      - node/install-packages: # yarn을 통해 package 설치
          pkg-manager: yarn
      - run: CURRENT_PATH=$(pwd)
      - run: sudo touch ${CURRENT_PATH}/.env.test # .env.test 환경 변수 파일 생성
      - run:
          name: "Setting environment vars for test env" # 테스트 환경을 위한 .env.test 파일 구성
          command: |
            echo "DATABASE_URL=${DATABASE_URL_TEST}" | sudo tee -a ${CURRENT_PATH}/.env.test
            echo "PORT=${PORT}" | sudo tee -a ${CURRENT_PATH}/.env.test
            echo "SECRET=${SECRET}" | sudo tee -a ${CURRENT_PATH}/.env.test
      - run: yarn install # install packages
      - run: yarn test    # start test with jest
  deploy:  # deploy job
    docker:
      - image: <아이디>/node_app:0.0.1
    steps:
      - add_ssh_keys:
          fingerprints:
            - ${FINGERPRINTS} # ssh public key를 사용할 fingerprints
      - run:
          name: "Run deploy script" # start deploy, 서버에 접속하여 deploy.sh 실행
          command: |
            ssh -o StrictHostKeyChecking=no ${HOST}@${HOSTNAME} /${TARGET_DIR}/deploy.sh
workflows:
  test-and-deploy: # workflow 이름
    jobs:
      - test  # test job
      - deploy:
          requires: # test가 끝나야 deploy 실행
              - test
          filters:
              branches:
                only: main # main 브랜치에 push 됐을 때만 실행
```

<br>

### tool 종류

1. Jenkins : Buildkite
2. GitHub Actions
3. GitLab CI/CD
4. CircleCI
5. Argo CD
