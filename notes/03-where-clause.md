# 03 — WHERE Clause

## الفكرة

WHERE بتفلتر الصفوف حسب شرط؛ الصف يظهر فقط لو الشرط TRUE. ممكن نفلتر بعمود مش موجود في SELECT.

## الكود

عايزين أسماء العائلة للموظفين اللي اسمهم الأول Amr:

```sql
SELECT last_name
FROM employees
WHERE first_name = 'Amr'
ORDER BY id;
```

### النتيجة

| last_name |
| --- |
| Zayed |
| Abdelhady |

## معاملات المقارنة

| المعامل | المعنى |
| --- | --- |
| = | يساوي |
| <> أو != | لا يساوي |
| > | أكبر من |
| >= | أكبر من أو يساوي |
| < | أصغر من |
| <= | أصغر من أو يساوي |

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary > 5000
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 3 | Amr | 7000 |
| 4 | Mai | 10000 |
| 6 | Amr | 10000 |
| 8 | Maryam | 12000 |

5000 نفسها مش داخلة لأن الشرط أكبر من، مش أكبر من أو يساوي. الصفوف ذات NULL كمان مش داخلة؛ المقارنة فيها UNKNOWN.

## AND وOR وNOT

- AND: الشرطان لازم يكونوا TRUE.
- OR: يكفي واحد يكون TRUE.
- NOT: تنفي TRUE وFALSE، لكن UNKNOWN تفضل UNKNOWN.

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary >= 5000 AND salary <= 10000
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 2 | Rana | 5000 |
| 3 | Amr | 7000 |
| 4 | Mai | 10000 |
| 5 | Kamel | 5000 |
| 6 | Amr | 10000 |

### الأقواس وأولوية المنطق

```sql
SELECT id, first_name, salary
FROM employees
WHERE (first_name = 'Amr' OR first_name = 'Ahmed')
  AND salary >= 6000
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 3 | Amr | 7000 |
| 6 | Amr | 10000 |

الاسم لازم يكون Amr أوAhmed، وفي نفس الوقت المرتب 6000 أو أكثر. Ahmed Gamal مرتبه 4000، وAhmed Khedr مرتبه NULL، فالاثنان ما ظهروش.

من غير الأقواس، AND ليها أولوية عن OR. عشان تلاحظ الفرق على نفس البيانات، بدّل 6000 بـ8000: بالأقواس يظهر Amr صاحب id 6 فقط، ومن غيرها يظهر Amr صاحب id 3 كمان.

الأولوية: NOT ثم AND ثم OR. دي أولوية فهم التعبير، مش ضمان لترتيب تنفيذ الشروط فعليًا.

## أخطاء شائعة

- ما تكتبش `first_name = 'Amr' OR 'Ahmed'`؛ اكتب شرطًا كاملًا لكل طرف أو استخدم IN.
- للمساواة `=` مش `==`.
- النصوص بين single quotes، والأرقام هنا من غير quotes.
- في الإعدادات المعتادة مقارنة النصوص دي حساسة لحالة الأحرف؛ ما تفترضش إن Amr وamr نفس القيمة.

---

[الفهرس](../README.md) · [بيانات الأمثلة](00-sample-data.md) · [السابق](02-select-clause.md) · [التالي](04-in-and-between.md)
