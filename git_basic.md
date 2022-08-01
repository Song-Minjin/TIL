# **1\. 버전 관리**

> 프로젝트 상태가 변경되는 정보를 기록하고, 그에 맞게 관리하는 일

-   Git은 commit을 이용하여 버전이 달라지는 것을 관리한다.

<br>

## **기초 용어**

-   **git initialize (git 초기화)** : 컴퓨터 내 프로젝트를 Git이 관리하는 프로젝트로 설정하기. 처음 한 번만 하면 된다.
-   **commit** : 현재 프로젝트의 상태를 저장하는 것. commit이 포함하는 정보는 다음과 같다.  
    -   **commit id**  : commit 을 구분하기 위한 유일한 값.
    -   **작업 일자** (날짜와 시간)
    -   **작업한 사람** (작성자 author)
    -   **작업 내역** (commit 메시지)
    -   **작업 내역의 순서** : 해당 commit 의 직전 commit 이 무엇인지 정보
-   **history** : commit한 기록을 볼 수 있는 곳
-   **add (= staging)** : commit에 반영할 파일을 선택하는 것

<br>

# **2\. Repository**

> Git으로 관리되는 프로젝트

<br>

### **Local Repository**

> \= 로컬 repo  
> 내 컴퓨터에 저장되어 있는 리포지토리

-   **Tracking (= Branch Tracking)** : 로컬 repo가 원격 repo를 연결하는 것

<br>

### **Remote Repository**

> \= 원격 repo  
> Github처럼 다른 곳에서 접속할 수 있는 공간에 저장되어 있는 것

-   **Push** : 로컬 repo의 commit들을 원격 repo에 반영하는 것 \= commit들을 원격 repo에 _**밀어(Push)넣는다**_
-   **Pull** : 원격 repo의 commit들을 로컬 repo에 반영하는 것 \= commit들을 원격 repo에서 _**당겨(Pull)온다**_

**👉🏻** Github : 원격 repo가 저장되어 있는 공간 + 개발자 커뮤니티 기능

<br><br>


# **conflict (충돌)**

> 원격 repo와 로컬 repo 의 파일 변경사항이 겹친다는 것을 알려주는 것  
> 즉, 원격 repo와 로컬 repo에서 같은 파일 수정 → Git이 '어떤 파일을 최종으로 할까?' 라고 확인 메시지를 줌

-   충돌을 피하기 위해서는 아래 순서를 따라준다.
    1.  원격 repo와 로컬 repo의 상태를 똑같이 맞춰준 후에 변경작업을 해준다. (= 로컬 repo에 원격 repo 작업내역 pull 해오기)
    2.  원격 repo에 변경사항이 생겼다 하면 먼저 pull 한 후 → 로컬 repo에서 작업하기


<br><br>


# **Clone**

> 원격 repo를 내 컴퓨터에서도 사용할 수 있도록 가져오는 것. = 일종의 초기 다운로드

-   A 컴퓨터에서 작업 → github에 업로드 → B 컴퓨터에서 보고 싶을 때
-   다른 사람의 repo를 나도 다운로드하여 보고 싶을 때

👉🏻 이처럼 원격 repo를 내 컴퓨터에 가져오고 싶을 때, clone을 사용한다.

<br>

-   즉 clone이란, repo를 내 컴퓨터에 복제해오는 것
-   이 때, url을 통해 원격 repo에 접근할 수 있다.

<br>

여기서 잠깐! 💡 공개 repo 뿐만 아니라 비공개 repo라도 권한이 있다면 (ex: 해당 repo의 주인) clone해올 수 있다.
