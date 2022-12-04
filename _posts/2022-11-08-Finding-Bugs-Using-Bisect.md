---
layout: post
title: Finding Bugs Using Bisect
date: 2022-11-08 17:42:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---
**خلاصه**: برای یافتنِ سریعِ باگی که نمی‌دونیم در کدوم کامیت بوجود اومده. بهش کامیت خوب و بد رو از طریقِ آی‌دیِ کامیت، می‌دیم و bisect هم از وسطِ کامیتِ خوب و بد شروع به یافتنِ کامیتِ باگ‌دار می‌کنه. و این رویه رو تا اجرایِ کامیتِ‌باگ‌دار ادامه می‌ده. با اجرایِ این دستور، HEAD نیز detach خواهد شد چون به MASTER اشاره نخواهد کرد بلکه به کامیتِ میانیِ بینِ کامیتِ خوب و بد اشاره خواهد کرد.

این ابزار، هر بار تعداد کامیت‌ها برای پیدا کردنِ باگ رو نصف می‌کنه.

```bash
git bisect start
git bisect bad
git bisect bad ca49180
```

---

در این جلسه قراره که راجع به یک ابزار فوق‌العاده قدرتمند برای یافتنِ سریعِ باگ‌ها صحبت کنیم. اسمش bisect هست.

خب بیاین بگیم که تمامی این کامیت‌ها رو ساختیم و در این لحظه از زمان که آخرین کامیت اینجاست یک باگ در اپلیکیشن‌مون داریم که نمی‌دونیم این باگ‌ کجا بوجود اومده. حال نمی‌خوایم که هر کدوم از این کامیت‌ها رو چک کنیم. اینجوری کلی زمان می‌بره.

```
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

پس با استفاده از دستورِ bisect می‌تونیم سریعاً کامیت‌هایی که مشکل ایجاد کردن رو پیدا کنیم. فقط باید به گیت بگیم که کامیتِ کنونی کامیتِ بدی هستش. همچنین باید یک کامیتِ خوب هم بدیم. برای مثال، اولین کامیتی که ساختیم یک کامیتِ خوب بوده و درش باگی رو نداشتیم.

پس برای یافتنِ کامیتِ بد دستورِ `git bisect start` رو اجرا می‌کنیم.

```bash
 git bisect start
```

پس از اجرایِ دستورِ بالا، می‌تونیم به bisect کامیتِ خوب و کامیتِ بد رو بدیم.

چون کامیتِ بد‌مون آخرین کامیت هستش بصورتِ زیر اون رو مشخص می‌کنیم.

```bash
git bisect bad
```

و کامیتِ خوب رو که در اینجا اولین کامیت‌مون هست رو از طریقِ آی‌دی‌ش مشخص می‌کنیم.

```bash
git bisect bad ca49180
```

خروجی:

```
Bisecting: 5 revisions left to test after this (roughly 3 steps)
[36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8] Include the command prompt in code sample.
```

حالا گیت می‌گه که پنج تا Revision یا پنج کامیت برای تست داریم و این سه قدم می‌خواد. ببیینین الان کجاییم. دیگه در Master نیستیم بلکه در `bisect/bad~6` هستیم.

حالا اگه دستورِ‌ `git log —-oneline` رو اجرا کنیم، خروجی‌ش زیر خواهد بود.

```
36cd6db (HEAD) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good—ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

همانطور که در بالا می‌بینید HEAD detached شده. چون دیگه به MASTER اشاره نمی‌کنه. البته می‌تونیم به تمامیِ کامیت‌ها با دستورِ `git log —-oneline —-all` دسترسی داشته باشیم.

```
a642e12 (master, refs/bisect/bad) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (HEAD) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good—ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

همانطور که در خروجیِ بالا می‌بینید کنارِ master عبارتی رو می‌بینیم که اشاره داره به کامیتِ بد. کامیتِ بد و خوب با رفرنس‌هایِ `refs/bisect/good` و `refs/bisect/bad` در خروجیِ بالا مشخص شده. HEAD به کامیتِ وسطیِ این دو کامیتِ خوب و بد اشاره داره.

الان برنامه‌مون رو اجرا می‌کنیم که ببینیم آیا باگِ مورد‌نظرمون در این کامیت (کامیتی که HEAD بهش اشاره داره) هست یا نه. اگر باگ درش باشه بدین معناست که باگی که نوشتیم جایی است بینِ کامیت‌هایِ ca49180 تا 36cd6db یعنی نیمه‌ی اولِ هیستوری‌مون. در این مورد نیازی نیست که نیمه‌ی دوم رو بررسی کنیم.

از طرفِ دیگه اگر این کامیتی که الان درش هستیم بدونِ باگ باشه (کامیتِ خوبی باشه) پس مشکل در نیمه‌ی دومِ هیستوری‌مون هستش یعنی بینِ کامیت‌هایِ 24e86ee تا a642e12. و باید نیمه‌ی اول رو بررسی کنیم.

به مثال‌مون برمی‌گردیم. به گیت می‌گیم که این کامیتی که الان HEAD بهش اشاره داره، خوبه.

```bash
git bisect good
```

خروجی‌ش می‌شه:

```
Bisectingi 2 revisions left to test after this (roughly 2 steps)
```

با توجه به خروجیِ بالا، حالا دو تا revisions یا کامیت برای تست داریم و این حداکثر دو قدم می‌خواد.

بیاین یه بارِ دیگه به لاگ‌مون نگاه کنیم.

```
a642e12 (master, refs/bisect/bad) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 (HEAD) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good—364918083ec471878d58612142572f3367faf5d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good—ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

حالا HEAD باز دوباره به کاکیتِ وسطیِ بین کامیت‌هایِ خوب و بد اشاره می‌کنه.

برای مثال می‌گیم که این کامیتی که HEAD بهش اشاره داره کامیتِ خوبی هستش و این یعنی باگ بینِ دو کامیت‌ِ 555b62e و 50db987 هستش.

```bash
git bisect good
```

خروجیِ کد بالا:

```
Bisectingi 0 revisions left to test after this (roughly 1 steps)
```

با توجه به خروجیِ بالا، صفر تا revision برایِ تست داریم و یه قدم دیگه مونده.

پس بیایین یه بار دیگه به لاگمون یه نگاهی بندازیم.

```
a642e12 (master, refs/bisect/bad) Add header to all pages.
50db987 (HEAD) Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 (refs/bisect/good—842918083ec471878d58612142572f3367faf1a5) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good—364918083ec471878d58612142572f3367faf5d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good—ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

حالا بیایین بگیم که این کامیتی که HEAD داره بهش اشاره می‌کنه نیز کامیتِ ‌بد هستش.

```bash
git bisect bad
```

خروجی‌ش:

```
Bisectingi 0 revisions left to test after this (roughly 0 steps)
```

به هیستوری‌مون یه نگاهی بندازیم.

```
a642e12 (master) Add header to all pages.
50db987 (refs/bisect/bad) Include the first section in TOC.
555b62e (HEAD) Include the note about committing after staging the changes.
91f7d40 (refs/bisect/good—842918083ec471878d58612142572f3367faf1a5) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good—364918083ec471878d58612142572f3367faf5d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good—ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

همانطور که در خروجی می‌بینین HEAD داره به کامیتی اشاره داره که قبلش کامیت‌خوبه‌ست و بعدش کامیت‌بده. پس اون جایی که HEAD داره بهش اشاره می‌کنه همون‌جایی هست که اولین‌بار باگ در اون کامیت بوجود اومده.

حالا به کامیت می‌گیم که این کامیت، کامیت‌بده هستش.

```bash
git bisect bad
```

و خروجیِ بالا:

```
555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6 is the first bad commit
commit 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date: Mon Aug 17 14:26:49 2020 —0700

 Include the note about committing after staging the changes.

sections/creating-snapshots/staging-changes.txt | 2 ++
1 file changed, 2 insertions(+)
```

حالا گیت اولین کامیتِ بده رو می‌دونه. در خروجیِ بالا اطلاعات کاملی رو در مورد این کامیت می‌بینیم. پس می‌تونیم به idش، نویسنده‌ش و زمانی که ساخته شده، پیغامش و خلاصه‌ای از تغییرات رو ببینیم.

پس با استفاده از ابزارِ bisect می‌تونیم هیستوری‌مون رو به نصف تبدیل کنیم و کامیت‌هایِ مختلفی رو چک کنیم تا اولین کامیت بد رو پیدا کنیم.

زمانی که کارمون تموم شد باید HEAD رو به master وصل یا attatch کنیم.

```bash
git bisect reset
```

حالا در master هستیم.
