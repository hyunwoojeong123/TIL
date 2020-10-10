# 1. 모든 user 레코드 조회

```django
# orm
User.objects.all()
```

```sqlite
-- sql
SELECT * FROM users_user;
```



# 2. user 레코드 생성

```django
# orm
User.objects.create(first_name = 'Hyunwoo', last_name = 'Jeong')
```

```sqlite
-- sql
-- 모든칼럼 다 쓸때
INSERT INTO users_user VALUES('Hyunwoo', 'JEONG')
-- 아이디 빼고 다른 컬럼을 명시해주게 되면, 그것만 적으면 됨
INSERT INTO "users_user" ("first_name", "last_name", "age", "country", "phone", "balance") VALUES ('길동', '홍', 100, '제주도', '1234', 10000);
```



# 3. 해당 user 레코드 조회

```django
# orm
User.objects.get(pk=101)
```

```sqlite
-- sql
SELECT * FROM users_user WHERE id = 101;
```



# 4. 해당 user 레코드 수정

```django
# orm
user.last_name = '김'
user.save()
```

```sqlite
-- sql
UPDATE "users_user" SET "last_name" = '김' WHERE "users_user"."id" = 101
```



# 5. 해당 user 레코드 삭제

```django
user = User.objects.get(pk=101)
user.delete()
```

```sql
DELETE FROM users_user WHERE id=101
```



# 조건에 따른 쿼리문

## 1. 전체 인원 수

```django
len(User.objects.all())
```

```sql
SELECT COUNT(*) FROM users_user
```



## 2. 나이가 30인 사람의 이름

```django
User.objects.filter(age=30).values('first_name')
```

```sqlite
SELECT first_name FROM users_user WHERE age = 30;
```



## 3. 나이가 30살 이상인 사람의 인원 수

```django
User.objects.filter(age_gte=30).count()
```

```sqlite
SELECT COUNT(*) FROM users_user WHERE age>=30;
```



## 4. 나이가 20살 이하인 사람의 인원 수

```django
User.objects.filter(age_lte=20),count()
```

```sqlite
SELECT COUNT(*) FROM users_user WHERE age<=20;
```



## 5. 나이가 30이면서 성이 김씨인 사람의 인원 수

```django
User.objects.filter(age=30, last_name = '김').count()
```

```sql
SELECT COUNT(*) FROM users_user WHERE age=30 AND last_name='김';
```



## 6. 나이가 30이거나 성이 김씨인 사람의 인원 수

```django
# orm
from django.db.models import Q
User.objects.filter(Q(age=30)|Q(last_name='김')).count()
```

```sqlite
-- sql
SELECT COUNT(*) FROM users_user WHERE age=30 OR last_name='김';
```



## 7. 지역번호가 02인 사람의 인원 수

```django
# orm
User.objects.filter(phone__startswith = '02-').count()
```

```sql
-- sql
SELECT COUNT(*) FROM users_user WHERE phone LIKE '02-%';
```



## 8. 거주 지역이 강원도이면서 성이 황씨인 사람의 이름

```django
# orm
User.objects.filter(live = '강원도', last_name='황씨').values('first_name')
```

```sql
SELECT first_name FROM users_user WHERE live='강원도' and last_name='황';
```



# 정렬 및 LIMIT, OFFSET

## 1. 나이가 많은 사람 순으로 10명

```
# orm
User.objects.order_by('-age')[:10]
```

```sql
-- sql
SELECT * FROM users_user ORDER BY age DESC LIMIT 10;
```



## 2. 잔액이 적은 사람순으로 10명

```django
User.objects.order_by('balance')[:10]
```

```sql
SELECT * FROM users_user ORDER BY balance ASC LIMIT 10;
```



## 3. 잔고는 오름차순, 나이는 내림차순으로 10명

```django
User.objects.order_by('balance','-age')[:10]
```

```sql
SELECT * FROM users_user ORDER BY balance ASC, age DESC LIMIT 10
```



## 4. 성, 이름 내림차순 순으로 5번째 있는 사람

```django
# orm
User.objects.order_by('-last_name', '-first_name')[4]
```

```sql
-- sql
SELECT * FROM users_user ORDER BY last_name DESC, first_name DESC LIMIT 1 OFFSET 4;
```



# 표현식

## 1. 전체 평균 나이

```django
from django.db.models import Avg
User.objects.aggregate(AVG('age'))
```

```sql
SELECT AVG(age) FROM users_user;
```



## 2. 김씨의 평균 나이

```django
from django.db.models import avg
User.objects.filter(last_name ='김').aggregate(AVG('age'))
```

```sql
SELECT AVG(age) FROM users_user WHERE last_name='김';
```



## 3. 강원도에 사는 사람의 평균 계좌 잔고

```django
# orm
User.objects.filter(country='강원도').aggregate(AVG('balance'))
```

```sql
-- sql
SELECT AVG(balance) FROM users_user WHERE country='강원도';
```



## 4. 계좌 잔액 중 가장 높은 값

```django
# orm
from django.db.models import Max
User.objects.aggregate(Max('balance'))
```

```sql
SELECT MAX(balance) FROM users_user;
```



## 5. 계좌 잔액 총액

```django
from django.db.models import Sum
User.objects.aggregate(Sum('balance'))
```

```sql
SELECT SUM(balance) FROM users_user;
```

