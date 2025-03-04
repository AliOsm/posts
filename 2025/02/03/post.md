---
date: 2025-02-03
day: الاثنين
tags: [ruby, ruby-on-rails]
---

لغة Ruby واستهلاك الذاكرة 😅

مشروع منصة باحث كان أول مشروعٍ كبيرٍ لي أكتبه بإطار عمل Ruby on Rails بعد سنوات من استخدامه في مشاريع مختلفة صغيرة أخرى.

بعد إطلاق منصة باحث، كنت مهتما بمتابعة استهلاكها للمعالج والذاكرة وتحسين الأداء، ومن الملاحظات التي كنت ألاحظها بشدة أن استهلاك الذاكرة يبدأ صغيرًا على الخادم ثم يزداد مع مرور الوقت، فقد يبدأ بـ 1.5GB ويصل إلى 20GB بعد أسابيع من تشغيل المنصة.

فكنت أُعيد نشر المنصة (Re-deploy) على فترات متباعدة لإعادة الذاكرة إلى نظام التشغيل وتخفيف الضغط عن الخادم، ولكن لماذا كان يحدث هذا الأمر؟

لغة Ruby مكتوبة بلغة C، وهو ما يسمى CRuby أو MRI اختصارًا لـ Matz's Ruby Interpreter و Matz هو اسم مُنشئ اللغة، الياباني Yukihiro Matsumoto.

يوجد نُسخ أخرى من لغة Ruby مكتوبة بـ Java كـ JRuby و TruffleRuby، ولكن هذا ليس موضوعنا.

النسخة الأصلية تستخدم لغة C، مما يعني أنها تستخدم `malloc` بشكل افتراضي لحجز الذاكرة، وحسب فهمي البسيط المتواضع فطريقة عمل `malloc` ليست الأفضل، ويوجد العديد من البدائل لـ `malloc` مثل `jemalloc` و `tcmalloc` و `mimalloc`.

الجميل في هذه البدائل أنها بدائل مباشرة، لا تحتاج إلى الكثير من الإعدادات (على الأقل في حالة `jemalloc`)، فكل ما تحتاجه هو تثبيت مكتبة `libjemalloc2` على نظام تشغيل Linux ثم إضافة مسارها إلى متغير `LD_PRELOAD`، على سبيل المثال:

```bash
export LD_PRELOAD="$(echo /usr/lib/*/libjemalloc.so.2)"
```

بعد استبدال `malloc` بـ `jemalloc` في منصة باحث استقر استهلاك الذاكرة عند 4.8GB، أكثر من نصفها (2.5GB تحديدًا) مُستهلكة من قِبل نموذج الذكاء الاصطناعي المستخدم في المنصة.

بكلمات أخرى، استقر استهلاك الذاكرة عند 2.3GB، وهذا بعد أشهر من تشغيل المنصة دون إعادة نشرها.

الخبر الجميل أنه وبداية من Rails 7.2 هذه الإعدادات تأتي جاهزةً مع المشروع من ناحية تثبيت `jemalloc` على الـ Docker image الخاصة بالمشروع، وكذلك استخدامه في `docker-entrypoint`.

يمكنك قراءة هذه المقالة في المقارنة بين `malloc` وبدائلها:  
https://lf-hyperledger.atlassian.net/wiki/spaces/BESU/pages/22156632/Reduce+Memory+usage+by+choosing+a+different+low+level+allocator

والسلام عليكم 👋🏻
