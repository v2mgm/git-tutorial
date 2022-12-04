---
layout: post
title: Finding Contributors Using Shortlog
date: 2022-11-08 18:43:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

بعضی اوقات لازمه که تمامی کسانی که در پروژ‌‌ه‌مون کمک کردن رو پیدا کنیم.

یه دستوری تویِ گیت همین کار رو می‌کنه.

```bash
git shortlog
```

خروجی‌ش:

```
Moshfegh Hamedani (13):
 Initial commit.
 Define the objectives.
 Define the audience.
 Write the first draft of initializing a repo.
 Include the warning about removing .git directory.
 Add a header to the page about initializing a repo.
 Include the command prompt in code sample.
 Add command line and GUI tools to the objectives.
 First draft of staging changes.
 Explain various ways to stage changes.
 Include the note about committing after staging the changes.
 Include the first section in TOC.
 Add header to all pages.
```

خروجیِ بالا اسمِ نویسنده و تعداد کامیت‌هاش و پیام‌هایِ کوتاه هر کامیت رو نشون می‌ده.

دستورِ `git shortlog` آپشن‌هایِ متنوع و جالبی رو داره.

برای اینکه خروجی رو براساس تعداد کامیت‌هایِ هر نویسنده مرتب کنیم از آپشنِ `n-` یا `numbered-—` استفاده می‌کنیم.

برای اینکه توضیحات نمایش داده نشن از آپشنِ `s-` یا `summary—-` استفاده می‌کنیم.

برای نشون دادنِ ایمیل از `e-` یا `email—-` استفاده می‌کنیم.

به کمک این دستور می‌تونیم خیلی راحت، فعال‌ترین contributer یا مشارکت‌کننده رو پیدا کنیم.

می‌تونیم خروجی این دستور فیلتر هم بکنیم. برای مثال می‌تونیم از `before—-` و `after—-` استفاده کنیم تا contributer رو براساس محدوده‌ی تاریخیِ مشخص‌شده پیدا کنیم.

```bash
git shortlog —n —s -e --before="" --after=""
```
