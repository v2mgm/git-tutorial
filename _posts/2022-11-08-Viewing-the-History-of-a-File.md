---
layout: post
title: Viewing the History of a File
date: 2022-11-08 18:56:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

ببینیم چطوری می‌تونیم تاریخچه‌ی یک فایل رو ببینیم. این‌جاهم از دستورِ log کمک می‌گیریم.

بیایین تمامیِ کامیت‌هایی که فایلِ toc.txt رو touch کرده رو پیدا کنیم.

```bash
git log --oneline toc.txt
```

می‌تونیم آمارِ تغییراتی که هر کامیت روی این فایل رو داشته با آپشنِ `stat` پیدا کنیم.

```bash
git log --oneline --stat toc.txt
```

برای اینکه تغییراتِ واقعی در این فایل رو در هر کامیت ببینیم از آپشنِ `patch` استفاده می‌کنیم.

```bash
git log --oneline --patch toc.txt
```
