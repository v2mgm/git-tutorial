---
layout: post
title: Staging Files
date: 2022-11-08 10:54:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**:‌ برای مشاهده‌ی وضعیتِ working directory از `git status` استفاده می‌کنیم. فایل یا فایل‌ها یا هر چیزی (period) که جدیده و یا تغییر داده شده رو با دستورِ `git add` به staging area می‌بریم.

---

بیایین چند تا فایل به پروژه‌مون اضافه کنیم. برای این کار از دستورِ استانداردِ یونیکس/لینوکس `echo` استفاده می‌کنیم. این دستور برای نوشتنِ محتوا در فایل استفاده می‌شه. 

```bash
echo hello > file1.txt
echo hello > file2.txt
```

حالا دو تا فایلِ جدید در پروژه‌مون داریم که هنوز توسطِ‌ گیت track نشدن. زمانی که برای اولین بار ریپویِ گیت  در پروژه‌تون init می‌کنید گیت بصورتِ اتوماتیک فایل‌ها رو track نمی‌کنه. حالا اگه هزارتا فایل هم در پروژه‌تون باشه باید به گیت بگین که اون فایل‌ها رو track کنه. 

با دستورِ زیر وضعیتِ Working Directory یا دایرکتوریِ کاری‌مون رو در staging area چک کنیم. 

```bash
git status
```

خروجیِ دستورِ git status رو در زیر می‌بینید.

```bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        file1.txt
        file2.txt

nothing added to commit but untracked files present (use "git add" to track)
```

هیچ کامیتی هنوز نداریم. یه سری فایل‌هایِ Untracked داریم. چون هنوز این فایل‌ها در staging area نیستن. برای این کار از دستورِ زیر به چهار طریق می‌تونیم استفاده می‌کنیم.

```bash
git add file1.txt
git add file2.txt
```

```bash
git add file1.txt file2.txt
```

```bash
git add *.txt
```

```bash
git add .
```

در استفاده کردن از period یا نقطه (که بصورتِ recursively کل فایل‌هایِ‌ پروژه رو اَد می‌کنه) کمی باید هُشیار باشید چون بعضاً فایل‌هایی هست که نمی‌خواین به ریپو اضافه کنین. مثلاً فایل‌هایِ بزرگ مثلِ فایل‌هایِ باینری بزرگ یا فایل‌هایِ log. چون سایز ریپو رو بیشتر می‌کنن. بعداً نحوه‌ی ignore کردنِ چنین فایل‌هایی رو یاد خواهیم گرفت.

حالا با دستورِ بالا فایل‌هامون رو در staging area قرار دادیم و آماده برایِ commit شدن هستن. 

حالا اگه دوباره `git status` کنیم مشاهده‌ خواهیم کرد که این دو فایل در Staging area قرار گرفتن.

```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt
```

دوباره با دستورِ زیر فایلِ `file1.txt` رو تغییرش می‌کنیم. علامتِ `<<` به معنایِ append کردنِ محتواست.

```bash
echo world >> file1.txt
```

و حالا دوباره `git status` می‌کنیم.

```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   file1.txt
```

با توجه به وضعیتِ بالا، دو فایل رو در staging area داریم و یک فایلِ modified هم در دایرکتوریِ کاری‌مون داریم. شاید بپرسید اما ما قبلاً file1.txt رو به staging area اضافه کردیم. آره. ولی وقتی که دستورِ add رو اجرا کردین گیت یک snapshot از `file1.txt` گرفت و اون snapshot رو به staging area اضافه‌ش کرد. 

حالا در staging area اولین نسخه‌ی `file1.txt` رو داریم. تغییراتی رو که در `file1.txt` انجام شده هنوز stage نشدن. پس چیزی که الان داخلِ مسیر‌ کاری‌مون یا Working directory داریم دومین نسخه از این فایله. یه سری تغییرات داشته که هنوز stage نشدن. پس یک از دو کارِ زیر رو می‌کنیم.

```bash
git add file1.txt
```

```bash
git add .
```

دوباره `git status` می‌کنیم تا به مسیرِکاری‌مون یه نگاهی بندازیم.

```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   file1.txt
        new file:   file2.txt
```

حالا هر دویِ فایل‌ها در staging area هستن و ما هیچ تغییرِ unstageای نداریم. در قدمِ بعدی می‌خوایم که نشونتون بدم که چطور این snapshot رو به صورتِ‌ دائم commit کنین تا داخلِ ریپوی گیت‌مون ذخیره شه.