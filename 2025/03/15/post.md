---
date: 2025-03-15
day: السبت
tags: []
---

احتجت في الأيام الماضية إلى استخدام أكثر من بريدٍ إلكترونيٍّ مع Git حسب المشروع الذي أعمل عليه، فبدأت البحث في الأمر للمرة الثانية في حياتي، لأن المرة الأولى بائت بالفشل 😂 فاكتشفت أن الأمر سهل، لكنه يحتاج إلى فهمٍ لما تقرأ 😁

ينقسم الأمر إلى خطوتين، إنشاء مفتاح SSH جديد وتخصيص البريد الإلكتروني واسم المستخدم الذي تريد استخدامهما مع المستودعات المختلفة.

نفّذ الأمر التالي لإنشاء مفتاح SSH جديد:
```bash
ssh-keygen -t ed25519 -C "email@example.com"
```

بعد ذلك، ستحتاج إلى إضافة المفتاح الجديد إلى GitHub (إذا كنت تستخدمه) وستحتاج إلى تنفيذ الأمر التالي لإضافة المفتاح الجديد إلى SSH:
```bash
ssh-add ~/.ssh/id_ed25519_example
```

ثم أضف المحتوى التالي إلى ملف `config` داخل مجلد `ssh./~` لتتمكن من استخدام المفتاح الجديد مع Git:
```
Host github-example
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_example
```

وأخيرا، عند إضافتك للـ Remote إلى مستودعك، يجب أن تستخدم نفس اسم الـ Host الذي وضعته في ملف `config` قبل قليل (في حالتنا الـ Host هو `github-example`):
```bash
git remote add origin git@github-example:username/repo.git
```

لتنفيذ الخطوة الثانية، وهي تخصيص البريد الإلكتروني واسم المستخدم حسب المستودع، نحتاج إلى تعديل ملف `gitconfig./~`.

داخل هذا الملف ستجد المعلومات الافتراضية الخاصة بك في Git كالتالي:
```
[user]
  name = Ali Hamdi Ali Fadel
  email = aliosm1997@gmail.com
```

لنفترض أن المستودعات الخاصة بالبريد الإلكتروني الجديد موجودة داخل مجلد واحد على حاسبك وهو `Users/aliosm/Desktop/repositories/other_email/`، لتعديل البريد الإلكتروني واسم المستخدم لكل المستودعات الموجودة داخل هذا المجلد سنحتاج إلى إضافة الإعدادات التالية إلى الملف المذكور في الأعلى:
```
[includeIf "gitdir:/Users/aliosm/Desktop/repositories/other_email/"]
  path = /Users/aliosm/Desktop/repositories/other_email/.gitconfig
```

وأخيرا، ستحتاج إلى إنشاء ملف `gitconfig.` داخل مجلد `other_email` وتضع فيه بريدك الإلكتروني الثاني واسم مستخدم مختلف:
```
[user]
  name = Ali Hamdi Ali Fadel
  email = different@email.com
```

قد تبدو الخطوات كثيرة، لكن إذا طبقتها بالشكل الصحيح، سينجح الأمر وسترتاح من تداخل البريد الإلكتروني بين مشاريعك وحساباتك على Git و GitHub 😎

والسلام عليكم 👋🏻

ملاحظة: كل الأوامر ومحتويات الملفات موجودة في الصورة ومرتبة حسب ترتيب ظهورها في المنشور 😁
