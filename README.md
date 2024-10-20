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
Найти максимальный возраст среди студентов, учащихся в 10 классе [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/46)

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

🔴
🟠
🟢