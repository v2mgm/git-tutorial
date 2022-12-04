---
layout: post
title: Squash Merging
date: 2022-11-13 20:50:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

در زیر bugfix branch رو با دو تا کامیت داریم؛ کامیت‌هایِ B1 و B2. 

فرض کنیم کارمون با این branch تموم شد و عملِ merge رو انجام دادیم. حالا کامیت‌هایِ B1 و B2 بخشی از تاریخچه‌‌مون شدن. ولی اگه این دو کامیت، کامیت‌هایِ باکیفیتی نباشن چی. شاید زیاد دقیق نباشن، یا زنجیره‌ی منطقیِ یکپارچه‌ای رو ارائه نمیدن، یا شاید چیزای ضد و نقیض مختلفی رو در هر کامیت داشته باشیم. به هر حال، شاید این کامیت‌ها باکیفیت نباشن. 

طبیعتاً این کامیتِ ترکیبیِ B1 و B2 به منظورِ‌ checkpoint اضافه شده. به همین خاطر، هیچ اهمیتی به تاریخچه‌ی bugfix branch نمی‌دیم. نمی‌خواهیم کامیت‌هایِ این branch تاریخچه‌ی master branch رو کثیف کنه. در چنین شرایطی راه‌حل بهتری به اسمِ Squash Merging رو داریم.

در Squash Merging، کامیتی رو می‌سازیم که تغییراتِ توی کامیت‌هایِ B1 و B2 (کامیت‌هایِ BugFix Branch) رو یکی کرده و در نتیجه زنجیره‌ی منطقیِ یکپارچه‌ای رو خواهیم داشت. این کامیت رو بعنوانِ آخرین کامیتِ master branch در نظر می‌گیریم. 

چیزی که باید بهش توجه کنید اینه که این کامیت، merge commit نیست. چون این کامیت دو تا والد نداره و به دو تا ارجاع به دو کامیت نداره و فقط به یه کامیت ارجاع داره (فقط یه دونه parent داره). فقط یه کامیتِ معمولی مثلِ دیگرِ کامیت‌هاست که کامیتِ آخرِ master هستش. 

حالا که کارمون با BugFix branch تموم شد می‌تونیم اون رو delete کنیم. و الان یک تاریخچه‌ی تمیز، خطی و ساده‌ای رو داریم. و این همون مزیتِ squash merging هستش. ولی این به این معنی نیست که همیشه از این نوع ادغام استفاده کنیم. زمانی باید از این تکنینک استفاده کنیم که با branchهایِ کوچیک، کوتاه‌عمر همراه با تاریخچه‌ی بی‌کیفیت روبرو هستیم. مثلِ branchهایِ bugfix یا feature که در چند ساعت یا در یک روز قابلِ پیاده‌سازی هستن.

![Squash-Merging]({{ page.imgPath }}Squash-Merging-1.gif#center)

branchای رو به اسمِ‌ bugfix/photo-upload رو می‌سازیم و داخلش دو تا کامیت می‌سازیم.

```bash
git switch -C bugfix/photo-upload
```

```bash
echo bugfix >> audience.txt
git commit -am "Update audience.txt"
```

```bash
echo bugfix >> toc.txt
git commit -am "Update toc.txt"
```

حالا داخلِ bugfix/photo-upload branch دو تا کامیت داریم. حالا دو تا کامیت جلوتر از آخرین کامیتِ master داریم.

```
* 827885a (HEAD -> bugfix/photo-upload) Update toc.txt
* 243d308 Update audience.txt
* 3a44949 (master) Revert "Merge branch 'bugfix/change—password' into master"
```

حالا بجای اینکه از mergeهایِ همیشگی استفاده کنیم و merge commit ثبت کنیم، از squash merge استفاده می‌کنیم. برای این کار، ابتدا به master branch سوئیچ می‌کنیم و سپس برای merge کردن از دستورِ زیر استفاده می‌کنیم.

```bash
git merge --squash bugfix/photo-upload
```

با اجرایِ دستورِ بالا، گیت کامیتِ جدیدی رو می‌سازه که این کامیت Squash commit نام داره. در این کامیت تغییراتِ موجود در دو فایلِ audience.txt و toc.txt یکی شدن. ولی هنوز کامیتی رو نداریم! تمامِ تغییرات در staging area هستن. 

```bash
M  audience.txt
M  toc.txt
```

حالا باید این تغییرات رو کامیت کنیم. 

```bash
gt commit -m "Fix the bug on the photo upload page."
```

حالا history رو نگاه کنیم.

```
* b697ca  (HEAD -> master) Fix the bug on the photo upload page.
| * 827885a (bugfix/photo-upload) Update toc.txt
| * 243d308 Update audience.txt
|/
* 3a44949 (master) Revert "Merge branch 'bugfix/change—password' into master"
```

حالا آخرین کامیت‌مون تمامِ تغییراتی که برای رفعِ‌ باگِ مورد نظرمون رو تو خودش combine کرده. حالا برای اینکه history تمیز و خطی‌ای رو داشته باشیم باید bugfix/photo-upload branch رو حذف کنیم ولی قبلش یه چیزی رو ببینیم.

حالا که تویِ master branch هستیم با دستورِ زیر branchهایی رو که با master ادغام شدن رو می‌بینیم.

```bash
git branch --merged
```

ولی در خروجیِ بالا هیچ اثری از bugfix/photo-upload branch نیست. چون در واقع merge commitای رو نداریم که branchهایِ bugfix/photo-upload و master رو به هم مرتبط کنه. 

به همین خاطر وقتی که در Squash merge هستیم خیلی ضروری هست که branch هدف رو حذف کنیم در غیر اینصورت branch همون‌جا باقی خواهد ماند و موجبِ سردرگمی‌مون خواهد شد. برای اثبات این دلیل به خروجیِ دستورِ زیر توجه کنید. 

```bash
git branch --no-merged
```

با اینکه تغییرات تویِ bugfix/photo-upload branch رو توی کامیتِ مشخصی یکی کردیم، در خروجی دستورِ بالا bugfix/photo-upload رو هم داریم! و این گیج‌کننده هستش. 

پس، این branch رو حذف می‌کنیم.

```bash
git branch -d bugfix/photo-upload
```

ولی با اجرای دستورِ بالا، با خطایِ عدم merge روبرو خواهیم شد. با توجه به اینکه در این حالت، گیت از merge واقعی استفاده نکرده با این نوع خطا روبرو می‌شیم. برای اینکه گیت رو مجبور به حذفِ این branch کنیم از آپشنِ `D-` استفاده می‌کنیم.

```bash
git branch -D bugfix/photo-upload
```

یه بار دیگه history رو ببینیم.

```
* b697ca  (HEAD -> master) Fix the bug on the photo upload page.
* 3a44949 (master) Revert "Merge branch 'bugfix/change—password' into master"
```

زمانی که از squash merging استفاده می‌کنیم امکانِ مواجهه با conflictها خواهد بود. فرایندِ رفعِ conflictها مثلِ سابق هستش: از ابزارِ merge استفاده می‌کنیم، conflictها رو resolve می‌کنیم و در نهایت commit می‌سازیم.