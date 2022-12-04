---
layout: post
title: Viewing the Changes Across Commits
date: 2022-11-08 17:34:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

اگر بخواهیم بدونیم که چه تغییراتی در کامیت‌ها رخ داده می‌تونیم از دستورِ `diff` استفاده کنیم. در بخشِ قبلی یاد گرفتیم که چطور با این دستور، تغییراتِ staged و unstaged رو ببینیم.

حالا با همین دستور می‌خواهیم تغییراتِ بینِ دو commit رو ببینیم.

```
git diff HEAD~2 HEAD
```

 برای اینکه تغییرِ فایلی رو در بینِ دو کامیت مشخص ببینیم اسمِ فایل‌ یا فایل‌ها رو در انتهایِ دستورِ بالا می‌نویسیم.

```
git diff HEAD~2 HEAD audience.txt
```

مثلِ دستورِ log در این دستور هم آپشن‌هایِ `name-only--` و `name-status--` رو داریم.

```
git diff HEAD~2 HEAD --name-only
git diff HEAD~2 HEAD --name-status
```
