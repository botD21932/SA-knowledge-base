**Общее табличное выражение (CTE)** — это временный результат выполнения SQL-выражения, который можно использовать в другом SQL-выражении ([[Реляционные БД]]). CTE позволяет упрощать сложные SQL-запросы, разбивая их на составные части.

**Синтаксис:**
```postgresql
WITH <CTE_name> (<column_list>) AS (
<CTE_query_definition>
)
<statement>;
```

**Синтаксис рекурсивного запроса:**
```postgresql
WITH RECURSIVE <CTE_name> AS(
    <CTE_query_definition> -- нерекурсивная часть
    UNION [ALL]
    <CTE_query definion> -- рекурсивная часть
```

PostgreSQL выполняет рекурсивное CTE в следующей последовательности:
1) Выполняет нерекурсивную часть, чтобы создать базовый набор результатов (R0)
2) Выполняет рекурсивную часть с Ri в качестве входных данных, чтобы вернуть результирующий набор Ri+1 в качестве выходных данных
3) Повторяет шаг 2, пока не будет возвращен пустой результат
4) Возвращает окончательный результат, который является итогом выполнения UNION или UNION ALL над наборами результатов R0, R1,…​Rn

При работе с рекурсивными запросами важно убедиться, что рекурсивная часть запроса в конечном итоге не возвращает ни одного элемента, иначе запрос уйдёт в бесконечный цикл. Вы можете использовать фразу CYCLE для обнаружения бесконечных циклов.

**Синтаксис:**
```postgresql
WITH RECURSIVE subordinates(employee_id, manager_id, full_name) AS (
    SELECT employee_id, manager_id, full_name
    FROM employees WHERE employee_id=2
    UNION
        SELECT e.employee_id, e.manager_id, e.full_name
        FROM employees e
    INNER JOIN subordinates s ON s.employee_id = e.manager_id
)  CYCLE employee_id SET is_cycle USING path
SELECT * FROM subordinates;
```

