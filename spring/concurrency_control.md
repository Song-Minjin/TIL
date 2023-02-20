
# Locking

## Shared Lock
> 공유락 → 읽기 O, 쓰기 X

- **공유 Lock은 데이터를 읽을 때 사용되어지는 Lock**이다.
- 이런 **공유 Lock은 공유 Lock 끼리는 동시에 접근이 가능**하다. 즉, 하나의 데이터를 읽는 것은 여러 사용자가 동시에 할 수 있다라는 것이다. 
- 하지만 공유 Lock이 설정된 데이터에 배타 Lock을 사용할 수는 없다.


### Exclusive Lock
> 배타락 → 읽기 X, 쓰기 X

- **배타 Lock은 데이터를 변경하고자 할 때 사용**되며, 트랜잭션이 완료될 때까지 유지된다. 
- **배타락은 Lock이 해제될 때까지 다른 트랜잭션(읽기 포함)은 해당 리소스에 접근할 수 없다.** 
- 또한 해당 Lock은 다른 트랜잭션이 수행되고 있는 데이터에 대해서는 접근하여 함께 Lock을 설정할 수 없다.    




### **비관적 락(Pessimistic Lock)**

- 트랜잭션이 충돌한다고 가정하고 락을 건다.
- DBMS의 락 기능을 사용한다. (ex. SELECT FOR UPDATE)
- 데이터 수정 시 즉시 트랜잭션 충돌여부를 확인할 수 있다.
- 코드
```java
@Lock(LockModeType.PESSIMISTIC_WRITE)
List<Posts> findAllByLocationId(Long locationId);
```


### **낙관적 락(Optimistic Lock)**

-   트랜잭션이 충돌하지 않는다고 가정한다.
-   자원에 락을 걸어서 선점하지말고 **커밋할 때 동시성 문제가 발생하면 그때 처리** 하자는 방법론입니다.
-   JPA에서는 자체적으로 제공하는 **버전 관리** 기능을 사용한다. (hashcode나 timestamp를 이용할 수도 있다.)
-   트랜잭션을 커밋하기 전까지는 충돌 여부를 확인할 수 없다.
-  `@Version` 어노테이션과 `@OptimisticLocking` 어노테이션을 사용하여 설정
-   `@OpimisticLocking`의 Type
	-   NONE: 낙관적 잠금을 사용하지 않음
	-   VERSION: @Version 어노테이션이 적용된 필드에 낙관적 잠금 사용
	-   DIRTY: 변경된 필드에 낙관적 잠금 사용
	-   ALL: 모든 필드에 낙관적 잠금 사용
-   코드

```java
@Lock(LockModeType.OPTIMISTIC) // 낙관적 락 설정
Optional<User> findByIdForUpdate(Long id);
```

```java
@Entity
// Lombok 생략
public class Posts{

@Id
@GeneratedValue
private Long id;

@Version
private Long version;
}
```
        
-   요약
    
    -   **비관적락** 은 데이터의 무결성이 중요하고, 충돌이 많이 발생하여 잦은 롤백으로 인한 효율성 문제가 발생하는것이 예상되는 시나리오에서 좋다.
    -   **낙관적락** 은 실제로 데이터 충돌이 자주 일어나지 않을것이라고 예상되는 시나리오에서 좋다.
    -   개인적인 생각으로는 데이터베이스 설계 단계에서 충돌여부가 발생하는지 어느정도 추측은 가능하나 확실치 않으므로, **애매한경우 비관적락** 을 걸어두고 서비스 도중 실제로 **충돌이 자주 일어나지 않는것이 확인** 된 경우에 **낙관적락** 을 사용하는 것이 좋을 것 같다.