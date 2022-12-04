---
layout: post
title: Formatting the Log Output
date: 2022-11-08 17:30:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

خروجی دستور log رو می‌تونید سفارشی‌سازی یا customize کنین. format string رو داخلِ کوتیشن‌مارک‌ها می‌نویسیم. format string می‌تونه ترکیبی از متن‌ساده، و چند placeholder باشه. placeholderها مثل متغیرهایی هستن که توسط گیت ارائه شدن مثلِ `an%` که منظور author name هستش.

```
git log --pretty:format="hello %an"
```

توجه کنید که hello یه متنِ ساده‌ای است که در خروجیِ در هر سطری از کامیت نشون داده خواهد شد. خروجیِ‌ دستورِ‌ بالا:

```
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
```

به تعداد کامیت‌ها سطر بالا تکرار خواهد شد.

در دستور زیر، متغیرِ `H%` اشاره داره به hash یا commit ID. البته این placeholder هَش رو به صورتِ‌ کامل نمایش خواهد داد که می‌تونیم اون رو با `h%` خلاصه‌تر کرد.

```
git log --pretty:format="%an commited %H"
git log --pretty:format="%an commited %h"
```

متغیرِ‌ `cd%` مخفف Created Date هستش.

```
git log --pretty:format="%an commited %H on %cd"
```

می‌تونیم حتی خروجی `log` رو رنگی‌ هم بکنیم. در دستورِ زیر هر چیزی بعد از `Cgreen%` به رنگ سبز نمایش داده خواهند شد.

```
git log --pretty:format="%Cgreen%an commited %H on %cd"
```

برای اینکه تمامیِ متن‌هایِ بعد از author name به رنگ سبز نشون داده نشن و فقط خودِ author name به رنگ سبز باشه می‌تونیم بعد از author name از `Creset%` استفاده کنیم.

```
git log --pretty:format="%Cgreen%an%Creset commited %H on %cd"
```

می‌تونید به [داکیومنت گیت](http://git-scm.com/docs/git-log) نگاه کنین تا با تمامیِ placeholderها آشنا بشین.
