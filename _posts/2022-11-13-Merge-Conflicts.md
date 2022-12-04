---
layout: post
title: Merge Conflicts
date: 2022-11-13 14:06:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---
معمولاً هنگامی که merge می‌کنیم با Conflict (مغایرت) روبرو می‌شیم.

conflicts زمانی رخ می‌ده که:

- همون خط‌کد در فایلِ یکسان به شکل‌هایِ متفاوت از هم در دو branch تغییر داده شده باشه. (Change1, Change2)
- فایلی در branchای تغییر داده شده باشه ولی در branch دیگری همون فایل حذف شده باشه. (Change, Delete)
- فایل با اسمِ یکسان ولی محتوای متفاوت‌تر از هم در دو branch اضافه (add) شده باشه. (Add1, Add2)

در این شرایط گیت نمی‌فهمه که چطور باید این تغییرات رو با هم merge کنه. به همین خاطر فرایندِ ادغام رو متوقف می‌کنه. و ما باید به گیت، نحوه‌ی انجام این فرایند رو مشخص کنیم. 

بریم سراغِ یه مثال واقعی. توی master branch هستیم. با دستورِ زیر یه branch جدید می‌سازیم و بهش switch می‌کنیم.

```bash
git switch -C bugfix/change-password
```

فایلِ `change-password.txt` رو که در master هست رو در این branch تغییر می‌دیم و این تغییر رو کامیت می‌کنیم. 

حالا به master branch سوئیچ می‌کنیم. الان در master همون فایل رو به شیوه‌ی دیگه‌ای تغییرش می‌دیم. 

حالا یک فایل یکسان رو در branchهایِ master و bugfix داریم که محتوایِ یکسانی رو ندارند. حالا که می‌خواهیم دستورِ merge رو بنویسیم با merge CONFLICT روبرو می‌شیم.

```bash
git merge bugfix/change-password
```

خروجیِ دستورِ بالا `Merge conflict in change-password.txt` خواهد بود. گیت فرایندِ ادغام رو متوقف کرده و این رو می‌دونیم که عملِ ترکیب رو باید دستی انجام بدیم. همچنین چون داخلِ فرایندِ merge هستیم عبارتِ merge در ترمینال نیز نمایان هستش. 

![img]({{ page.imgPath }}Merge-Conflicts.png#center)

دستورِ git status رو اجرا می‌کنیم.

```
Unmerged paths:
	(use "git add <file>..." to mark resolution)
		both modified: change—password.txt
```

خروجیِ بالا، فایل‌ یا فایل‌هایِ conflict رو مشخص کرده. هر دو branch فایلِ `change—password.txt` رو modify کردن. البته در اینجا با یه نمونه‌ی ساده روبرو هستیم در سناریوهایِ واقعی بیشتر از ده فایل در خروجیِ بالا لیست خواهند شد. 

اساساً هر چقدر که مسیرِ branchهاتون از هم جدا می‌شه همون‌قدر با conflictهایِ بیشتری روبرو خواهیم شد.

حالا که با conflict روبرو هستیم باید چی کار کنیم؟ فایلِ `change—password.txt` رو باز می‌کنیم.

تو محتوایِ فایلِ `change—password.txt` تغییرات در هر branch توسطِ `>>>>>>>` و `<<<<<<<` مشخص شده. منظور از HEAD یعنی branch فعلی‌ای که توش هستیم و HEAD داره بهش اشاره می‌کنه.

توسطِ `========` تغییرات از هم جدا شدن.

```
hello

<<<<<<< HEAD
Change in the master branch.
=======
Change in the bugfix branch.
>>>>>>> bugfix/change—password
```

در یه سناریویِ واقعی با چندین conflict در یه فایل روبرو خواهیم بود. و به ازایِ هر تغییر، علامت‌هایِ بالا رو خواهیم داشت.

اگه همین فایل رو با VSCode باز کنیم VSCode عبارتِ `Accept Current Change` رو برامون نشون خواهد داد که با کلیک روی این عبارت همه‌ی علامت‌ها حذف خواهند شد و فقط تغییراتی که master branch اعمال شده بود باقی خواهند ماند. یعنی فایل بصورتِ زیر تغییر خواهد کرد.

```
hello
Change in the master branch.
```

VSCode عبارتِ دیگه‌ای رو هم داره به اسمِ `Accept Incoming Change` که با فشردن این دکمه تغییراتِ bugfix branch فقط باقی خواهد موند و فایل بصورتِ زیر خواهد بود. 

```
hello
Change in the bugfix branch.
```

گزینه‌ی دیگری که VSCode بهمون پیشنهاد می‌ده `Accept Both Changes` هستش. که نتیجه‌اش محتوایِ زیر خواهد بود.

```
hello
Change in the master branch.
Change in the bugfix branch.
```

البته می‌تونیم این conflict رو به صورتِ دستی با حذفِ علائم تویِ متنِ فایل نیز حل کنیم. البته در این حالت نباید کد جدیدی نوشته باشه. چون این کد در هیچ کدوم از دو branchها نیستش. اگه این کار رو کنید این merge commit به عنوانِ یک evil commit شناخته خواهد شد. چون در این کامیت تغییری اعمال شده که در هیچ دو branch نیستش.

هدف اصلیِ merge commit اینه که تغییراتِ در هر دو branch رو یکی کنه. پس تا حد امکان سعی کنید در شرایط بالا، کد جدیدی رو ننویسید. البته در سناریوهایِ واقعی مجبور می‌شیم این کار رو بکنیم. 

حالا که conflict رو حل کردیم دستورِ add رو می‌نویسیم تا این فایل به staging area بره. چون این فایلی هست که می‌خواهیم در کامیتِ بعدی قرار بگیره.  

```bash
git add change-password.txt
```

```bash
git status
```

حالا خروجیِ دستورِ بالا به شرحِ زیر تغییر داده شده:

```bash
Changes to be committed:
	modified: change—password.txt
```

با توجه به خروجیِ بالا دیگه هیچ conflictای رو نداریم. حالا دستورِ `git commit` رو می‌نویسیم تا عملِ merge رو تموم کنیم.