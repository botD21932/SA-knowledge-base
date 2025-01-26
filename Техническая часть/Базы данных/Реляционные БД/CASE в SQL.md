Оператор **CASE** позволяет выполнять условные проверки и возвращать значения на основе заданных условий в SQL ([[Реляционные БД]]).

**Синтаксис:**
```postgresql
CASE 
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE default_result
END
```

**Пример применения с агрегирующей функцией:**
```postgresql
SELECT
  CASE 
    WHEN age < 20 THEN 'Молодежь'
    WHEN age < 60 THEN 'Взрослые'
    ELSE 'Пожилые'
  END as ВозрастнаяГруппа,
  COUNT(*) as Количество
FROM
  граждане
GROUP BY
  ВозрастнаяГруппа;
```
