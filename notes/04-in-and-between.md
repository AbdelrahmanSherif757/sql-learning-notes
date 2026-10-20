# 04 — IN وBETWEEN

## الفكرة

IN بتختصر مقارنة نفس التعبير بقيم متعددة. BETWEEN بتحدد نطاقًا شاملًا للطرفين. مش بديلين لكل استخدامات AND وOR.

## IN

```sql
SELECT id, first_name, last_name
FROM employees
WHERE first_name IN ('Amr', 'Ahmed')
ORDER BY id;
```

### النتيجة

| id | first_name | last_name |
| --- | --- | --- |
| 3 | Amr | Zayed |
| 6 | Amr | Abdelhady |
| 7 | Ahmed | Khedr |
| 10 | Ahmed | Gamal |

نفس النتيجة مع `first_name = 'Amr' OR first_name = 'Ahmed'`.

`NOT IN ('Amr', 'Ahmed')` تستبعد الاسمين؛ تظهر الأرقام 1 و2 و4 و5 و8 و9.

## BETWEEN

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary BETWEEN 1000 AND 5000
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 1 | Mohamed | 2000 |
| 2 | Rana | 5000 |
| 5 | Kamel | 5000 |
| 10 | Ahmed | 4000 |

الشرط مكافئ لـ `salary >= 1000 AND salary <= 5000`. الحدّان داخل النطاق، حتى لو بياناتنا مفيهاش موظف مرتبه 1000.

`NOT BETWEEN 1000 AND 5000` ترجع الأرقام 3 و4 و6 و8، لكن لا تختار NULL.

## NULL داخل القوائم

```sql
SELECT id, first_name
FROM employees
WHERE first_name NOT IN ('Amr', NULL)
ORDER BY id;
```

### النتيجة

**ولا صف.**

Amr مرفوض لأنه مطابق؛ باقي الأسماء نتيجتها UNKNOWN بسبب NULL. عشان كده ما تضيفش NULL لقائمة NOT IN وتتوقع إنها تستبعد القيم المفقودة بالطريقة العادية.

`salary IN (5000, NULL)` مش بتختار المرتبات المفقودة. لو عايز 5000 أوNULL:

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary = 5000 OR salary IS NULL
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 2 | Rana | 5000 |
| 5 | Kamel | 5000 |
| 7 | Ahmed | NULL |
| 9 | Batoul | NULL |

## أخطاء شائعة

- BETWEEN بتستخدم AND بين الحدّين، مش فاصلة.
- حط الحد الأصغر الأول؛ BETWEEN العادية مش بتبدّل الحدّين تلقائيًا.
- IN بتطابق قيم كاملة، مش جزء من النص.
- في نطاقات timestamp، نهاية اليوم مش هي بداية اليوم نفسه؛ لاحقًا هنستخدم بداية اليوم شاملة وبداية اليوم التالي غير شاملة.

---

[الفهرس](../README.md) · [بيانات الأمثلة](00-sample-data.md) · [السابق](03-where-clause.md) · [التالي](05-nulls-and-three-valued-logic.md)
