Git에서 브랜치를 나누어 작업한 후, 작업이 완료되면 통합 브랜치(보톨 main or master, or develop)에 병합시키게 된다. 이 때 어느 쪽을 사용하느냐에 따라, 통합 후 로그 및 브랜치의 이력이 매우 달라진다.

# Merge
![](https://velog.velcdn.com/images/sw_smj/post/227e8dc0-ab09-47ef-bc8b-2f10217f84a4/image.png)

우선 위와 같은 상황이라고 생각해보자. 각기 다른 브랜치에서 작업을 한 내역이 남아있는 경우이다. 이러한 상황에서 bugfix라는 브랜치를 master 브랜치에 병합하고 싶을 때, Merge를 하면 다음과 같이 브랜치 이력이 남게 된다.

![](https://velog.velcdn.com/images/sw_smj/post/22598557-47ab-476e-b61d-290eac46909b/image.png)


<br>


## Fastforward

단, 브랜치 병합에서 특이점은 다음과 같은 상황이다.

![](https://velog.velcdn.com/images/sw_smj/post/8e5b273a-440f-48c4-9381-c5623359dc86/image.png)

병합할 대상이 되는 브랜치에서 새로 브랜치가 나온 이래로 새로운 변화 이력이 없었다면, Fast-Forward(빨리감기) 병합 옵션을 선택하여 다음과 같이 병합할 수 있다.

이 경우 master 브랜치는 단순히 이동하기만 해도 bugfix의 내용을 모두 적용할 수 있다는 것이다.

![](https://velog.velcdn.com/images/sw_smj/post/e9eab1cc-f616-4531-b8b1-9cc63c1c0837/image.png)

이 경우는 master 브랜치였던 부분을 결국 bugfix의 마지막 상태로 빨리감기했다고 생각하면 되고, 이 상태에서 bugfix 브랜치를 삭제해버리면 결과적으로는 master 브랜치에 bugfix의 새로운 내역이 추가되는 결과와 같다.

단, 깃클라이언트(ex: 소스트리, Github Desktop)에서 'fast-forward가 가능해도 새 커밋으로 생성' 등의 옵션이 있는데, 이런 옵션을 선택하면 다음과 같이 이력을 남기는 것이 가능하다.

![](https://velog.velcdn.com/images/sw_smj/post/a8f42c73-03a7-4e29-b550-2315221977ea/image.png)

이렇게 fast-forward 병합이 가능한 경우라도, non fast-forward 병합을 적용시켜 실행하면 브랜치가 그대로 남게 된다.

➡ 이는 bugfix라는 브랜치로 실행했던 작업 확인 및 브랜치 관리 면에서 더욱 유용할 수 있다.

<br>

# Rebase

다시 Merge해야 하는 경우로 돌아와보자.

![](https://velog.velcdn.com/images/sw_smj/post/2ccd4035-7734-46f1-8423-302d89b0238f/image.png)

Fast-forward 병합이 불가능한 경우이다. 이때, 위의 방법처럼 수정 시점에 맞게 각 이력을 넣는 Merge 방법 외에, Rebase(재배치)를 선택할 수 있다.


![](https://velog.velcdn.com/images/sw_smj/post/840d96b7-157f-4c93-b1fe-1d29a63da866/image.png)

Rebase 병합을 적용하는 경우, 병합하는 브랜치는 master 브랜치의 이력 뒤로 이동하여 붙게 된다. 따라서 아래 그림과 같이 하나의 줄기로 이어지게 된다.

이때, Conflict는 각각의 커밋에서 발생하게 된다. 이때는 각각의 커밋에서 발생한 충돌 내용을 수정한다.


![](https://velog.velcdn.com/images/sw_smj/post/1db41491-36f0-46db-86e0-37ed9b205d11/image.png)

Rebase만 한 경우에는, 다음과 같이 master브랜치의 최종 위치는 그대로 유지된다. 따라서 master 브랜치의 헤드를 병합한 bugfix 브랜치의 헤드로 이동시키기 위해서는 다음과 같이 master 브랜치에서 fast-forward 병합을 하면 된다.

![](https://velog.velcdn.com/images/sw_smj/post/3a33753d-ccce-423e-b342-9aef56abf442/image.png)

