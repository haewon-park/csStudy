# SQL vs NoSQL
## 🥕 SQL과 NoSQL의 차이점은 무엇인가요?

### SQL (Structured Query Language)
- **관계형 데이터베이스(RDBMS)**
- 데이터베이스 자체를 나타내기보단 특정 유형의 데이터베이스와 상호 작용하는데 사용하는 쿼리 언어 
- 데이터는 **정해진 데이터 스키마**에 따라 테이블에 저장됨
- 데이터는 **관계**를 통해 **여러 테이블에 분산**됨
- RDBMS에서 데이터 저장, 수정, 삭제 가능

1. **엄격한 스키마**

![schema](https://user-images.githubusercontent.com/63101648/127866569-b867f499-7fec-4c92-9a48-46aa0157bb8e.jpeg)

2. **관계**

![relation](https://user-images.githubusercontent.com/63101648/127866793-ecaeab0f-6559-4fac-8dbd-551654d46a43.jpeg)


### NoSQL
- **비관계형** 또는 **분산 데이터베이스**
- NO 스키마, NO 관계
- 레코드를 Document라고 하며 JSON과 비슷한 형태를 지님
- 수직적, 수평적 확장 모두 가능

⭐NoSQL에는 조인이라는 개념이 없다.
- 컬렉션을 통해 데이터를 복제하고 각 컬렉션 일부분에 속하는 데이터를 산출하도록 함
- 이 경우 데이터가 중복되어 서로 영향을 줄 위험이 존재

```조인을 잘 사용하지 않고 자주 변경되지 않는 데이터일 때 사용하는 것이 효율적이다.```  

### ✅정리 
 - **SQL은 테이블 구조**를 가지고 **스키마를 준수**하며 **수직적 확장만 가능**
 -  **NoSQL은 Document 구조**로서 **테이블을 유연한게 변경**할 수 있고 **수직적, 수평적 확장이 모두 가능**하다.
 - 대표적인 **SQL은 MySQL**이 존재하고 **NoSQL에는 MongoDB**가 존재한다.
 
 

<br>

 ## 🥕 SQL의 장단점은 무엇인가요?
 ### **SQL 장점**
- 명확하게 정의된 스키마  ( 데이터 무결성 보장)
- 관계는 각 데이터를 중복없이 한번만 저장이 된다. 
 ### **SQL 단점**
 - 관계를 맺고 있기에 JOIN문이 많은 복잡한 쿼리가 만들어질 수 있다.
 - 수평적 확장이 어렵다. ( 수직적 확장만 가능)

<br>


 ## 🥕 NoSQL의 장단점은 무엇인가요?
 ### **NoSQL 장점**
- 스키마가 없어서 유연하다.
- 언제든지 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장된다.
 ### **NoSQL 단점**
 - 데이터가 여러 컬렉션에 중복되어 있기 때문에, 수정할 땐 모든 컬렉션에서 수행해야한다. 

<br>


 ## 🥕 수직적, 수평적 확장이 무엇인가요?
 ![SCALING](https://user-images.githubusercontent.com/63101648/127767462-b436d997-2d85-41d3-999c-0bb9bc1f0f14.jpeg)

### ✅ 수직적 확장 (Vertical Scaling)
- 데이터베이스 서버의 성능 향상
- Ex) CPU 업그레이드
### ✅ 수평적 확장 (Horizontal Scaling)
- 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨
- 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동 


<br>

 ## 🥕 둘 중에 어느 것이 더 좋은가요?
 ❌ 정답은 없다! 경우에 따라 다름!

 🔆 **고려할 점**
 - **어떤 데이터**를 다루는가
 - **어떤 애플리케이션**에서 사용되는가 
 ### ✅ **SQL의 경우**
 - 관계를 맺고 데이터가 자주 변경되는 애플리케이션 
 - 명확한 스키마가 사용자와 데이터에게 중요한 경우 
 ### ✅ **NoSQL의 경우**
- 정확한 데이터 구조를 알 수 없거나 변경 또는 확장될 수 있는 경우
- 읽기처리를 자주 하지만 데이터를 자주 변경하지 않는 경우
- 데이터를 수평적으로 확장해야 하는 경우
- 막대한 양의 데이터를 다뤄야 하는 경우

<br>

## 출처
- https://jungeun960.tistory.com/166
- https://siyoon210.tistory.com/130
- https://ko.myservername.com/sql-vs-nosql-exact-differences#What_is_SQL
