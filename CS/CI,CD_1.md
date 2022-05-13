## CI/CD - Intro

- CI: Continuous Integration (지속적인 통합)
- CD: Continuous Delivery (지속적인 제공), Continuous Deployment (지속적인 배포)

애플리케이션 개발 단계를 **자동화**하여 애플리케이션 개발을 보다 **짧은 주기**로 고객에게 제공하는 방법이며, 새로운 코드 통합으로 인해 개발 및 운영팀에서 발생하는 문제(일명 통합지옥(Integration hell))를 해결하는 솔루션이다.

### CI

1. 코드 변경사항을 주기적으로 빈번하게 merge해야 한다.

2. 통합을 위한 단계 (빌드, 테스트, 머지)의 **자동화**

이를 통해 여러명의 개발자가 동시에 프로그램을 개발할 경우 서로 충돌할 수 있는 문제를 해결할 수 있다.

즉, CI는 빌드/테스트 자동화

<br>

### CD

CI를 통해 release 준비를 하고 그 다음 최종 배포를 거치게 된다.

이를 통해 애플리케이션 수동 배포 프로세스로 인한 프로세스 과부하 문제를 해결해준다.

즉, CD는 배포 자동화

<br>

### tool 종류

1. Jenkins : Buildkite
2. GitHub Actions
3. GitLab CI/CD
4. CircleCI
