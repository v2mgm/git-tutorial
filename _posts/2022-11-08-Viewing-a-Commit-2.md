---
layout: post
title: Viewing a Commit
date: 2022-11-08 17:33:05 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

می‌تونیم به دو طریق به کامیت اشاره داشته باشیم: IDش، و اشاره‌گر HEAD.

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

دستورِ زیر جزئیات کامیتی که دو تا از Head قبل‌تر هست (555b62e) رو نمایش می‌ده.

```
git show Head~2
```

اگر می‌خواهیم تمامِ جزئیات رو مشاهده‌ نکنیم و فقط به فایلِ خاصی در کامیتِ مورد نظر تمرکز کنیم و آخرین نسخه‌ی اون فایل رو مشاهده کنیم از دستور زیر استفاده می‌کنیم.

```
git show Head~2:sections/staging-changes.txt
```

اگه می‌خواهیم اسمِ تمامی فایل‌هایی که در کامیتِ مورد نظر اضافه‌شدن، تغییرکردن یا حذف شدن رو ببینیم از دستورِ‌ زیر استفاده می‌کنیم.

```
git show Head~2 --name-only
```

و اگر می‌خواهیم علاوه بر اسمِ فایل، نوعِ‌ تغییر (A,D,M) رو هم ببینیم از آپشنِ `name-status-—` استفاده می‌کنیم.

```
git show Head~2 --name-status
```
