Git을 활용한 협업이 정말 중요한 것은 알고 있으나, 실질적으로 팀프로젝트에서, 혹은 실무에서 어떤 방식과 흐름으로 git 협업 프로젝트를 하고 있는지 정리해본다.


<br>

# Git Flow



: 현재 Git으로 개발할 때 거의 표준과 같이 사용되는 방법론

- Vincent Driessen이라는 사람의 블로그 글에 의해 널리 퍼지기 시작함

- Git Flow에서는 **총 5가지의 브랜치**를 사용하여 운영한다.

    - **`master`** : 전체적인 기준이 되는 브랜치. 제품을 배포하는 브랜치

    - **`develop`** : 개발 브랜치. 개발자들의 병합 대상 브랜치이다.

    - **`feature`** : 단위 기능을 개발하는 브랜치. 보통 이슈 번호와 이름을 붙여 작업하기도 한다.

    - **`release`** : 배포를 위해 master 브랜치로 보내기 전 먼저 QA(품질 검사, Quality Control)를 하기 위한 브랜치

    - **`hotfix`** : master 브랜치로 배포를 했는데, 버그가 생겼을 때 긴급 수정하는 브랜치

![](https://velog.velcdn.com/images/sw_smj/post/278c64c6-ab38-439f-bc00-522d7c5fe367/image.png)

<br>

규모가 있는 개발을 할 경우, 브랜치만으로 관리를 하지 않고 Fork와 Pull Request를 활용하여 협력을 하고는 한다.

<br>

## Fork & Pull Requests



: 브랜치와 비슷하지만, 프로젝트를 통째로 외부로 복제하여 개발을 하는 방식

- 브랜치처럼 Merge를 하는 것이 아니라, Pull Requests로 프로젝트 관리자에게 Merge 요청을 보내면 관리자가 PR된 코드를 보고 적절성을 판단하여 기능을 붙인다.