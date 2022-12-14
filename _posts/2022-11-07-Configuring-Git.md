---
layout: post
title: Configuring Git
date: 2022-11-07 22:38:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---
در استفاده‌ی اول از گیت باید یه سری کانفیگ‌ها رو براش تعیین کنیم. باید اسم، ایمیل و ادیتورِ پیشفرض‌مون (Default Editor) و اینکه نحوه‌ی هندل کردنِ پایان خط‌ها (Line Endings) رو براش مشخص کنیم. 

می‌تونیم تنظیمات رو در سه سطح انجام بدیم:

- System Level

تنظیماتی که در این سطح انجام می‌شه برای همه‌ی کاربرهایِ سیستمِ فعلی اعمال می‌شه.

- Global

تنظیماتِ در این سطح، رویِ تمامیِ ریپوهایِ کاربرِ فعلی اعمال می‌شه.

- Local

تنظیماتِ این سطح فقط رویِ ریپویِ کنونی یا ریپویِ موجود در پوشه‌ی فعلی اعمال می‌شه.

در ترمینال، دستوراتِ زیر رو می‌نویسیم. در دو دستورِ زیر گزینه‌هایِ `user.name` و `user.email` رو کانفیگ کردیم

```
git config --global user.name "vahid"
```

```
git config --global user.email v2mgm@yahoo.com
```

حالا نوبتِ تنظیمِ کدادیتورِ پیشفرض‌مون هست. 

در اینجا از VSCode برای این منظور استفاده می‌کنیم. برای اینکه بتونیم تنها با نوشتنِ اسمِ فایلِ اجراییِ VSCode در هر مسیرِ ویندوز اون رو اجرا کنیم فایل‌ اجرایی‌ش رو در path ویندوز اضافه می‌کنیم. با این کار می‌تونیم تو هر جایی از سیستم بدونِ مشخص کردنِ مسیرِ کلی‌ش VSCode رو بازش کنیم. اسمِ فایلِ اجراییِ ادیتورِ وی‌اس‌کُد `Code.exe` هستش، پس اگر بنویسیم `code` وی‌اِس‌کُد برامون باز خواهد شد.

```
git config --global core.editor "code --wait"
```

با فلگِ wait به ترمینال می‌گیم که تا زمانی که صفحه‌ی جدیدِ وی‌اِس‌کُد رو نبستیم منتظر بمونه.

تمامیِ این پیکربندی‌ها در یک فایلِ تکست ذخیره می‌شن. این فایل رو می‌تونیم با ادیتورِ پیش‌فرض‌مون که وی‌اس‌کُد هست ویرایش‌ کنیم. برای اینکه فایلِ پیکربندی رو ببینیم دستورِ زیر رو اجرا می‌کنیم.

```
git config --global -e
```

با اجرایِ دستورِ بالا فایلِ تنظیمات سطحِ global در ادیتورِ وی‌اس‌کُد باز خواهد شد و ترمینال تا زمانی که این پنجره‌ی VSCode رو نبستیم، منتظر خواهد ماند.

در قدمِ بعدی می‌خوایم که پیکربندی کنیم که گیت چطوری باید انتهایِ خطوط رو تنظیم کنه. این یک تنظیم خیلی مهمی هستش که کلی از مردم فراموشش می‌کنن اون رو انجام بدن.

|---|---|
|  ![img]({{ page.imgPath }}Configuring-Git-1.png#center){:width="250px" height="240px"}  |  ![img]({{ page.imgPath }}Configuring-Git-2.png#center){:width="250px" height="134px"} |

در ویندوز انتهایِ خط‌ها با دو کاراکترِ خاص تموم می‌شه: carriage return و line feed.

در مک و لینوکس انتهایِ خطوط با line feed مشخص می‌شه.

اگر انتهایِ خطوط رو درست تنظیم نکنیم با مشکلات زیادی روبرو می‌شیم. برای جلوگیری از این مشکلات باید یک property به‌نامِ‌ core.autocrlf (مخففِ carriage return و line feed) رو کانفیگ کنیم. 

بیاین فرض کنیم دو نفر به اسمِ جان و جولی هستن که رویِ یک ریپو کار می‌کنن. جان از ویندوز استفاده می‌کنه و جولی از مک. و همانطور که گفتم در ویندوز انتهایِ خطوط با carriage return و line feed تموم می‌شن. پس زمانی ‌که جان می‌خواد کدش رو داخلِ ریپو چک کنه گیت باید carriage return رو از انتهایِ خطوط پاک کنه. به همین ترتیب زمانی که کدش رو از ریپو چک می‌کنه گیت باید انتهایِ خطوط رو آپدیت کنه و carriage return رو اضافه کنه. برای رسیدن به این رفتار در ویندوز، باید این property رو با true مقداردهی کنیم. 

از طرفِ دیگه وقتی جولی کد رو چک می‌کنه، نمی‌خواد که انتهایِ خطوط carriage return باشه. اگر چه شاید بخاطر ادیتوری که جولی ازش استفاده می‌کنه به صورتِ‌ تصادفی به انتهایِ خطوط carriage return اضافه شده باشه. به هر حال گیت باید زمانی که کد رو در رپیو ذخیره می‌کنه انتهایِ خطوط رو درست کنه. برای رسیدن به این رفتار در مَک و لینوکس، باید property رو با input مقداردهی کنیم. که بدین معناست گیت باید انتهایِ خطوط رو وقتی که کد رو در رپیو ذخیره می‌کنه درست کنه.

برگردیم به ترمینال.

```shell
git config --global core.autocrlf true
```

```shell
git config --global core.autocrlf input
```
