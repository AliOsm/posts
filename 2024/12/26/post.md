---
date: 2024-12-26
day: الخميس
tags: [ruby]
---

البارحة أُطلق الإصدار 3.4 من لغة Ruby، وقررت أبدأ نشر مجموعة من المنشورات عن اللغة بشكل عام وإطار العمل Ruby on Rails، مش هدفي أقنعك تستخدم Ruby أو Rails، ولكن هدفي أعرّفك بلغة وإطار عمل مُلهمين ومفيدين بشكل كبير 😎

اللي شدني في آخر تحديث بشكل أساسي أمرين:

في Ruby ممكن تكتب التالي:
```ruby
squares = [1, 2, 3].map { |element| element * element }
```

ببساطة الكود يقوم بتربيع كل قيمة من قيَم المصفوفة، في هذه الحالة تقدر تستغني عن اسم المُتغيّر `element` وتكتب الكود كالتالي:
```ruby
squares = [1, 2, 3].map { _1 * _1 }
```

طبعا زي ما انت متوقع، `1_` الموجودة بين الأقواس تُعبّر عن أول عنصر من عناصر الحَلقة، وممكن تستخدم `2_` و `3_` وهكذا، ولكن استخدام أكثر من `1_` مش لطيف في الكود.

في الإصدار الجديد ممكن تكتب `it` مكان `1_` واللي شكلها ألطف بمراحل:
```ruby
squares = [1, 2, 3].map { it * it }
```

هذا الشيء الأول، الثاني هو تحسينات على YJIT واللي هو عبارة عن just in time compiler للغة Ruby مكتوب بلغة Rust واللي ممكن يعطيك زيادة في السرعة تصل إلى 90% مقابل استهلاك إضافي للذاكرة يُقدّر بـ 15-20%. التحسينات تتضمن سرعة أكثر واستهلاك ذاكرة أقل حسب الـ benchmarks اللي ممكن تطّلع عليها من هنا:
https://speed.yjit.org

ومن الأشياء اللطيفة اللي كانت موجودة في الـ release notes هي تحسينات على دالة `Kernel#Float` (نعم دالة مش Class 😁) بحيث اصبح بإمكانها استقبال الرقم على هيئة نص بدون كتابة الجزء العشري منه، فعلى سبيل المثال ممكن تكتب:
```ruby
Float("1.0")
```

أو تكتب:
```ruby
Float("1.")
```

والاثنين نفس النتيجة، الاهتمام بالتفاصيل لطيف أحيانًا 😂

أخيرًا، شو ممكن أعمل بلغة Ruby؟ ممكن تبني موقع زي باحث:
https://baheth.ieasybooks.com
وأكثر من ذلك بكثير زي ما حنشوف في باقي المنشورات مستقبلا✌

ولمن سيسأل لماذا اسمه YJIT، فهو اختصار لـ Yet Another Ruby JIT، السلام عليكم 👋🏻