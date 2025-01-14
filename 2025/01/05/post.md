---
date: 2025-01-05
day: الأحد
tags: [ruby-on-rails, pwa, hotwire, native, android, ios]
---

تطبيقات الهاتف وعبء تطويرها 😪

من الأشياء اللي كانت مطلوبة بكثرة من مستخدمي منصة باحث هي تطبيقات الهاتف للـ Android والـ iOS، وبما اني ما اشتغلت تطبيقات في حياتي إلا مشاريع الجامعة وما عندي ميزانية أجيب مطوّر يشتغلها وما عندي صديق يشتغل التطبيقات (وأنا كسول وما بدي أعمل APIs 😂) فكنت دائما أبتعد عن هذا الأمر.

مع بداية المنصة وفّرت PWA (زي ما هو الوضع في  #قبيلة  حاليا) ولكن المستخدم العادي ما بيعرف شو هو الـ PWA ولا كيف يثبته على الهاتف، وهذا من أكبر أسباب عدم انتشار الـ PWAs خارج نطاق المنتجات التقنية على حد علمي، وحتى المنتجات التقنية في الغالب تبدأ بـ PWA ثم تنتقل إلى تطبيق هاتف متكامل زي ما صار مع Linear مثلا.

إلى أن أتى الله بالفرَج على يد Rails 😎

تاريخيًّا، Rails فيها ميزة شغالة بشكل تلقائي اسمها Turbolinks، مهمتها انك بمجرد ما تكبس على رابط هي تجيب محتويات الصفحة اللي انت طلبتها وتستبدل الـ Body الخاص بالصفحة الحالية بالـ Body الجديد وتدمج الـ Head الحالي بالـ Head الجديد، فانت بتاخذ تأثير Single Page Application مجانا.

مع إطلاق الإصدار السابع من Rails، أُلغي الدعم عن Turbolinks في مقابل إصدار مكتبة Turbo واللي فيها نفس مميزات Turbolinks مع أشياء إضافية زي ميزة Prefetch بحيث ان المستخدم بمجرد ما يعمل Hover على رابط، Turbo بتعمله Prefetch ولما يضغط عليه، الصفحة بتتغير مباشرة بدون ما ينتظر، وهذا بيعطي إيحاء أن الموقع يستجيب بسرعة.

مكتبة Turbo كانت واحدة من 3 مكتبات أُطلقت تباعا مع الإصدار السابع من Rails وهي Turbo و Stimulus و Native. بطلة المنشور هي مكتبة Native واللي بناء على مميزات Turbo بتسمحلك تبني تطبيقات هجينة أو Hybrid بين الـ WebView والـ Native. بناء على مكتبة Native عملت تطبيقات باحث بأقل القليل من المعرفة في برمجتها واللي ممكن توصلها من هون:
- Android: https://bit.ly/baheth-google-play
- iOS: https://bit.ly/baheth-app-store

المميز إني مش محتاج أفتح APIs وكل التعديلات اللي بعملها على المنصة بتوصل للمستخدمين بدون ما أحتاج أرفع تحديث على المتاجر وقادر أدمج مميزات Native في التطبيقات زي الزر اللي بيفتح القائمة الجانبية أو أفتح نوافذ سفلية أو Bottom Sheets.

الزر على سبيل المثال هو Native ولكن بيفتح القائمة الموجودة في الـ WebView. طريقة الدمج بين المكونات الـ Native والـ WebView سهلة وما فيها تعقيدات كبيرة، ممكن تقرأ عنها من هون:  
https://native.hotwired.dev/ios/bridge-components

بهذه الطريقة انت ممكن تطلع بتطبيق لشركتك أو مشروعك الشخصي بدون ما تتكلف تكاليف إضافية أو تجيب مطورين للهاتف ثم مع الوقت ممكن تتحول من الـ Hybrid إلى Native بالكامل، خصوصا وأن المكتبة نفسها تدعم الانتقال من الصفحات الـ Native إلى الـ WebView والعكس.

إذا حاب تشوف تطبيقات ثانية بتشتغل بنفس التقنية ممكن تشوف هذا الموقع:  
https://turbonative.directory

والسلام عليكم 👋🏻