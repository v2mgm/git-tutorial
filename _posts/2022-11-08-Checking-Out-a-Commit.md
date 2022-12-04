---
layout: post
title: Checking Out a Commit
date: 2022-11-08 17:35:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

درباره‌ی دیدنِ فایل‌ها در کامیت صحبت کردیم. حال بعضاً می‌خوایم که یه اسنپ‌شات کلی از پروژه‌مون در اون زمانِ موردِنظر ببینیم. در این شرایط می‌تونیم یک کامیت که داریم رو checkout کنیم تا اسنپ‌شاتی که در اون کامیت هست رو بازیابی می‌کنیم و مسیر‌کاری‌مون درست مثل یک حالت خاصی در گذشته می‌شه.

برای ریستورِ working directoryمون به کامیتِ مشخصی از دستور زیر استفاده می‌کنیم.

```
git checkout dad47ed
```

البته با اجرای دستور بالا با اخطارِ `.You are in 'detached HEAD' state` روبرو خواهیم شد. این مفهومی هستش که خیلی از افراد رو گیج کرده. بذارین توضیحش بدم.

فرض کنیم اینها کامیت‌هایی هستن که تا حالا داشتیم که سمتِ چپی اولین کامیت‌مونه و راستی آخرین کامیت‌مون.

![img](../../../assets/img/Checking-Out-a-Commit-1.png#center)

همانطور که در تصویر می‌بینید هر کامیت به کامیتِ قبلِ خودش اشاره داره. و این‌طوری گیت، می‌تونه history رو حفظ کنه.

همه‌ی این کامیت‌هایی که تا حالا ساختیم بخشی از چیزی هستن که Master branch یا خطِ اصلیِ کار (Main Line of Work) می‌نامیم.

![img](../../../assets/img/Checking-Out-a-Commit-2.png#center)

در مورد branchها با جزئیات بیشتر در بخش بعدی صحبت خواهیم کرد. ولی بهتره این رو بدونین که در گیت و  برخی از Version Control Systemها که از Multiple Branch پشتیبانی می‌کنن می‌تونیم چندین branch برای کار بر رویِ بخش‌های مختلف به صورتِ ایزوله کار کنیم.

هر respository بصورتِ پیشفرض branchای به اسمِ Master داره که خطِ اصلی کار هستش. در دیگر Version Control Systemها این branch اسمش truck هست.

روشی که گیت branchها رو باهاش ارائه می‌ده استفاده از یک اشاره‌گر هستش. پس Master به آخرین کامیتی که ما تا بدینجا ساختیم اشاره می‌کنه. به محض اینکه کامیت‌های جدیدی بسازیم مستر می‌ره جلو به آخرین کامیت حال اشاره می‌کنه.

![img](../../../assets/img/Checking-Out-a-Commit-3.gif#center)

چون می‌تونیم چندین branch رو داشته باشیم گیت نیاز داره که بدونه در حالتِ فعلی روی کدوم branch داریم کار می‌کنیم. به همین خاطر اشاره‌گر ویژه‌ای داریم به اسمِ HEAD.

![img](../../../assets/img/Checking-Out-a-Commit-4.png#center)

اشاره‌گر HEDA به branchای اشاره داره که داریم روش کار می‌کنیم. که در اینجا Main branch یا Master branch هستش. این رو قبلاً در خروجی‌ِ `log` هم دیدین.

```
**>** git log --oneline
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
```

همان‌طور که در خروجیِ بالا می‌بینین Head اشاره داره به master. با ساختنِ یه کامیت به همراهِ master،‌ اشاره‌گر HEAD نیز به آخرین کامیت اشاره می‌کنه. به محض اینکه کامیت‌های جدید بسازیم این دو اشاره‌گرِ HEAD و master میرن جلو.

با checkout کردنِ کامیت‌ مورد‌نظرمون اشاره‌گرِ HEAD به اون کامیت اشاره خواهد کرد. که این کار رو detached Head می‌گن. و حالا دیگه HEAD به هیچ branch وصل نیست بلکه به کامیتِ مشخص‌شده‌ای داره اشاره می‌کنه. در این حالت نباید هیچ کامیت جدیدی رو بسازیم و باید فقط کدمون رو مشاهده کنیم و بس. چرا؟

![img](../../../assets/img/Checking-Out-a-Commit-5.png#center)

اگه در شرایطِ بالا (detached Head)، کامیتِ جدیدی رو بسازیم اون کامیت به کامیتِ قبلیش اشاره خواهد کرد که این شکلی خواهد بود و در نقطه‌ای که در تصویرِ زیر هست قرار خواهد گرفت.

![img](../../../assets/img/Checking-Out-a-Commit-6.png#center)

در جایی نیاز خواهد بود که اشاره‌گر HEAD رو به branchمون attach و وصل کنیم. و اینجاست که با مشکلی روبرو خواهیم شد. کامیتی که که در تصویرِ قبل ساخته شد و در تصویر زیر مشخص هستش، توسطِ هیچ کامیتی (قبل از خودش هیچ کامیتی بهش اشاره نداره) یا اشاره‌گری قابلِ دسترس نیست پس یک کامیتِ مرده یا Dead Commit هستش. گیت کامیت‌هایی مثل این رو به صورتِ دوره‌ای چک می‌کنه و پاکشون می‌کنه و فضا اشغال نکنن.

![img](../../../assets/img/Checking-Out-a-Commit-7.png#center)

پس کامیتِ مرده و تمامِ تغییراتِ توش رو از دست خواهیم داد. پس زمانی که در detached HEAD هستیم نباید  کامیت‌هایِ جدید بسازیم فقط باید کدمون رو نگاه کنیم (به اطراف نگاه کنیم) و تغییرات آزمایشی انجام بدیم.

برگردیم به کدمون:

```
git checkout dad47ed
```

پس از اینکه کد بالا رو اجرا کردیم دیگه در ترمینال master رو نخواهیم دید بلکه چیزی رو خواهیم دید که فعلاً HEAD بهش اشاره داره. در این مثال `master~9` رو داریم که یعنی **9 قدم عقب‌تر از آخرین کامیت هستیم**.

```
**>** git log --oneline
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

قبل از اینکه checkout کنیم خروجی `git log —oneline` بالایی بود ولی حالا اگر `git log —oneline` کنیم کامیت‌هایی که قبلاً داشتیم رو نمی‌بینیم. اون کامیت‌ها یه جورایی مخفی هستن.

```
dad47ed (HEAD) Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

برای دیدن تمامیِ اون کامیت‌های اضافه‌ای که داریم باید از یک گزینه‌ی اضافی به نامِ `all-—` استفاده کنیم.

```
**>** git log --oneline --all
a642e12 (master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed (HEAD) Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

به خروجیِ بالا دقت کنید؛ اشاره‌گرِ master جلوی آخرین کامیته اما اشاره‌گر HEAD به کامیتِ دیگری اشاره داره و دیگه به master اشاره نداره.

حال برای وصلِ master به HEAD دستورِ زیر رو می‌نویسیم.

```
git checkout master
```

حالا در برنچِ مستر هستیم و می‌تونیم کامیت‌های جدید بسازیم.
