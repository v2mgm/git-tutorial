---
layout: post
title: Aborting a Merge
date: 2022-11-13 17:18:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

اگه فرصتِ رفع کردنِ conflictها رو نداشتیم می‌تونیم به حالتی برگردیم که هنوز اقدامِ به merge نکردیم. فرض کنین که وسطِ فرایندِ merge conflictها هستیم و باید conflictها رو resolve کنیم. برای اینکه merge رو لغو کنیم، دستورِ زیر رو می‌نویسیم.

```bash
git merge --abort
```

البته اگه برخی conflictها رو در فرایندِ merge رفع کرده باشیم (و هنوز کامیتی رو انجام ندادیم تا این رفعِ ابهام‌ها ثبت بشن) با دستورِ بالا اون conflict resolvingهایی که انجام دادهیم نیز از بین خواهند رفت.