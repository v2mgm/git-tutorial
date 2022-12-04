---
layout: post
title: Short Status
date: 2022-11-08 12:53:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**:‌ مشاهده‌ی وضعیتِ working directory بصورتِ مختصر با `git status -s`

معنی علایمِ تویِ خروجی:‌ کاراکترِ رنگِ قرمز و سمتِ راستی برایِ Working Directory و کاراکترِ رنگِ سبز و سمتِ چپی برایِ Staging area

`??` فایل تازه درست‌شده و هنوز در staging area نیست. `MM` تغییرات جدیدی در working directory هست که هنوز در staging area نیست. `A` فایل با تمامِ تغییراتش در staging area هست. `M` فایل تغییر داده شده و هیچ نمونه‌ای ازش نیز به staging area اضافه یا add نشده.

---

|---|---|
|  ![img]({{ page.imgPath }}Short-Status-1.png#center){:width="290px" height="201px"} |  ![img]({{ page.imgPath }}Short-Status-2.png#center){:width="290px" height="193px"} |

خُب شما بدست‌ آوردنِ وضعیت مسیر‌کاری رو با کمکِ دستورِ `git status` یاد گرفتین.

خروجیِ این دستور بسیار جامع هستش و خیلی هم پر از کلمات هستش. به عنوانِ یک جایگزین می‌تونیم از فلگِ short درش استفاده کنیم.

```
git status -s
```

بیایین، خروجیِ زیر رو یه نگاهی کنیم.

```
 M   file1.js
??   file2.js
```

در خروجیِ بالا با دو تا ستون سروکار داریم. سمتِ چپی، staging area رو نمایش می‌ده و سمتِ راستی مسیرِ‌کاری‌مون رو. ما `file1.js` رو تغییر دادیم برای همین‌ هم که یه m در ستونِ راستی داریم که همون مسیرِ‌کاریه. اما این تغییرات در staging area نیستن. برای همینم هست که هیچ چیزی در ستونِ چپی نداریم.

با توجه به اینکه `file2.js` فایلِ جدیدیه علامتِ سوال در هر دو ستون داریم. حال بیایین `file1.js` رو به staging area اضافه کنیم.

```
git add file1.js
```

حالا خروجیِ دستورِ `git status`

```bash
M    file1.js
??   file2.js
```

حالا برایِ `file1.js` یه m سبز در ستونِ چپی یا staging area داریم. پس تمامِ تغییراتی که در مسیرِ کاری‌مون داشتیم حالا در staging area هست. در ستونِ راستی هیچ تغییراتی رو نداریم و به همین دلیل خالی هستش. اگه فایلِ `file1.js` رو تغییر بدیم خروجیِ `git status -s` به صورتِ زیر خواهد بود.

```bash
MM    file1.js
??   file2.js
```

در ستونِ چپی یک M سبز داریم که به معنایِ اینه که یه سری تغییرات در staging area داریم اما یه سری تغییرات دیگه هم در Working directory یا مسیرِ‌کاری‌مون داریم که به staging area اضافه نکردیم. 

حالا بیایین `file1.js` رو یه بارِ‌ دیگه به staging area اضافه کنیم و بعدش `git status -s` رو اجرا کنیم.

```
git add file1.js
git status -s
```

```bash
M    file1.js
??   file2.js
```

حالا تموم تغییراتی که در مسیرِ‌کاری‌مون داشتیم در staging area هستن. 

کارِمون با file1 تموم شد. بیاین یه نگاهی به `file2.js` بندازیم. 

```
git add file2.js
git status -s
```

```
M    file1.js
A    file2.js
```

برایِ `file2.js` یک A سبز در ستونِ سمتِ چپ داریم که معنیِ Added هستش. پس `file2`.js اضافه شده و `file1.js` هم تغییر کرده.