# SQL_academy_solutions

В этом репозитории содержатся все мои запросы по SQL, во время выполнения тренажера на сайте : **[SQL Academy]()**

42.  Сколько времени обучающийся будет находиться в школе, учась со 2-ой по 4-ую пару? [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/42)

<details>

  <summary>Решение</summary>

```sql
select TIMEDIFF(
(select end_pair from Timepair where id = 4),
(select start_pair from Timepair where id = 2)
) as time


```

</details>

43. Выведите все фамилии учителей, которые преподают Физкультуру (Физическую Культуру). Отсортировать фамилии в алфавитном порядке [(ссылка на задание)](https://sql-academy.org/en/trainer/tasks/43)

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
