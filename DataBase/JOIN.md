## JOIN (조인)이란?
>두 개 이상의 테이블이나 데이터베이스를 연결하여 **데이터를 검색**하는 방법


<br><br>

## JOIN의 종류

### 1. INNER JOIN

![](https://images.velog.io/images/yanghl98/post/a9f22ec1-6ba7-41ec-978f-0f44b976f161/image.png)

두 테이블의 `교집합`, 즉 두 테이블간 JOIN 조건을 만족하는 행을 반환한다.

#### 1) 명시적 조인 표현 
테이블에 조인을 하라는 것을 지정하기 위해 'JOIN' 키워드를 사용하고 ON의 키워드를 조인에 대한 구문을 지정하는데 사용한다.

```sql
SELECT *
FROM EMPLOYEE 
INNER JOIN DEPARTMENT
ON EMPLOYEE.DepartmentID = DEPARTMENT.DepartmentID;
```
  
#### 2) 암시적 조인 표현 

SELECT 구문의 FROM절에서 콤마(,)를 사용하여 단순히 조인을 위한 여러 테이블을 나열한다.

```sql
SELECT *
FROM EMPLOYEE, DEPARTMENT
WHERE EMPLOYEE.DepartmentID = DEPARTMENT.DepartmentID;
```

<br>

### 2. OUTER JOIN
OUTER JOIN이란 **조인 조건에서 동일한 값이 없는 행도 반환할 때 사용**한다.

<br>

### 2-1. LEFT OUTER JOIN
![](https://images.velog.io/images/yanghl98/post/a9780b09-a808-4860-a1ac-c64a1a327aa3/image.png)

조인문의 왼쪽에 있는 테이블의 모든 결과를 가져온 후 오른쪽 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표시한다.

```sql
SELECT *
FROM EMPLOYEE E LEFT OUTER JOIN DEPARTMENT D 
ON E.DEPARTMENTID = D.DEPARTMENTID;
```

<br>

### 2-2. RIGHT OUTER JOIN
![](https://images.velog.io/images/yanghl98/post/27098f6e-6f3b-4ee5-8f3d-4a51134704fb/image.png)

조인문의 오른쪽에 있는 테이블의 모든 결과를 가져온 후 왼쪽의 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표시한다. LEFT의 반대 버전.

```sql
SELECT *
FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D
ON E.DepartmentID = D.DepartmentID;
```

<br>


### 2-3. FULL OUTER JOIN

![](https://images.velog.io/images/yanghl98/post/5cfb50d5-6b1d-424f-894a-f97d7eaddf4c/image.png)

LEFT OUTER JOIN과 RIGHT OUTER JOIN을 합친 것으로, 양쪽 모두 조건이 일치하지 않는 것들까지 모두 결합하여 출력한다. 이것 역시 매칭되는 데이터가 없는 경우 NULL을 표시한다.

```sql
SELECT *
FROM EMPLOYEE E FULL OUTER JOIN DEPARTMENT D
ON E.DepartmentID = D.DepartmentID;
```

<br>

### 3. CROSS JOIN

![](https://images.velog.io/images/yanghl98/post/30ed3621-e112-4ec1-97ac-0121f8a7c35b/image.png)

Cartesian Product(카디션 곱)이라고도 하며 조인되는 두 테이블에서 `곱집합`을 반환한다. 

- 예를 들어 m열을 가진 테이블과 n열을 가진 테이블이 교차 조인되면 m*n 개의 열을 생성한다. 

```sql
SELECT *
FROM EMPLOYEE 
CROSS JOIN DEPARTMENT;
```

<br>

### 4. SELF JOIN
![](https://images.velog.io/images/yanghl98/post/7252760a-19d8-436c-a9d9-0d47f1054541/image.png)

**자기자신과 자기자신**을 조인하는 것으로, 하나의 테이블을 여러번 복사해서 조인한다고 생각하면 편하다.같은 테이블을 사용하기 때문에 테이블에 반드시 별명을 붙여야한다.

명령어가 따로 있는게 아니라 outer join이던 inner join이던 자기 자신의 테이블과 조인할 경우 SELF JOIN이라고 생각하면 된다.

```sql
SELECT
A.NAME, B.AGE
FROM TABLE_A A, TABLE_A B
```

<br><br>

## 출처
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDatabase%20SQL%5D%20JOIN.md
https://jhkang-tech.tistory.com/55
