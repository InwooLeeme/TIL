# 프로그래머스 SQL 문제 풀이

#### [이름에 el이 들어가는 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59047)

```sql
select ANIMAL_ID, NAME from ANIMAL_INS WHERE ANIMAL_TYPE="Dog" and NAME LIKE "%el%" order by NAME ASC
```

sql의 select문을 이용해서 ANIMAL_ID, NAME을 선택해준 이후 ANIMAL_TYPE이 강아지인 것과 이름에 el이 존재하기만 하면 되는 것들을 이름을 기준으로 오름차순으로 뽑으면 된다.

#### [NULL 처리하기](https://school.programmers.co.kr/learn/courses/30/lessons/59410)

```sql
select ANIMAL_TYPE, IFNULL(NAME, "No name"), SEX_UPON_INTAKE from ANIMAL_INS
```

동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, 이름이 없는 동물의 이름은 "No name"으로 표시하여야하기 때문에 IFNULL을 사용해서 NAME의 속성 값이 NULL인 경우 "No name"으로 출력되게 하면 된다.

#### [잡은 물고기의 평균 길이 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/293259)

```sql
// 잡은 물고기의 평균 길이를 출력하는 SQL문을 작성해주세요.

// 평균 길이를 나타내는 컬럼 명은 AVERAGE_LENGTH로 해주세요.
// 평균 길이는 소수점 3째자리에서 반올림하며, 10cm 이하의 물고기들은 10cm 로 취급하여 /
// 평균 길이를 구해주세요.

select ROUND(AVG(IFNULL(LENGTH, 10)), 2) as AVERAGE_LENGTH from FISH_INFO
```

수학 함수를 잘 쓰면 된다.

#### [특정 물고기를 잡은 총 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298518)

```sql
// FISH_INFO 테이블에서 잡은 BASS와 SNAPPER의 수를 출력하는 SQL 문을 작성해주세요.
// 컬럼명은 FISH_COUNT로 해주세요.

select COUNT(FISH_TYPE) as FISH_COUNT from FISH_INFO where FISH_TYPE IN (select FISH_TYPE from FISH_NAME_INFO where FISH_NAME IN ('BASS', 'SNAPPER'))
```

조인을 사용하지 않고 서브쿼리를 이용해서 풀었다.

#### [루시와 엘라 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59046)

```sql
// 동물 보호소에 들어온 동물 중 이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인
// 동물의 아이디와 이름, 성별 및 중성화 여부를 조회하는 SQL 문을 작성해주세요.
select ANIMAL_ID, NAME, SEX_UPON_INTAKE from ANIMAL_INS where NAME in ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty') order by ANIMAL_ID ASC
```

## 2025.11.05

#### [물고기 종류 별 잡은 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/293257)

```sql
// FISH_NAME_INFO에서 물고기의 종류 별 물고기의 이름과 잡은 수를 출력하는
// SQL문을 작성해주세요.

// 물고기의 이름 컬럼명은 FISH_NAME, 잡은 수 컬럼명은 FISH_COUNT로 해주세요.
// 결과는 잡은 수 기준으로 내림차순 정렬해주세요.


select count(*) as FISH_COUNT, N.FISH_NAME
from FISH_NAME_INFO N
JOIN FISH_INFO I
ON N.FISH_TYPE = I.FISH_TYPE
GROUP BY N.FISH_NAME
ORDER BY FISH_COUNT DESC
```

JOIN축약을 이용해서 GROUP BY와 같이 이용해서 풀었다.

#### [ROOT 아이템 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/273710)

```sql
// ROOT 아이템을 찾아 아이템 ID(ITEM_ID), 아이템 명(ITEM_NAME)을 출력하는 SQL문을 작성해 주세요. 이때, 결과는 아이템 ID를 기준으로 오름차순 정렬해 주세요.
select ITEM_ID, ITEM_NAME
from ITEM_INFO
where ITEM_ID in (
    select ITEM_ID
    from ITEM_TREE
    where PARENT_ITEM_ID IS NULL
)
```

JOIN을 이용해서 풀 수도 있긴한데.... 그냥 서브쿼리로 풀었다.
