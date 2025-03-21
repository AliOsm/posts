---
date: 2025-01-20
day: الاثنين
tags: []
---

إذا كنت تعمل في شركة GitHub، لا تقرأ من فضلك 😅

تحتوي منصة باحث على أكثر من 380 ألف مادة والعدد في ازدياد، بين فتاوى ودروس ومحاضرات وبرامج تلفزيونية لأكثر من 175 عالم وشيخ وداعية. الملفات الصوتية غير المرئية MP3 الخاصة بهذه المواد يصل حجمها لأكثر من 8TB والحجم يزداد يوما بعد يوم.

منذ اليوم الأول، قررت قرارين:
- تضمين المواد من منصة YouTube مباشرة في باحث
- الاحتفاظ بنسخة صوتية من أي مادة تُضاف إلى باحث

ولكن بعد فترة بدأت المشاكل تظهر. YouTube "لا يحب" بعض المواد الموجودة عنده ويحذفها ويُعيد الناس نشرها وهكذا. مثال ذلك مواد الشيخ عبدالعزيز الطريفي والمهندس أيمن عبدالرحيم فرّج الله عنهما.

فأصبحت المواد على باحث تُعرض كنص بدون مادة مرئية أو مسموعة يُستفاد منها استفادة حقيقية، وكنت أفكر دائما: "أين يمكن أن أرفع المواد الصوتية بدون تكلفة وأعرضها على منصة باحث مرة أخرى؟"، بما أن المواد موجودة عندي في الأساس.

أحد الخيارات كان موقع archive.org، ولكن هو أيضًا عليه بعض القيود وقد تُحذف منه المواد، غير أن الموقع نفسه رُفعت عليه العديد من القضايا. بعد تفكير لأيام، تذكرت GitHub (وقت الـ 😂).

جرّبت رفع ملف صوتيٍّ على GitHub وتضمينه في صفحة HTML ونجح الأمر، ثم حاولت التحكّم بمُشغّل المادة نفسه من خلال JavaScript لتحديد المكان الذي يجب أن يبدأ التشغيل منه وغيرها من الأمور ونجح الأمر كذلك.

بعد ذلك غصتُ قليلا في قيود GitHub نفسه فيما يتعلق بحجم الملفات وحجم المستودعات ككل. فكان أكبر حجم للملفات يمكن رفعه هو 100MB ولكن من الأفضل أن لا يتجاوز 50MB، وحجم المستودع يمكن أن يصل إلى 5GB ومن الأفضل أن لا يتجاوز 2GB.

بناءً على ذلك، قررت إنشاء حسابٍ جديدٍ على GitHub باسم baheth-platform وكتبت بعض الـ Bash Scripts التي تقوم بضغط الصوتيات وترفعها إلى الحساب الجديد بشكل تلقائي من خلال إنشاء مستودع لكل قائمة تشغيل تُحذف من YouTube.

أعدت رفع 80 قائمة تشغيل تخص الشيخ عبدالعزيز الطريفي والمهندس أيمن عبدالرحيم ثم عدّلت منصة باحث لأستطيع تغيير مصدر قوائم التشغيل بسهولة من YouTube إلى GitHub والحمدلله نجحت الفكرة.

هل ما قمت به هو الأفضل والأسلم؟ بالتأكيد لا! ولكنه يُلبّي احتياجاتي ويحافظ على تكاليف شبه صفريّة للمنصة مما يضمن دوامها لأكبر فترة ممكنة، ولكن بكل تأكيد هذا ليس حلًّا لمشاريع ربحية مستدامة تقوم على تقديم خدمات مستقرة للمستخدمين.

يمكنك تجربة هذه القوائم من خلال صفحة الشيخ عبدالعزيز الطريفي على منصة باحث:  
https://baheth.ieasybooks.com/speakers/عبدالعزيز-الطريفي

أو من صفحة المهندس أيمن عبدالرحيم:  
https://baheth.ieasybooks.com/speakers/أيمن-عبدالرحيم

وهذا رابط حساب المنصة على GitHub لمن أحب الاطلاع:  
https://github.com/baheth-platform?tab=repositories

وأخيرا، أرجو عدم التبليغ عن الحساب في GitHub 😅، والسلام عليكم 👋🏻
