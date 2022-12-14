---
layout: post
title: Viewing a Commit
date: 2022-11-08 16:48:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**:‌ هر آبجکتی (کامیت، blob (فایل)، tree (مسیر) و tag) که در دیتابیسِ گیت هستش رو با دستورِ show می‌تونیم مشاهده‌ش کنیم.

آرگومان‌هایِ این دستور می‌تونه بخشی از آی‌دیِ کامیت، اشاره‌گرِ HEAD و کامیت‌هایِ قبل‌تر HEAD به کمکِ کاراکترِ تیلدا و سپس برای دقیق‌تر شدن، در ادامه دونقطه و اسمِ فایل. آرگومان‌هایِ دیگه‌ش می‌تونه آی‌دیِ blob و tree و تگ باشه.

```bash
git show HEAD~1
git show HEAD~1:.gitignore
git show 1dcc30
```

برای اینکه تمامیِ مسیرها و فایل‌هایِ تویِ کامیت رو ببینیم از دستورِ `git ls-tree` استفاده می‌کنیم.

```bash
git ls-tree HEAD~1
```

---

دیدنِ لیستِ‌ کامیت‌ها عالیه. اما اگر بخواهیم که ببینیم دقیقاً تو اون کامیت چی رو تغییر دادیم چی؟ این وقتی هست که از دستورِ `show` استفاده می‌کنیم. 

آرگومانی که برایِ دستورِ show پاس می‌دیم می‌تونه آی‌دیِ کامیت به تعداد کاراکترهایی باشه که ازش در آی‌دیِ کامیت‌ها تکرار نشده باشه. 

آرگومانِ دیگه‌ای که می‌تونیم بهش پاس بدیم دادنِ عبارتِ HEAD هستش. head به آخرین کامیت اشاره داره. 

آرگومانِ دیگه‌ای که می‌تونیم بهش پاس بدیم، ارسال کامیت‌هایِ قبل‌تر از کامیتی که HEAD بهش اشاره داره. بصورتِ `HEAD~1` که 1 اشاره به تعداد قدمِ قبل‌تر هست. 

```bash
git show HEAD~1
```

خروجیِ دستورِ بالا:

```
Author: Mosh Hamedani <programmingwithmosh©gmail.com>
Date: Tue Aug 4 16:52:21 2020 -0700

	Include bin/ in gitignore.

diff --git a/.gitignore b/.gitignore
index 8432ad3..1dcc30c 100644
--- a/.gitignore
+++ b/.gitignore
@@ -1,3 +1,4 @@
logs/
main.log
—*.log
\ No newline at end of file 1
+*.log
+bin/
\ No newline at end of file
```

در سه خط اول author و بعدش تاریخ کامیت و همینطور پیغامش رو می‌بینیم. 

حالا اگه نخواهیم تفاوت‌ها رو در خروجی ببینیم چی؟ اگر بخواهیم نسخه‌ی نهایی رو ببینیم. دقیقاً اون نسخه‌ای که در کامیت هست. 

```bash
git show HEAD~1:.gitignore
```

خروجیِ دستورِ بالا:

```
logs/
main.log
*.log
bin/
```

در خروجیِ بالا، نسخه‌ی دقیقی که داخلِ کامیتِ مورد نظر از فایلِ‌ `gitignore.` ذخیره شده رو می‌بینیم.

همانطور که قبلاً نیز بهتون گفتم هر کامیت یک کپی کامل از مسیرِ‌کاری‌مون داره. نه فقط تغییرات بلکه وقتی ما دستورِ show رو اجرا می‌کنیم فقط تغییرات و چیزی که تغییر کرده رو می‌بینیم. اگر بخواین که تمامیِ فایل‌ها و مسیرها داخلِ این کامیت رو ببینین چی؟

برای این کار باید از یک دستورِ متفاوت استفاده کنیم.

```bash
git ls-tree HEAD~1
```

چرا این یه درخت نامیده می‌شه؟ خُب این درخت، یک ساختمان‌ِ داده هست که اطلاعاتی رو با ترتیب نمایش‌ می‌ده. در یک درخت، می‌تونیم node داشته باشیم و این nodeها می‌تونن فرزند داشته باشن. حال مسیر‌ها در فایل‌سیستم می‌تونن توسط یک درخت ارائه بشن. چون هر مسیر می‌تونه فرزند داشته باشه. این ‌فرزندها می‌تونن فایل یا هر زیرمسیرِ دیگه‌ای باشن. 

پس `ls-tree` یعنی تمامِ فایل‌هایِ داخلِ درختِ رو لیست کن.

خروجیِ دستورِ بالا:

```
100644 blob 1dcc30c4cd47f8915741af2cfef91e16e0dc7d89 .gitignore
040000 tree 64629cd51ef4a65a9d9cb9e656e1f46e07e1357f bin
100644 blob badfb70fd8b1725682b26674f7b2882e94078579 file1.js
```

در خروجیِ بالا تمامیِ فایل‌ها و فولدرهایِ داخلِ کامیتِ مشخص‌شده رو می‌بینیم. 

آیدیِ‌هایِ تویِ خروجیِ بالا براساسِ محتوایِ فایل یا مسیر ساخته شده. در دیتابیسِ گیت یک آبجکت با هر یک از این آیدی‌ها داریم. 

حالا یه نگاهی به نوعِ آبجکت‌ها بندازین. در tree فایل‌ها با blob نمایش دیده می‌شن و مسیر‌ها توسطِ tree نمایش داده می‌شن. تمامیِ بالایی‌ها آبجکت‌هایی هستن که در دیتابیسِ گیت ذخیره شدن. 

با دستورِ show می‌تونیم خیلی راحت یک آبجکت رو که در دیتابیس گیت ذخیره شده رو ببینیم. برای مثال اگر بنویسیم git show و بعدش آیدی رو مشخص کنیم (فقط چند حرف ازش که تکراری با بقیه‌ی آیدی‌ها نشه) می‌تونیم محتوایِ اون آبجکت رو ببینیم.

```bash
git show 1dcc30
```

خروجیِ دستورِ بالا:

```
logs/
main.log
*.log
bin/
```

بیایید به محتوایِ یه مسیر یا tree نگاهی بندازیم.

```bash
git show 64629
```

خروجیِ دستورِ بالا:

```
tree 64629

app.bin
```

در داخلِ این درخت، فایل‌ِ `app.bin` رو داریم.