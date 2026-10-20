# SQL Learning Notes 📚

ملاحظاتي وتطبيقاتي أثناء تعلّم **SQL باستخدام PostgreSQL**، بشرح عربي بسيط وأمثلة توضح النتيجة وسببها.

هدفي أوثّق فهمي وأراجع بسهولة، وأبني أساس كويس في رحلتي لتعلّم **Data Engineering**.

## ابدأ من هنا

- اقرأ [المقدمة](notes/01-introduction.md) لو دي أول مرة تتعامل مع قواعد البيانات.
- افتح [بيانات الأمثلة المشتركة](notes/00-sample-data.md) قبل تطبيق الاستعلامات. بتطابق الصفوف العشرة في صور جدول مذاكرتي، وفيها كود تجهيز اختياري داخل Markdown.
- اتبع الفهرس بالترتيب. كل درس فيه فكرة وأمثلة ونتائج وملاحظات وأخطاء شائعة، وروابط للسابق والتالي.

## فهرس الملاحظات

| الترتيب | الموضوع | هتتعلم إيه؟ |
| --- | --- | --- |
| 01 | [Introduction to Databases and SQL](notes/01-introduction.md) | قواعد البيانات، SQL، RDBMS وCRUD |
| 02 | [SELECT Clause](notes/02-select-clause.md) | اختيار الأعمدة، aliases والحسابات |
| 03 | [WHERE Clause](notes/03-where-clause.md) | فلترة الصفوف والمقارنات وAND / OR / NOT |
| 04 | [IN and BETWEEN](notes/04-in-and-between.md) | القوائم والنطاقات الشاملة |
| 05 | [NULL and Three-valued Logic](notes/05-nulls-and-three-valued-logic.md) | القيم المفقودة وTRUE / FALSE / UNKNOWN |
| 06 | [Logical Processing Order](notes/06-logical-processing-order.md) | الترتيب المنطقي وخطة التنفيذ |
| 07 | [Relationships](notes/07-relationships.md) | المفاتيح وأنواع العلاقات والجدول الوسيط |

## أسلوب الملاحظات

- الشرح بالعربي، والمصطلحات وأسماء الملفات بالإنجليزي.
- أمثلة الاستعلامات مبنية على صفوف جدولي العشرة؛ النتائج تفترض عدم تعديلها.
- اسم الجدول `employees` افتراضي لأن الصور لا تعرض اسمه.
- أمثلة العلاقات مستقلة؛ الصور لا تعرض جداول مرتبطة أو قيودًا أو أنواع أعمدة.
- الكود داخل ملفات Markdown، من غير ملفات SQL منفصلة أو تمارين.
- أسماء الجداول والأعمدة بحروف صغيرة و`snake_case`.
- أي مثال غير صحيح بغرض توضيح خطأ مميّز بوضوح.

## تطوري في التعلّم

الموضوعات الحالية تصل إلى **Relationships**. سأضيف ملاحظات جديدة وأحسّن الأمثلة كلما تقدّمت في الدراسة.

هذه ملاحظات تعلّم شخصية، والمصادر الرسمية مرجع للتأكد من التفاصيل. لم يُحدّد إصدار PostgreSQL المثبّت لدي؛ الأمثلة تستخدم خصائص أساسية مستقرة.

## مراجع PostgreSQL الرسمية

- [SELECT ومعالجة الاستعلام](https://www.postgresql.org/docs/current/sql-select.html)
- [المقارنات وBETWEEN واختبارات NULL](https://www.postgresql.org/docs/current/functions-comparison.html)
- [المنطق ثلاثي القيم](https://www.postgresql.org/docs/current/functions-logical.html)
- [IN وNOT IN](https://www.postgresql.org/docs/current/functions-comparisons.html)
- [الأسماء وعلامات التنصيص](https://www.postgresql.org/docs/current/sql-syntax-lexical.html)
- [العمليات الحسابية](https://www.postgresql.org/docs/current/functions-math.html)
- [القيود والمفاتيح والعلاقات](https://www.postgresql.org/docs/current/ddl-constraints.html)
- [نظرة على آلية عمل PostgreSQL](https://www.postgresql.org/docs/current/overview.html)
