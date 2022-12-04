---
layout: post
title: Visual Diff Tools
date: 2022-11-08 16:36:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**: مشخص کردن ابزارِ diff با ویرایشِ فایلِ کانفیگ. برای مشاهده‌ی فایلِ کانفیگ از دستورِ `git congif --global -e` استفاده می‌کنیم.

```bash
git config ——global diff.tool vscode
git config ——global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```

حالا می‌تونیم تفاوت‌ها رو بصورتِ بصری ببینیم.

```bash
git difftool
git difftool --staged
```

---

همونطور که در جلسه‌ی قبلی گفتم، معمولاً ما از ابزارهایِ بصریِ diff برای مقایسه‌ی فایل‌ها استفاده می‌کنیم. کلی برنامه‌ی بصریِ diff هست که محبوب‌ترین‌شون kdiff و p4merge هستن که کراس‌پلتفرم هستن. و winmerge که فقط برای ویندوزه.

در این جلسه از VSCode برای قیاسِ فایل‌ها استفاده خواهیم کرد. 

ابتدا در ترمینال، اول از همه باید به گیت بگیم که می‌خوایم از VSCode به عنوانِ ابزارِ diff پیشفرض استفاده کنیم. باید دو تا پیکربندی انجام بدیم. 

در خطِ اول، vscode فقط یه اسمی هستش که برایِ ابزارِ diffمون انتخاب کردیم.

در خطِ دوم نحوه‌ی کارِ VSCode رو مشخص کردیم. در این خط با توجه به اینکه VSCode رو به path اضافه کردیم (تا بتونیم از هر جایی اجراش کنیم) از code استفاده کردیم. در این خط، code رو با یه سری آرگومان اجرا می‌کنیم. اولی `wait-—` هست که به ترمینال می‌گه که صبر کنه تا کارِ ما با VSCode تموم بشه. یعنی تا زمانی که ما تغییرات رو مقایسه کرده و VSCode رو ببندیم. 

دومین آرگومان، `diff-—` هست که به VSCode می‌گه می‌خوایم برای مقایسه‌ی فایل‌ها یا diff ازش استفاده کنیم. بعدش دو تا آرگومان دیگه هم داریم که `LOCAL$` (با حروفِ بزرگ) و `REMOTE$` (با حروفِ بزرگ) هستن. این‌ها نگه‌دارنده‌ای برایِ کپی‌هایِ قدیمی و جدیدِ فایل هستن.

```bash
git config ——global diff.tool vscode
git config ——global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```

با دستورِ زیر مطمئن بشین که این قدم رو درست انجام دادین.

```bash
git congif --global -e
```

حالا می‌تونیم با دو دستورِ زیر با ابزارِ diffمون کار کنیم.



```bash
git difftool
git difftool --staged
```

این روزا خیلی از ابزارِ‌ diff استفاده نمی‌کنیم. فقط برا این گفتم چون می‌خوام دوره‌م کامل باشه. این روزها اکثر ادیتور و IDE‌ها به شما اجازه‌ی مشاهده‌ی stage و unstage رو به عنوانِ بخشی از محیطِ توسعه می‌دن.