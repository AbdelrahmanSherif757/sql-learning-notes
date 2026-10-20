# 05 — NULL وThree-valued Logic

## الفكرة

NULL بتعبّر عن غياب قيمة: مش معروفة أو مش منطبقة حسب السياق. مش صفر، ومش النص الفاضي `''`، ومش النص `'NULL'`.

المقارنة العادية مع NULL نتيجتها UNKNOWN. منطق SQL ثلاثي: TRUE وFALSE وUNKNOWN. PostgreSQL بيمثّل UNKNOWN في تعبير Boolean بقيمة NULL.

## اختيار المرتبات المفقودة

```sql
SELECT id, first_name, last_name, salary
FROM employees
WHERE salary IS NULL
ORDER BY id;
```

### النتيجة

| id | first_name | last_name | salary |
| --- | --- | --- | --- |
| 7 | Ahmed | Khedr | NULL |
| 9 | Batoul | Said | NULL |

IS NULL بترجع TRUE أوFALSE. عكسها IS NOT NULL، ودي هنا هتختار 8 موظفين.

## ليه = NULL مش صح؟

| التعبير | النتيجة |
| --- | --- |
| `5000 = NULL` | UNKNOWN |
| `5000 <> NULL` | UNKNOWN |
| `NULL = NULL` | UNKNOWN |
| `NULL IS NULL` | TRUE |
| `5000 IS NULL` | FALSE |

`WHERE salary = NULL` مش هتختار الصفوف المفقودة؛ استخدم IS NULL.

## مثال الكراسة: مساوي أو غير مساوي

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary = 5000 OR salary <> 5000
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 1 | Mohamed | 2000 |
| 2 | Rana | 5000 |
| 3 | Amr | 7000 |
| 4 | Mai | 10000 |
| 5 | Kamel | 5000 |
| 6 | Amr | 10000 |
| 8 | Maryam | 12000 |
| 10 | Ahmed | 4000 |

ظهر 8 موظفين. Ahmed Khedr وBatoul Said ما ظهروش: UNKNOWN OR UNKNOWN تساوي UNKNOWN. WHERE بتحتفظ بـTRUE فقط؛ FALSE وUNKNOWN بيتستبعدوا، لكن مش معناهم واحد.

لإظهار كل الموظفين:

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary = 5000 OR salary <> 5000 OR salary IS NULL
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 1 | Mohamed | 2000 |
| 2 | Rana | 5000 |
| 3 | Amr | 7000 |
| 4 | Mai | 10000 |
| 5 | Kamel | 5000 |
| 6 | Amr | 10000 |
| 7 | Ahmed | NULL |
| 8 | Maryam | 12000 |
| 9 | Batoul | NULL |
| 10 | Ahmed | 4000 |

نفس نتيجة إزالة WHERE في المثال ده، فالشرط زائد لو المطلوب كل الصفوف.

## جدول المنطق

U معناها UNKNOWN:

| A | B | A AND B | A OR B |
| --- | --- | --- | --- |
| TRUE | TRUE | TRUE | TRUE |
| TRUE | FALSE | FALSE | TRUE |
| TRUE | U | U | TRUE |
| FALSE | TRUE | FALSE | TRUE |
| FALSE | FALSE | FALSE | FALSE |
| FALSE | U | FALSE | U |
| U | TRUE | U | TRUE |
| U | FALSE | FALSE | U |
| U | U | U | U |

| A | NOT A |
| --- | --- |
| TRUE | FALSE |
| FALSE | TRUE |
| U | U |

FALSE كفاية لرفض AND، وTRUE كفاية لقبول OR، حتى مع طرف UNKNOWN. دي قواعد نتائج، مش ترتيب تنفيذ.

## IS DISTINCT FROM — مقارنة تراعي NULL

```sql
SELECT id, first_name, salary
FROM employees
WHERE salary IS DISTINCT FROM 5000
ORDER BY id;
```

### النتيجة

| id | first_name | salary |
| --- | --- | --- |
| 1 | Mohamed | 2000 |
| 3 | Amr | 7000 |
| 4 | Mai | 10000 |
| 6 | Amr | 10000 |
| 7 | Ahmed | NULL |
| 8 | Maryam | 12000 |
| 9 | Batoul | NULL |
| 10 | Ahmed | 4000 |

بعكس `<> 5000`، الصفان ذوا المرتب NULL بيظهروا هنا. العامل ده بيعتبر NULL مساوية لـNULL ومختلفة عن القيم غير NULL. عكسه `IS NOT DISTINCT FROM`.

## أخطاء شائعة

- UNKNOWN نتيجة منطقية، مش اسم مرتب أو رقم خاص.
- NOT UNKNOWN تفضل UNKNOWN.
- NULL داخل NOT IN ممكن تمنع ظهور نتائج متوقعة.
- ما تستبدلش القيمة المفقودة بصفر من غير سبب؛ ده بيغيّر معناها.

---

[الفهرس](../README.md) · [بيانات الأمثلة](00-sample-data.md) · [السابق](04-in-and-between.md) · [التالي](06-logical-processing-order.md)
