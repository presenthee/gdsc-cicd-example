# gdsc-cicd-example

## CI/CD란?

- Continuous Integration/Continuous Deployment(or Delivery)의 약자.
- 어플리케이션 개발 / 통합 / 테스트 / 배포 단계를 자동화하여 개발과 운영의 비용을 줄이고, 유저에게 더욱 짧은 주기로 업데이트를 제공할 수 있음.
- 이러한 자동화된 일련의 단계를 ***CI/CD pipeline*** 이라고 한다.

### CI(지속적 통합)

어플리케이션의 변경사항이 주기적으로 빌드 및 테스트되어 통합되는 것

→ 코드의 **빌드, 테스트, 통합 자동화**를 통해 달성할 수 있다.

- 개발자가 작성한 코드 merge를 위해 repo에 공유할 때, 자동으로 빌드 및 테스트가 수행되어 통합된다.
- 개발자가 push 할 때마다 push한 코드에 테스트가 실행되도록 한다.
- 👍 변경사항의 문제를 빠르게 파악하고 수정할 수 있다

### CD(지속적 배포, 제공)

CI과정을 거친 코드가 배포되기까지의 단계

- Delivery: 이전 단계(빌드, 테스트)를 통과한 코드가 자동으로 공유 repo에 release되는 것
- Deployment: 이전 빌드, 테스트, 병합 단계를 모두 통과한 코드가 자동으로 deploy되는 것

### 기존 어플리케이션 개발의 워크플로우

1. 개발자들 코드 수정
2. 각자 feature 브랜치에 코드를 push
3. 2의 코드를 통합(Intergration)
4. 통합된 코드에서 에러가 발생 → 디버깅 🐞
5. 수동 배포

### CI/CD 도입 후 어플리케이션 개발의 워크플로우

1. 개발자들 코드 수정
2. 각자 feature 브랜치에 코드를 push
3. push를 통해 lint, test, build 파이프라인 trigger
    1. 에러 발생 → 디버깅 🐞 후 다시 push
4. 3의 코드를 통합. 통합으로 인한 test 파이프라인 trigger
5. 환경에 따라 자동 or 수동 배포

## CI/CD 툴의 종류

- Jenkins
- Circle CI
- Github Actions
- GitLab

# Github Actions를 이용한 CI/CD 구축

Application workflow의 자동화를 위해 github에서 제공하는 platform.

**Github Actions**를 통해 CI/CD pipeline을 구축할 수 있다.

### 핵심 개념

- Workflow
    - event로 trigger되는 일련의 자동화된 프로세스.
    - Workflow를 configure하는 파일은 YAML 형식으로 작성
    - repo의 `.github/workflows` 디렉토리에 생성한다.
- Event
    - Workflow를 trigger하는 특정 활동
    - examples
        - 특정 브랜치로 Push 했을 때
        - 특정 브랜치로 Pull Request 했을 때
        - 특정 시간대에 (Cron)
        - manual
- Job
    - workflow를 이룬다.
    - 각 Job은 독립된 가상 머신(또는 컨테이너)인 runner 내에서 실행된다.
    - 다른 Job에 의존 관계를 가질 수 있고, 병렬 실행도 가능함
- Step
    - 하나의 job안에서 순차적으로 실행되는 단위
    - command 또는 script 또는 action이 될 수 있다.
- Action
    - 반복되는 task를 수행하는 step의 조합.
    - 개인적으로 만든 Action을 사용할 수도 있고, Marketplace에 있는 공용 Action을 사용할 수도 있음
        - [Github Marketplace](https://github.com/marketplace?type=actions)와 [Github Actions Repository](https://github.com/actions/)
