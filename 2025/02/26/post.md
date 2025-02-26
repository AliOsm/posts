---
date: 2025-02-26
day: الأربعاء
tags: []
---

البارحة بدأت بتطوير مشروع صغير مُساعد لمنصة باحث، قد أُعلن عنه مستقبلًا، ولكن خلال التطوير احتجت للوصول إلى المُعالج الرسومي (GPU) من داخل Docker Container، والذي حاولت فعله مسبقًا ولم أنجح 😁

عدت للبحث في الأمر وكيفية تنفيذه بالشكل الصحيح، وهذه الخطوات التي نجحت معي:
- ثبّت Docker من خلال التوثيق الرسمي: https://docs.docker.com/engine/install/ubuntu
- اتّبع التوثيق الخاص بخطوات ما بعد التثبيت: https://docs.docker.com/engine/install/linux-postinstall
- والخطوة الأهم، استخدم Docker Images الداعمة للمُعالجات الرسومية المقدّمة من Nvidia: https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch

ملاحظة: حجم Docker Images الداعمة للمُعالجات الرسومية من Nvidia كبير، في حدود الـ 22GB، لذلك كن صبورًا 😅

بهذه الخطوات ستستطيع الوصول إلى المعالج الرسومي الموجود على حاسبك من داخل Docker Container، وإذا واجهت مشكلة شبيهة بهذه:

```
docker: Error response from daemon: unknown or invalid runtime name: nvidia
```

فراجع هذا المنشور من StackOverflow: https://stackoverflow.com/a/77342669

والسلام عليكم 👋🏻
