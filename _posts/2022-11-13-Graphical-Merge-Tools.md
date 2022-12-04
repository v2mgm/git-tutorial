---
layout: post
title: Graphical Merge Tools
date: 2022-11-13 17:16:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

راستش؛ VSCode ابزار خوبی برای حل کردنِ conflictها نیستش. ابزارهایِ دیگه‌ای هم برای این کار هست که معروف‌ترین‌هاش Kdiff، P4Merge و WinMerge هستش. البته اگه از GitKraken و یا از IDE قوی‌ای مثلِ IntelliJ استفاده می‌کنید نیازی به این ابزارها نیست. 

در این آموزش می‌خواهیم از [P4Merge](https://www.perforce.com/products/helix-core-apps/merge-diff-tool-p4merge) استفاده کنیم تا conflictها رو برطرف کنیم. 

پس از نصبِ P4Merge، این ابزار رو به عنوانِ ابزارِ پیشفرض برای merge کردن کانفیگ می‌کنیم. به همین منظور از دستورِ زیر استفاده می‌کنیم.

```bash
git config --global merge.tool p4merge
```

پس از اجرای دستورِ بالا مسیرِ p4merge رو هم برای گیت مشخص می‌کنیم. 

```bash
git config --global mergetool.p4merge.path "C:\ProgramFiles\p4merge\p4merge.exe"
```

حالا اگه پس از اجرایِ دستورِ `git merge` و سپس اسمِ branch، با conflict روبرو شدیم می‌تونیم دستورِ زیر رو برایِ resolve کردنِ conflict بنویسیم.

```bash
git mergetool
```

با اجرایِ دستورِ بالا ابزارِ P4Merge اجرا خواهد شد. 

منظور از local یعنی همون master branch یا همون branchای که الان توش هستیم. 

پس از اینکه conflictها توسطِ این ابزار رفع کردیم برمی‌گردیم به ترمینال و تغییرات رو کامیت می‌کنیم.

```bash
git add .
git commit
```