---
layout: post
title: Renaming or Moving Files
date: 2022-11-08 12:03:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**: با تغییر‌نام فایل با دستورِ یونیکسِ `mv`، باید دو تا فایل رو add کنیم (به staging area). یکی فایلِ حذف شده و تغییر‌یافته (فایل با اسمِ قبلی) (`M`) و فایلِ جدید و untracked (فایل با اسمِ‌ تازه) (`??`). چاره‌‌ی کار: مثلِ دستورِ `git rm` دستورِ `git mv` رو هم داریم.

```bash
git mv main.js file1.js
```

---

حال بیاین در مورد تغییرِ نام یا جابجاییِ فایل‌ها صحبت کنیم. در حال حاضر یه فایل در مسیرِ کاری مون داریم.

```bash
ls
```

```
file1.txt
```

اسمِ فایلِ رو به `main.js` تغییر می‌دیم.

```bash
‌mv file1.txt main.js
```

با دستورِ‌ mv هم می‌تونیم نام فایل رو تغییر بدیم و هم می‌تونیم به دایرکتوری یا مسیر دیگه جابجا کنیم. 

حال که مسیرِ کاری‌مون تغییر داشته، بیایین `git status` رو اجرا کنیم.

```
On branch master
Changes not staged for commit:
	(use "git add/rm <file>..." to update what will be committed)
	(use "git restore <file>..." to discard changes in working directory) 

		deleted: file1.txt

Untracked files:
(use "git add <file>..." to include in what will be committed)
		main.js

no changes added to commit (use "git add" and/or "git commit -a")
```

دو تا تغییر داریم و هر دوشون unstage هستن. یک عملیاتِ حذف داریم. (`deleted: file1.txt`) و در قسمتِ untracked files یک فایلِ جدید داریم. 

همونطور که در ابتدایِ این بخش مشاهده کردین گیت به صورتِ خودکار تمامی فایل‌هایِ جدیدتون رو شناسایی نمی‌کنه. هر موقع که شما فایلِ جدید به پروژه‌تون اضافه می‌کنین باید به staging area اضافه‌ش کنین تا گیت بتونه شروع به شناساییش کنه. 

دوباره از دستورِ add استفاده می‌کنیم تا هر دویِ تغییر بالا رو stage کنیم.

```bash
git add file1.txt
```

دستورِ بالا برای پاک کردنشه و حالا بیایین فایلِ جدید شناسایی نشده‌مون یعنی main.js رو اضافه کنیم.

```bash
git add main.js
```

حال بیایین یه بار دیگه `git status` رو اجرا کنیم.

```
On branch master
Changes to be committed:
	(use "git restore --staged <file>..." to unstage)
		renamed: tile1.txt —> main.js
```

گیت متوجه شد که ما file1.txt رو به main.js تغییر دادیم و در staging area هست. 

پس جابجایی یا تغییرِ نامِ فایل دو مرحله است. 

- باید مسیر کاریمون رو تغییر بدیم.
- باید دو نوعِ تغییر رو stage کنیم. یک افزودن و یک پاک کردن.

درست مثلِ حذفِ فایل‌ها، گیت به ما یک دستورِ خاص برای جابجایی یا تغییر نام فایل‌ها داده که `git mv` هست.

پس بجایِ استفاده از دستورِ استانداردِ یونیکس، قراره بیشتر از گیت استفاده کنیم. حال بیایین main.js رو به file1.js تغییر بدیم.

```bash
git mv main.js file1.js
```

حالا `git status` رو اجرا می‌کنیم.

```
On branch master
Changes to be committed:
	(use "git restore --staged <file>..." to unstage)
		renamed: file1.txt —> file1.js
```

یک عملِ تغییر نام برایِ تغییرِ‌نامِ file1.txt به file1.js داریم.

زمانی که از دستورِ `git mv` استفاده می‌کنیم تغییرات قراره که هم در مسیرِ‌کاری و هم در staging area اعمال بشه. 

حال بیایین این تغییرات رو commit کنیم.

```bash
git commit -m "Refactor code."
```

```
[master 7e3f6b1] Refactor code.
 1 file changed, 0 insertions(+), 0 deletions(—)
 rename file1.txt => file1.js (100%)
```

با توجه به خروجی و آمارِ و جزئیاتِ بالا، یک فایل تغییر داده شده، صفر درج داریم. چون هیچ خطی به هیچ کدوم از فایل‌هامون اضافه نکردیم همچنین صفر حذفیات داریم چون هیچ خطی رو از هیچ فایلی پاک نکردیم.