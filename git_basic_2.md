Git으로는 다음과 같은 작업 방식을 정말 편리하게 할 수 있다.

1.  누가 이 작업을 할 것인지 정한다.
2.  각자 맡은 것을 작업한다.
3.  각자 작업을 프로젝트에 합칠 수 있게 공유한다.
4.  작업한 내용을 리뷰하고 최종적으로 프로젝트에 반영한다.

이러한 방식은 실제로 개발자들이 협업 프로젝트를 할 때 진행하는 방식이다. 이 때, 협업하는 조직마다 Git을 사용하는 방법(깃 컨벤션)을 정해두고 약속에 지켜 협업한다.

<br>

# **Issue**

> 프로젝트에서 해결해야 하는 문제

-   **Bug Report (버그 리포트)** : 버그(프로그램이 원하는대로 동작하지 않는 것)을 신고
-   **Enhancement** : 기능 추가 등의 프로젝트 개선 제안
-   위 문제들을 해결하기 위한 작업단위

**개발자들의 'issue (이슈)'라는 용어 사용법**

-   회원가입 기능에서 버그 있네요. 이슈 등록해둘게요~
-   여기 버튼을 눈에 더 잘 띄게 고치면 좋을 것 같은데요? 이슈 등록해둘게요.
-   6번 이슈 제가 처리할게요. 제 앞으로 할당해두겠습니다.

<br>

## **Issue Tracker**

> \= Issue Tracking Tool(이슈 추적 도구), 이슈 트래커

-   이슈를 추적(tracking)하면서 관리할 수 있는 툴
-   Github, Jira, Trello, YouTrack 등


<br>


## **Github에서 Issue 등록하기**

[##_Image|kage@twpOv/btrILe8KSxH/M1kuWkhF4AmVq8ebcmDrOK/img.png|CDM|1.3|{"originWidth":1462,"originHeight":760,"style":"alignCenter","width":700,"height":364}_##]

-   **Assignees(담당자)** : 이 이슈 작업자 및 연관자
-   **Labels** : 이 issue가 어떤 종류인지 분류해주는 것. Github이 제공하는 기본 라벨도 사용 가능하며, 직접 만들어 사용도 가능.  
    -   bug : 예기치 않은 문제 또는 의도하지 않은 동작(버그)
    -   documentation : 문서를 개선/추가해야 할 필요가 있음
    -   duplicate : 해당 이슈 또는 PR이 기존에 있음
    -   enhancement : 새로운 기능 추가/개선 요청
    -   good first issue : 처음 프로젝트에 참여하는 사람이 작업하기 쉬운 이슈
    -   help wanted : 관리자가 문제 또는 PR 요청에 대한 도움을 원함
    -   invalid : 이슈 또는 PR 요청이 더이상 관련이 없음
    -   question : 이슈 또는 풀 요청에 추가 정보가 필요함
    -   wontfix : 문제나 PR 요청에서 작업이 계속되지 않음

           \* **PR** = **Pull Request** : 내가 수정한 코드가 있으니 내 branch를 가져가 검토 후 병합해달라 요청하는 것

-   **이슈 번호** : #숫자 형태. 작업할 때 issue 번호를 정보로 사용하게 된다. repo 기준으로 1부터 생성된다.
-   **Close Issue** : 이슈를 종료한다. 더이상 이슈를 남겨둘 필요가 없거나 작업이 완료되었을 때 실시. 이슈가 왜 종료되었는지를 기록하면 나중에 프로젝트 관리할 때 더욱 편리함
-   **Reopen Issue** : 이슈 종료 후, 필요할 때 다시 이슈 열어주기 가능


<br><br>

# **Branch**

> 특정 commit에서 나뭇가지처럼 갈라져나와 작업하는 것. 보통 기능별로 브랜치 이름을 만들어 작업함

-   **checkout** : 현재 작업하는 브랜치를 선택하는 것
  
<br>

## **Branch 이름 붙이기**

**📌**

브랜치명은 규칙을 가지고 잘 이름 지으면 프로젝트 관리가 쉬워짐

-   feature/이슈번호\_관리 쉬운 이름
    -   feature : 기능 개발하는 브랜치에 관행적으로 붙여주는 이름

<br>

## **Branch 용어 알아보기**

[##_Image|kage@bIyktO/btrIEYl1212/7kbRPkDIAYP94TxbSkKCnk/img.png|CDM|1.3|{"originWidth":537,"originHeight":28,"style":"alignCenter"}_##]

-   origin/main : origin(연결된 원격 repo)의 main 브랜치
-   origin/HEAD : 현재 작업중인 commit을 가리킴. 즉, origin(연결된 원격 repo)의 최신 commit
-   main : 로컬 repo의 main 브랜치

<br><br>

# **Flow**

> 흐름. commit하고 작업하는 방법

-   **Github-Flow** : 웹 프로젝트 개발에서 많이 사용함
-   **GitLab-Flow**
-   **Git-Flow**

<br><br>

# **Merge**

> 병합. 브랜치를 다른 브랜치에 합치는 것

-   즉, 특정 브랜치의 commit들을 다른 브랜치의 commit 내역에 모두 반영하는 것
-   실제 프로젝트에서는 작업내역을 모두 merge할 브랜치를 정해두고 작업함
-   작업이 완료되어 merge한 후, 작업했던 브랜치는 보통 삭제해준다 → 나중에 브랜치 설정이 꼬이는 것 방지!



<br><br>

# **Merge Conflict**

> Merge(병합)할 때 발생하는 충돌

**👉🏻** Git : 충돌하는 내용 중 어느 내용을 반영할지 묻는 메시지를 주는 기능이 있음

-   하나의 파일을 여러 군데에서 변경하려고 하면, 여러 변경 내용 중 어떤 것을 브랜치에 반영할지 파악하기 위해 정보를 제공한다.

```
<<<<<<< HEAD
{현재 브랜치의 다른 파일 내용}
=======
{충돌나는 브랜치명 또는 commit에서의 다른 파일 내용}
>>>>>>> 충돌나는 브랜치명 또는 commmit 아이디
```

-   충돌이 나는 부분 : `<<<<<<<` 여기 `>>>>>>>`

<br>

## **충돌 해결 방법** 

1.  내가 원하는 대로 파일을 수정한다.
2.  <<<<<<< HEAD , \======= , \>>>>>>> 충돌나는 브랜치명 또는 commit 아이디 를 지운다.
3.  그 후 이렇게 수정된 파일을 다시 commit 한다.