---
layout: post
title: Fast-forward Merges
date: 2022-11-12 16:55:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

بهتره که هر موقع قصد داریم از branchها استفاده کنیم از آپشنِ `graph` دستورِ log استفاده کنیم. این آپشن ارائه‌‌ی بهتری از branchها و اینکه چطوری branchها از هم جدا شدن، نشون می‌دن. همانطور که می‌بینید این دستور زیاد طولانی شده و اینجاست که می‌تونیم از aliasها استفاده کنیم. 

```
> git log --oneline --all --graph
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
* 9052f6f (HEAD -> master) Restore toc.txt
* 5e7a828 Remove toc.txt
* a642e12 Add header to all pages.
* 50db987 Include the first section in TOC.
```

با توجه به خروجیِ بالا، bugfix branch یک کامیت جلوتر از master هست. همچنین با یه مسیرِ خطی روبرو هستیم. اگه bugfix branch شروع کنیم به master خواهیم رسید. master از bugfix جدا نیست. و این یعنی، وقتی که دستورِ merge رو اجرا کنیم گیت master branch رو fast-forward (جهش به جلو) خواهد کرد. 

برای اینکه تغییرات رو از bugfix به master بیاریم باید ابتدا در master branch باشیم و بعد از دستورِ زیر استفاده کنیم. 

```
> git merge bugfix/signup-form
Updating 9052f6f..f882c5c
Fast—forward
	audience.txt | 5 ++---
	1 file changed, 2 insertions(+), 3 deletions(—)
```

همانطور که در خروجی مشخصه از fast-forward merge استفاده شده و فایلِ `audience.txt` تنها فایلی هست که پنج بار تغییر داشته. 

یه بارِ دیگه نگاهی به تاریخچه بندازیم.

```
> git log --oneline --all --graph
* f882c5c (HEAD -> master, bugfix/signup-form) Fix the bug that prevented the users from signing up.
* 9052f6f Restore toc.txt
* 5e7a828 Remove toc.txt
* a642e12 Add header to all pages.
* 50db987 Include the first section in TOC.
```

با توجه به خروجی، هر دویِ branchها به یک کامیت اشاره می‌کنن و این کامیت هم آخرین کامیت‌ هستش و همچنین با یک linear history (تاریخچه‌ی خطی) روبرو هستیم. 

### غیرفعال کردنِ fast-forwad

می‌تونیم fast-forward رو با آپشنِ `no-ff—-` غیرفعال کنیم و این کار چندین مزیت داره. پس از اینکه branchای به اسمِ `bugfix/login-form` ساختیم و کامیتی توش ثبت کردیم، دستورِ زیر رو می‌نویسیم.

```bash
git merge --no-off bugfix/login-form
```

با دستورِ بالا به گیت می‌گیم که حتی اگه fast-forward ممکن هست، این کار رو نکن. یه کامیتِ merge بساز که شاملِ تمامِ تغییراتِ target branch (همون branchای که می‌خواهیم تغییراتش رو با master branch ادغام کنیم) باشه و این کامیت ادغامِ target branch با master branch باشه.

پس از اجرایِ دستورِ بالا نیازه که commit message رو بنویسیم و ممکنه که بعد از اجرایِ دستورِ بالا ادیتورِ پیشفرض برای این کار باز بشه. پیامِ پیشفرض‌ برای کامیت `Merge branch 'bugfix/login-form' into master` هستش. 

حالا اگه log با آپشنِ graph کنیم خروجیِ زیر رو خواهیم داشت.

```
* f1f1c6f (HEAD -> master) Merge branch 'bugfix/login-form' into master
|\
| * b4697d1 (bugfix/login-form) Update toc.txt
|/
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
...
```

قبل از merge کردن master branch به f882c5c اشاره داشت. bugfix/login-form branch نیز از کامیتِ f882c5c بوجود اومده (originate شده). پس از اینکه دستورِ merge رو نوشتیم master به کامیتِ جدیدی که توسطِ همین دستورِ merge ایجاد شد (f1f1c6f)، اشاره کرد.

### مزایایِ غیرفعال کردنِ fast-forwad

حالا مزیت این روش چیه؟ چرا باید fast-forward merge رو غیرفعال کنیم؟ این مطلب یکی از اون‌هایی هست که یه‌کم بحث‌برانگیزه.

در جامعه‌ی گیت، دو نوع کاربر داریم. بعضی‌ها از merge commitها متنفر هستن و دلیل‌شون اینه که merge commitها تاریخچه رو آلوده می‌کنن و درک و خوندن اینکه چه اتفاقی داره میفته رو سخت‌تر می‌کنن. مخصوصاً وقتی که branchهایِ بیشتری رو داریم. این افراد یک تاریخچه‌ی خطی رو ترجیح می‌دن. 

گروه دیگه رو داریم که با merge commitها موافق هستن. و این رو انعکاس واقعی از تاریخچه (True reflection of history) می‌دونن و این انعکاس همون چیزی هست که وقتی branchهامون رو merge می‌کنیم اتفاق میفته. 

از نظر من هر دوی این‌ها درست هستن. قطعاً خوندنِ تاریخچه‌ی خطی راحت‌تره اما باید یادتون باشه که یه تاریخچه‌ی خطی، تاریخچه‌ی واقعیِ نیست. این کاملاً بستگی به تیم و نوعِ پروژه‌ای که روش کار می‌کنین داره. تصمیم‌گیری اینکه کدوم براتون بهتره رو به شما واگذار می‌کنم. 

علاوه بر این کامیت‌هایِ merge یک مزیتِ دیگه هم دارن. امکانِ undo کردنِ featureای رو برامون ساده‌تر می‌کنن. 

### بازنویسیِ تاریخچه

در تصویرِ زیر دو تا branch داریم: master و feature. 

branchهامون از هم جدا نیستن. پس یک مسیرِ مستقیم از feature به master هست. پس می‌تونیم در این حالت از fast-forward merge استفاده کنیم. اما ببینیم اگه از fast-forward merge استفاده نکنیم چه اتفاقی رخ می‌ده. 

پس با این توصیف پس از merge کردن با `no-ff—-` یه merge commit خواهیم داشت که تمامیِ تغییرات داخلِ feature branch رو هم شامل خواهد شد. پس اگر داخلِ feature branch دو کامیت با اسم‌هایِ F1 و F2 داشته باشیم این merge commit شاملِ تمامیِ تغییرات F1 و F2 می‌شه. 

فرض کنیم که حالا بنابه‌دلایلی می‌خواهیم همین featureای که نوشتیم رو از code baseمون پاک کنیم یا undo کنیم. می‌تونیم خیلی راحت به آخرین کامیت در master branch بریم. البته در موردِ reverting commit بعداً صحبت خواهیم کرد ولی فعلاً در موردِ‌ rewriting history (بازنویسیِ تاریخچه) صحبت می‌کنیم.

اساساً برای برگشت به یک کامیت، یک کامیتِ جدیدی رو می‌سازیم که مخالفِ کامیتِ فعلی‌مون هست. یعنی کامیتِ جدید undo شده‌ی کامیتِ فعلی‌مونه. 

پس اگه از یک merge commit استفاده کنیم در اصل یه commit داریم که بهش برگردیم. 

![Fast-forward-Merges-1.gif]({{ page.imgPath }}Fast-forward-Merges-1.gif#center)

ولی اگه از Fast-forward استفاده کنیم بعد از merge شدن master pointer به همان کامیتی اشاره خواهد کرد که feature pointer داره اشاره می‌کنه. در این حالت اگه بخواین این feature رو از code base حذف کنیم باید کامیت‌هایِ بیشتری رو revert کنیم و این می‌تونه یه‌کم پیچیده باشه. 

![Fast-forward-Merges-2.gif]({{ page.imgPath }}Fast-forward-Merges-2.gif#center)


### غیرفعال کردن fast-forward از کانفیگ

ممکنه جایی که کار می‌کنین یه سری قاعده داشته باشه که بگه باید از `no-ff—-` استفاده بشه. در این مورد برای جلوگیری از فراموش کردنِ نوشتنِ این آپشن می‌تونیم Fast-forward رو از repositoryمون غیرفعال کنیم تا دیگه هر بار مجبور به نوشتنِ این آپشن نباشیم.

دستورِ زیر fast-forward رو از repoی فعلی غیرفعال می‌کنه.

```bash
git config ff no
```

دستورِ زیر fast-forward رو در تمامِ repoها غیرفعال می‌کنه.

```bash
git config --global ff no
```