# 02 — SELECT Clause

## الفكرة

`SELECT` بتحدد الأعمدة أو التعبيرات اللي عايز تعرضها. `FROM` بتحدد المصدر؛ في أمثلتنا بنفترض إن الجدول اسمه `employees`.

## اختيار أعمدة محددة

```sql
SELECT first_name, salary
FROM employees
ORDER BY id;
```

### النتيجة

| first_name | salary |
| --- | --- |
| Mohamed | 2000 |
| Rana | 5000 |
| Amr | 7000 |
| Mai | 10000 |
| Kamel | 5000 |
| Amr | 10000 |
| Ahmed | NULL |
| Maryam | 12000 |
| Batoul | NULL |
| Ahmed | 4000 |

اختيار الأعمدة مش بيستبعد صفوف؛ الفلترة وظيفة WHERE. الفاصلة بتفصل بين الأعمدة.

## Aliasing — اسم بديل

```sql
SELECT first_name AS employee_name
FROM employees
ORDER BY id;
```

### النتيجة

| employee_name |
| --- |
| Mohamed |
| Rana |
| Amr |
| Mai |
| Kamel |
| Amr |
| Ahmed |
| Maryam |
| Batoul |
| Ahmed |

الاسم البديل عنوان في النتيجة، مش تغيير لاسم العمود الأصلي.

لو الاسم فيه مسافات، في PostgreSQL بنستخدم double quotes:

```sql
SELECT first_name AS "First Name"
FROM employees
ORDER BY id;
```

نفس الأسماء السابقة تحت عنوان `First Name`.

| الكتابة | معناها |
| --- | --- |
| `'Amr'` | قيمة نصية — single quotes |
| `"First Name"` | اسم عمود أو alias — double quotes |
| `first_name` | اسم عمود بسيط |

الأسماء غير المحاطة بـdouble quotes بتتحول لحروف صغيرة في PostgreSQL. بنفضّل أسماء صغيرة وsnake_case.

## Basic Arithmetic Operations

| الرمز | العملية |
| --- | --- |
| + | جمع |
| - | طرح |
| * | ضرب |
| / | قسمة |

مثال: المرتب بعد زيادة 15%.

```sql
SELECT id, first_name, salary, salary * 1.15 AS salary_after_bonus
FROM employees
ORDER BY id;
```

### النتيجة

| id | first_name | salary | salary_after_bonus |
| --- | --- | --- | --- |
| 1 | Mohamed | 2000 | 2300.00 |
| 2 | Rana | 5000 | 5750.00 |
| 3 | Amr | 7000 | 8050.00 |
| 4 | Mai | 10000 | 11500.00 |
| 5 | Kamel | 5000 | 5750.00 |
| 6 | Amr | 10000 | 11500.00 |
| 7 | Ahmed | NULL | NULL |
| 8 | Maryam | 12000 | 13800.00 |
| 9 | Batoul | NULL | NULL |
| 10 | Ahmed | 4000 | 4600.00 |

بنضرب في `1.15` عشان 100% من المرتب + 15% زيادة. قيمة الزيادة وحدها `salary * 0.15`. الحساب مش بيعدّل البيانات المتخزنة. العمليات الحسابية دي مع NULL بترجع NULL.

### القسمة في PostgreSQL

```sql
SELECT 5 / 2 AS integer_result, 5.0 / 2 AS decimal_result;
```

الناتج 2 و2.5؛ قسمة عددين صحيحين بتشيل الجزء الكسري. SELECT ممكن تشتغل من غير FROM لما مفيش جدول محتاجينه.

## SELECT *

```sql
SELECT *
FROM employees
ORDER BY id;
```

### النتيجة

| id | first_name | last_name | salary |
| --- | --- | --- | --- |
| 1 | Mohamed | Saad | 2000 |
| 2 | Rana | Elsayed | 5000 |
| 3 | Amr | Zayed | 7000 |
| 4 | Mai | Radwan | 10000 |
| 5 | Kamel | Mohamed | 5000 |
| 6 | Amr | Abdelhady | 10000 |
| 7 | Ahmed | Khedr | NULL |
| 8 | Maryam | Karim | 12000 |
| 9 | Batoul | Said | NULL |
| 10 | Ahmed | Gamal | 4000 |

النجمة بتختار كل الأعمدة. مفيدة للاستكشاف؛ لو محتاج أعمدة محددة اكتب أسماءها.

## أخطاء شائعة

- بعد FROM بنكتب اسم الجدول، مش اسم قاعدة البيانات وحده.
- `first-name` مش `first_name`؛ الشرطة ممكن تتفهم كطرح.
- `SELECT *` مش معناها إزالة التكرار.
- مش كل SQL بتبدأ بـSELECT؛ فيه INSERT وUPDATE وغيرها.

---

[الفهرس](../README.md) · [بيانات الأمثلة](00-sample-data.md) · [السابق](01-introduction.md) · [التالي](03-where-clause.md)
