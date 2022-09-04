# 그룹 함수

그룹 함수의 종류에는 ROLLUP, CUBE, SETS 등이 있다. 세 함수 모두 GROUP BY와 함께 붙여 사용할 수 있다.


##1.  ROLLUP



: 소그룹간의 합계와 총계를 같이 계산해주는 함수

- 그룹핑 기준 필드를 ROLLUP() 괄호 안에 감싸 나열하며, 기준 필드가 여러 개이면 콤마(`,`)로 구분한다.

- 그룹핑되는 컬럼의 수를 N개라고 할 때, **N+1** 레벨의 소계가 생성된다.

### 👉🏻 활용 1 - 필드가 1개 일 때
  ```sql
 -- 비교 : ROLLUP을 사용하지 않았을 때
 SELECT ID, EMPLOYEE_NAME, DEPT_ID, SUM(SALARY)
  FROM EMPLOYEES e
  GROUP BY DEPT_ID
  ORDER BY ID;
   
  -- ROLLUP 사용한 경우
  SELECT ID, EMPLOYEE_NAME, DEPT_ID, SUM(SALARY)
  FROM EMPLOYEES e
  GROUP BY ROLLUP (DEPT_ID)
  ORDER BY ID;
  ```

➡ 이렇게 ROLLUP을 사용하면 결과값에서 `NULL`이라는 이름으로 `SUM(SALARY)`의 총합이 추가된 것을 확인할 수 있다.



### 👉🏻 활용 2 - 필드가 여러 개 일 때

```sql
-- ROLLUP을 사용한 경우
SELECT ID, DEPT_ID 부서번호, JOB_ID 직무, COUNT(*) 직원 수
FROM EMPLOYEES e
GROUP BY ROLLUP(DEPT_ID, JOB_ID)
ORDER BY DEPT_ID;
  ```

➡ 그냥 `GROUP BY`만 사용한 경우에서는 부서번호 + 직무별로 그룹핑되어 보여졌던 것에 추가적으로, ROLLUP으로 새로운 row들을 생성한다.

- **새로 생성되는 행들**

  - 부서번호별 총 직원 수
  - 전체 직원 수


> 💡 **주의**
> 
> - ROLLUP함수를 사용할 때에는, 그룹핑 순서에 따라 결과 set이 달라진다.
> ➡ 따라서, 소계를 구할 필드를 먼저 그룹핑해야 한다.


<br>


## 2. CUBE



: GROUPBY 절에 명시한 모든 컬럼에 대해 소그룹 합계를 계산하여 다차원적인 소계를 도출하는 함수

- ROLLUP에서는 1차 그룹핑 필드에 대해서만 소계를 구하는 반면, CUBE 함수는 모든 기준 필드에 대한 소계를 다 구한다.

### 👉🏻 활용

```sql
SELECT ID, DEPT_ID 부서번호, JOB_ID 직무, COUNT(*) 직원 수
FROM EMPLOYEES e
GROUP BY CUBE(DEPT_ID, JOB_ID)
ORDER BY DEPT_ID;
```

➡ `ROLLUP` 함수를 썼을 때보다는 조금 복잡하게 나온다. 부서번호별 직원 수 뿐만 아니라, 직무별 직원 수도 한 번에 확인할 수 있다.



<br>

## 3. GROUPING SETS



: 특정 항목에 대한 소계를 계산하는 함수

- 각각의 컬럼으로 `GROUP BY`한 값을 `UNION ALL`한 것과 동일한 결과를 보여줌

### 👉🏻 활용

```sql
SELECT ID, DEPT_ID 부서번호, JOB_ID 직무, COUNT(*) 직원 수
FROM EMPLOYEES e
GROUP BY GROUPING SETS(DEPT_ID, JOB_ID)
ORDER BY DEPT_ID;
```

➡ 앞의 `ROLLUP`, `CUBE`보다 결과가 훨씬 단순하게 나온다.

- `ROLLUP`, `CUBE`는 GROUP BY 결과 + 소그룹 합계 + 토탈 합계를 보여줌

- 반면 `GROUPING SETS`는 각 소그룹별 합계만 간단히 보여줌
