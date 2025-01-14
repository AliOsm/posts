---
date: 2024-12-27
day: الجمعة
tags: [docker, devcontainers]
---

"بس هو شغّال على جهازي 🤔"

هذه من المشاكل اللي بتواجه الفِرق البرمجية في الشركات الصغيرة والكبيرة على حدٍّ سواء، وهي أن المشروع شغّال عندك ومش شغّال عند زميلك.

من سنة ونص تقريبًا تعرّفت على الـ DevContainers، وهو أمر لو تعلمون عظيم 🚀

أولا وقبل ما نتعرّف على الـ DevContainers، انت محتاج تفهم ولو شوي شو هو Docker، وهذا خارج نطاق هذا المنشور، ولكن ببساطة مُخِلَّه ممكن تعتبر Docker شيء يسمحلك بتشغيل نظام تشغيل مُصغّر داخل جهازك.

الـ DevContainer هي عبارة عن Docker image تستخدمها لتطوير مشاريعك على جهازك وتسمحلك بإعادة بنائها وتشغيلها على أكثر من جهاز، بحيث أن كل أعضاء الفريق يكون عندهم نفس بيئة التطوير، بنفس إصدار لغة البرمجة والخدمات الإضافية كقاعدة البيانات وإضافات وإعدادات المحرر.

للبدء في استخدام الـ DevContainers، تأكد أن عندك Docker على جهازك ثم افتح محرر VSCode وتأكد أن إضافة Dev Containers موجودة عندك، بعد ذلك محتاج تعمل مجلد باسم devcontainer. داخل مشروعك، هذا المجلد سيحتوي على كل ما يتعلق بالـ DevContainer في مشروعك.

داخل المجلد ممكن تعمل أكثر من ملف ومجلد لأكثر من وظيفة، ولكن الملفات الأساسية بالنسبة لي في أي مشروع هي 4:

- devcontainer.json
- docker-compose.yml
- Dockerfile
- setup.sh

الأول يحتوي على إعدادات بيئة التطوير الخاصة بك وهذا مثال عليه:  
https://github.com/ieasybooks/tafrigh/blob/main/.devcontainer/devcontainer.json

وهي بيئة تطوير برنامج تفريغ، ببساطة الملف يقوم بتجهيز بيئة العمل ببرمجية FFmpeg، محرر vim، لغة البرمجة Python إصدار 3.12 و Zsh مع إضافة OhMyZsh. هذا فيما يتعلق ببيئة التطوير من ناحية البرمجيات، من ناحية إضافات المحرر فالـ DevContainer تقوم بتثبيت 8 إضافات منها GitBlame وبعض الإضافات الخاصة بلغة Python.

في نفس هذا الملف devcontainer.json يتم استدعاء ملف docker-compose.yml لبناء الـ Docker image وملف setup.sh.

داخل docker-compose.yml ممكن تعريف الإضافات اللي محتاجها في مشروعك زي قاعدة البيانات ومحرك البحث، وهذا الملف مثال عليه:
https://github.com/AliOsm/wisal/blob/main/.devcontainer/docker-compose.yml  
وهو يقوم بتجهيز محرك البحث MeiliSearch وكذلك Redis.

أما ملف setup.sh مهمته تشغيل بعض الأوامر بعد الانتهاء من تجهيز بيئة العمل بالكامل، على سبيل المثال تشغيل أمر yarn install لتثبيت المكتبات الخاص بتطوير المشروع، وهذا مثال عليه:  
https://github.com/ieasybooks/tafrigh/blob/main/.devcontainer/setup.sh

أخيرا ملف Dockerfile ويتم استدعاءه من ملف docker-compose.yml وداخله يتم تحديد الـ Docker image الأساسية المُراد استخدامها في التطوير مع إمكانية تخصيصها بأريحية أكبر، وهذا مثال عليه:  
https://github.com/AliOsm/wisal/blob/main/.devcontainer/Dockerfile

وفيه يتم تحديد ghcr.io/rails/devcontainer/images/ruby:3.3.6 كـ Docker image أساسية، وتثبيت برمجية RustyWind الخاصة بمكتبة TailwindCSS.

بعد تجهيز DevContainer لمشروعك، ممكن كل عضو في الفريق يبنيها عنده بدون مشاكل، وممكن تشغيل المشروع على GitHub Codespaces على المتصفح كذلك من أي جهاز.

أخيرا، DevContainers مش لازم تستخدم مع VSCode فقط، ممكن تستخدمها مع محررات أخرى، ويوجد بدائل لها مثل موقع GitPod وبرنامج Flox.

والسلام عليكم 👋🏻
