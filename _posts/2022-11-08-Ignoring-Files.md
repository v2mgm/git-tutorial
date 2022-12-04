---
layout: post
title: Ignoring Files
date: 2022-11-08 12:06:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**: چشم‌پوشی و ignore یه سری فایل‌ها با قرار دادنشون در فایلِ `gitignore.`

البته برای اینکه این فایل ignore بشه و تغییراتش ردیابی نشه علاوه بر وجود در فایلِ `gitignore.` باید در staging area هم نباشه. برای اینکه فایل رو فقط از staging area پاکش کنیم (و نه از working dir) از دستورِ `rm` با آپشن‌هایِ زیر استفاده می‌کنیم.

```bash
git rm --cached -r bin/
```

---

تقریباً در هر پروژه ای ما باید به گیت بگیم که یک سری فایل‌ها و مسیرهای مشخص رو چشم‌پوشی کنه. برای مثال نمی‌خواهیم فایل‌هایِ log یا باینری که به عنوان نتیجه کامپایل کدمون هست رو شامل کنیم. چون افزودن این فایل‌ها فقط سایزِ ریپومون رو بدون هیچ امتیازِ مثبتی زیاد می‌کنه. 

هر توسعه‌دهنده‌ای می‌تونه فایل‌هایِ log خودش رو داشته باشه درسته؟ لاگ فایل‌ها فایل‌هایی نیستن که بخوایم به اشتراک بذاریم و با بقیه اعضا سینک کنیم. برای این نمونه بیاین ی مسیر به نام logs بسازیم و بعدش ی فایل log اینجا داشته باشیم.

```bash
mkdir logs
```

دوباره، میتونیم از دستور `echo` برای نوشتن `hello` در `logs/dev.log` استفاده کنیم.

```bash
echo hello > logs/dew.log
```

حالا بیاین `git status` رو اجرا کنیم. 

```
On branch master
Untracked files:
	(use "git add <file>..." to include in what will be committed)
		logs/

	nothing added to commit but untracked files present (use "git add" to track)
```

خب گیت میگه که یک فایل ناشناس در مسیر logs داریم. اما ما نمی‌خوایم که این رو به Staging area اضافه کنیم چون نمیخوایم این رو شناسایی و ردیابی کنه. پس برای جلوگیری از این ما باید یک  فایلِ مخصوص به نام `gitignore.` بسازیم. این فایل هیچ نامی نداره و فقط یک پسوند داره و باید تو مسیر اصلی  پروژتون باشه.

 

```bash
echo logs/ > .gitignore
```

بیاین حالا این فایل رو با وی‌اس‌کد باز کنیم (`code .gitignore`) 

در این فایل یک نوشته یک خطی داریم /logs  که نمایانگر یه مسیره. می‌تونیم هر چقدر که می‌خوایم فايل و مسیر اینجا لیست کنیم.

```
logs/
main.log
*.log
```

اگر `git status` روی بار دیگه اجرا کنین دیگه نمیگه یه مسیر جدید به نام `logs` داریم چون داره ازش چشم پوشی می‌کنه در عوض می‌گه که یک فایل جدید به نام `gitignore` داریم.

```
On branch master
Untracked files:
	(use "git add <file>..." to include in what will be committed)
		.gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

خب بیاین این رو به staging area اضافه کنیم و بعدش کدمون رو کامیت کنیم.

خب add gitignore و اینجوری متیونیم از یه سری فایل‌ها و مسیر‌ها در گیت چشم‌پوشی کنیم.

```bash
git add .gitignore
```

```bash
git commit -m "Add gitignore"
```

فقط یادتون باشه که اگر تصادفاً یک فایل رو در ریپوتون اضافه کردین و بعدش gitignore رو اضافه کردین اون فایل رو ignore نخواهد کرد.

```bash
mkdir bin
```

تصور کنین که مسیر بالا شامل سورس کدِ کامپایل‌شده‌ی ماست. با کمک دستور echo عبارتِ hello در داخل bin/app.bin مینوسیم

```bash
echo hello > bin/app.bin
```

 و حالا `git status` 

```
On branch master
Untracked files:
(use "git add <file>..." to include in what will be committed)
	bin/

nothing added to commit but untracked files present (use "git add" to track)
```

این رو به ریپومون کامیت کنیم.

```bash
git add .
git commit —m "Add bin."
```

بعدش میایم به کدمون. مشکل اینجاست هر موقع که کدمون رو کامپایل میکنیم گیت میگه که این فایل bin/app.bin تغییر داشته. پس چرا باید هر سری که برناممون رو کامپایل می‌کنیم این فایل رو commit کنیم.

برمیگردیم سراغ `gitignore.` و مسیر `/bin` رو هم اضافه کنیم.

 برگردیم به ترمینال. بیاین دستور `git status` رو اجرا کنیم.

```
modified: .gitignore
```

 خب ما `gitignore.` رو به صورت modified داریم. زیباست. حال بیاین این تغییر رو کامیت کنیم.

```bash
git add .
git commit —m "Include bin/ in gitignore."
```

حال در این مورد گیت این مسیر رو شناسایی و ردیابی کرده پس بیاین فایل bin رو با کدِ زیر تغییر بدیم.

```bash
echo helloworld > bin/app.bin
```

دستورِ git status رو می‌زنیم. 

```
On branch master
Changes not staged for commit:
	(use "git add <file>..." to update what will be committed)
	(use "git restore <file>..." to discard changes in working directorY) 
		modified: bin/app.bin

no changes added to commit (use "git add" and/or "git commit —a")
```

گیت می‌گه که این فایل تغییر داده شده. این چیزی نیست که ما می‌خوایم. برای رفع این مشکل ما باید این فایل رو از Staging area پاک کنیم.

خب قبل‌تر درباره `git ls-files` صحبت کردیم می‌تونین ببینین مسیر یا فایل bin داخلِ staging area هست باید از اینجا پاکش کنیم. چطوری؟

```bash
git ls-files
```

```
.gitignore
bin/app.bin
file1.js
```

 خب قبلاً راجع به دستور `rm` صحبت کردیم. بهتون گفتم که با این دستور می‌تونیم یک فایل و یا مسیر رو هم از مسیر کاری‌مون و هم از Staging area پاک کنیم. ولی می‌خوایم که این فایل رو فقط از Staging area پاک کنیم. چطوری؟

```bash
git rm --cached bin/
```

ولی با اجرایِ دستورِ بالا با خطایِ زیر مواجه می‌شیم.

```
fatal: not removing 'bin/' recursively without -r
```

چون می‌خواهیم کل مسیر bin رو از staging area پاک کنیم از دستورِ زیر استفاده می‌کنیم.

```bash
git rm --cached -r bin/
```

حالا کلِ مسیر `/bin` از staging area پاک شده. اگه `git status` کنیم خروجیِ زیر خواهیم داشت.

```
On branch master
Changes to be committed:
	(use "git restore ——staged <file>..." to unstage)
		deleted: bin/app bin
```

این تغییر رو کامیت می‌کنیم.

```bash
git commit —m "Remove the bin directory that was accidentally commited."
```

اوکی. از اینجا به بعد دیگه گیت قرار نیست تغییرات مسیرِ `/bin` رو ردیابی کنه.

در [این آدرس](http://github.com/github/gitignore) می‌تونید فایل‌هایِ gitignore. رو برای زبان‌هایِ برنامه‌نویسیِ مختلف پیدا کنید.