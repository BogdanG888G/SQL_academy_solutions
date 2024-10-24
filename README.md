# SQL_academy_solutions

В этом репозитории содержатся все мои запросы по SQL, во время выполнения тренажера на сайте : **[SQL Academy]()**

<br>

42. Medium 🟠 🟠<br> Сколько времени обучающийся будет находиться в школе, учась со 2-ой по 4-ую пару? [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/42)

<details>

  <summary>Решение</summary>

```sql
select TIMEDIFF(
(select end_pair from Timepair where id = 4),
(select start_pair from Timepair where id = 2)
) as time


```

</details>

43. Medium 🟠 🟠 <br>Выведите все фамилии учителей, которые преподают Физкультуру (Физическую Культуру). Отсортировать фамилии в алфавитном порядке [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/43)

<details>
<summary>Решение</summary>

```sql
select last_name from Teacher JOIN Schedule 
on Schedule.teacher = Teacher.id JOIN Subject
on Subject.id = Schedule.subject

where name = "Physical Culture"
ORDER BY last_name ASC 

```

</details>

44. Hard 🔴🔴🔴<br>
Найти максимальный возраст среди студентов, учащихся в 10 классе [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/44)

<details>
<summary>Решение</summary>

```sql
select max(abs(TIMESTAMPDIFF(YEAR, CURDATE(), birthday))) as max_year 

from Class JOIN 
Student_in_class on Student_in_class.class = Class.id
JOIN Student on Student.id = Student_in_class.student

where Class.name like '10%'

```

</details>

45. Hard 🔴🔴🔴<br>
Какие классы использовались чаще всего для занятий. Вывести те, которые использовались чаще всего [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/45)

<details>
<summary>Решение (через cte)</summary>

```sql
with t as (
select classroom, 
count(*) as c 

from Schedule

group by classroom

order by c desc
)

select classroom from t
where c = (select max(c) from t)
```
</details>

<details>
<summary>Решение (без cte)</summary>

```sql
select classroom from Schedule
group by classroom

having count(*)  = 
(select count(*) from Schedule
group by classroom 
order by count(*) desc 
limit 1) 
```
</details>

46. Medium 🟠🟠<br>
В каких классах будет преподавать Крауз "Krauze"?[(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/46)

<details>
<summary>Решение</summary>

```sql
select DISTINCT name 
from Teacher
JOIN Schedule on Schedule.teacher = Teacher.id
JOIN Class on Class.id = Schedule.class

WHERE last_name = "Krauze"
```

</details>

47. Medium 🟠🟠<br>
Как много классов было у Крауза 30 Августа 2019 года?[(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/47)

<details>
<summary>Решение</summary>

```sql
select count(DISTINCT name) as count 
from Teacher
JOIN Schedule on Schedule.teacher = Teacher.id
JOIN Class on Class.id = Schedule.class

where last_name = "Krauze"

```

</details>

48. Medium 🟠🟠<br>
Вывести количество студентов в каждом классе в порядке убывания [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/48)

<details>
<summary>Решение</summary>

```sql
select name, count(*) as count
from Class JOIN Student_in_class
on Student_in_class.class = Class.id

GROUP BY name

ORDER BY count desc
```

</details>

49. Medium 🟠🟠<br>
Какой процент студентов, учащихся в "10 А" [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/49)

<details>
<summary>Решение</summary>

```sql
select 
(SELECT count(name) FROM Class
JOIN Student_in_class ON Class.id = Student_in_class.class
WHERE name = "10 A") / COUNT(*) * 100 as percent
FROM Class
JOIN Student_in_class ON Class.id = Student_in_class.class

```

</details>

50. Medium 🟠🟠<br>
Какой процент студентов родилось в 2000 году? [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/50)

<details>

<summary>Решение</summary>

```sql
SELECT 
FLOOR((SELECT COUNT(*) FROM Student
WHERE YEAR(birthday) = 2000) / COUNT(*) * 100) as percent
FROM Student
```

</details>


51. Medium 🟠🟠<br>
Добавьте продукт с названием "Сыр" и отнесите его к типу "Еда" [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/51)

<details>

<summary>Решение</summary>

```sql
INSERT INTO Goods
SET good_id   = (
    SELECT COUNT(*) + 1
    FROM Goods AS gs
),
    good_name = 'Cheese',
    type      = (
        SELECT good_type_id
        FROM GoodTypes
        WHERE good_type_name = 'food'
    );
```

</details>

52. Medium 🟠🟠<br>
Добавьте в список типов товаров (GoodTypes) новый тип "auto" [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/52)

<details>

<summary>Решение</summary>

```sql
INSERT INTO GoodTypes
SET good_type_id   = (
    SELECT COUNT(*) + 1
    FROM GoodTypes AS gt
),
    good_type_name = 'auto';
```

</details>


52. Medium 🟠🟠<br>
Добавьте в список типов товаров (GoodTypes) новый тип "auto" [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/52)

<details>

<summary>Решение</summary>

```sql
INSERT INTO GoodTypes
SET good_type_id   = (
    SELECT COUNT(*) + 1
    FROM GoodTypes AS gt
),
    good_type_name = 'auto';
```

</details>

53. Easy 🟢<br>
Поменяйте имя "Andie Quincey" на новое - "Andie Anthony" [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/53)

<details>

<summary>Решение</summary>

```sql
UPDATE FamilyMembers
SET member_name = 'Andie Anthony'
WHERE member_name = 'Andie Quincey';
```

</details>



59.  Medium 🟠🟠<br>
Выведите пользователей, у которых белорусский номер телефона (код "+375")
 [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/59)

<details>

<summary>Решение</summary>

```sql
SELECT * FROM Users
WHERE phone_number LIKE '+375%'
```

</details>

60. Hard 🔴🔴🔴<br>
Выведите идентификаторы учителей, которые преподавали хотя бы один раз за все время в каждом из одиннадцатых классов [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/60)

<details>

<summary>Решение</summary>

```sql
SELECT teacher FROM (
SELECT Schedule.teacher, Class.name, 
ROW_NUMBER() OVER(PARTITION BY Schedule.teacher ORDER BY Class.name) as dc 
FROM 
Teacher JOIN Schedule on Schedule.teacher = Teacher.id
JOIN Class on Class.id = Schedule.class

where Class.name LIKE '11%'
GROUP BY Schedule.teacher, Class.name
) as fin
where dc = 2
```

</details>


🔴
🟠
🟢