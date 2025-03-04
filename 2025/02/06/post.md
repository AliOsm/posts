---
date: 2025-02-06
day: الخميس
tags: [database, ruby-on-rails]
---

البيانات الهرمية في قاعدة البيانات

أعمل حاليا على إضافة ميزة جديدة إلى منصة باحث (قريبًا 🚀) وتحتاج هذه الميزة إلى ترتيب البيانات هرميًّا، فكل صف من صفوف الجدول يُعبّر عن عنصرٍ وهذا العنصر قد يكون له ابن أو مجموعة أبناء، وهكذا إلى أن نحصل على شجرة من البيانات.

هذا التمثيل للبيانات مهم ومنتشر في حياتنا فيمكنك من خلاله تمثيل فئات المنتجات (مثلا: فئة البقالة تحتها منتجات الألبان ومنتجات اللحوم) أو تمثيل الموظفين في الشركة حسب أقسامهم (مثلا: قسم تكنولوجيا المعلومات تحته قسم الصيانة وقسم المشتريات).

كنت أظن الأمر سهلا ولا يوجد فيه الكثير من التعقيدات، مجرد جدول في قاعدة البيانات مع عمودٍ باسم `parent_id` من خلاله تعرف الأب لكل صف من صفوف الجدول، وإذا كان الصف بدون `parent_id`، فهذا يعني أنه جذر في هذه الشجرة، سهلة.

ولكن قبل البدء في التنفيذ قررت البحث والقراءة عن الأمر، فاكتشفت الخيارات الكثيرة المتاحة لك عند تمثيل هذا النوع من البيانات، ومنها الخيار المذكور في الفقرة السابقة والمسمى بـ "أب-ابن" (Parent-Child).

استخدام هذا النوع سهلٌ جدًّا في Ruby on Rails، تحتاج إلى إضافة العمود ثم تعريف العلاقة في الـ Model كما هو موضّح في الصورة. بهذه الطريقة يمكنك الوصول إلى أب أي عنصر من خلال دالة `parent` والوصول إلى أبناء أي عنصر من خلال دالة `children`.

هذا الخيار يُوّفر لك سرعة كبيرة في إضافة العناصر الجديدة، فأنت تحتاج إلى كتابة صفٍّ واحدٍ فقط، ولكن القراءة فيه تكون بطيئة، فإذا وُجد عنصر يبعد عن الجذر الخاص به بمسافة 5 عناصر، فستحتاج إلى 4 استعلامات على قاعدة البيانات لتصل إلى الجذر، لذلك يُنصح به إذا كان أطول مسارٍ في شجرة بياناتك لا يتعدَّى عنصرين أو ثلاثة عناصر كحد أقصى.

النوع الثاني يسمى المسار الملموس (Materialized Path)

في هذا النوع أنت تحتفظ بكل آباء العنصر إلى أن تصل إلى الجذر في كل صف من صفوف الجدول، فلا تحتاج إلى الكثير من الاستعلامات لتصل إلى جذر عنصرٍ مُعيّن لأنك تمتلك المسار كاملًا من العنصر إلى الجذر، ولكن الكتابة في هذا النوع مكلفة وحجم البيانات المُخزّنة أكبر.

يوجد مكتبة لـ Rails توفّر لك هذا النوع من التمثيل تسمى `ancestry`، يمكنك الاطلاع عليها من هنا:  
https://github.com/stefankroes/ancestry

النوع الأخير يسمى المجموعات المتداخلة (Nested Sets)

وهذا النوع أعقدهم، ولكنه يوفّر قراءة سريعة جدًّا لعناصر الشجرة. يعمل هذا النوع بمبدأ مُشابه لمبدأ عمل الـ Segment Tree، والتي شرحتها في هذا المقطع:  
https://www.youtube.com/live/U_sZY8WTX-Y

سريعًا، يستخدم هذا النوع 3 أعمدة وهي `level` و `left` و `right` لتمثيل مستوى العناصر في الشجرة وبداية ونهاية العناصر المُنتمية لكل عنصرٍ من عناصر الشجرة. باستخدام هذه الأعمدة يمكنك الاستعلام عن أبناء عنصر من العناصر بسرعة كبيرة، ولكن كسابقه، الكتابة فيه مكلفة.

يوجد مكتبة لـ Rails توفّر لك هذا النوع من التمثيل تسمى `awesome_nested_set`، يمكنك الاطلاع عليها من هنا:  
https://github.com/collectiveidea/awesome_nested_set

قررت الابتعاد عن الخيار الأول والأخير في باحث واستخدام الخيار الثاني، فالكتابة في حالتي قليلة والقراءة هي الأساس، ولا حاجة للتعقيد الإضافي من الخيار الأخير.

هل استخدمت أي نوع من هذه الأنواع سابقًا ؟.؟ وهل تعرف أنواعًا أخرى؟ شاركنا لنستفيد 😁

والسلام عليكم 👋🏻
