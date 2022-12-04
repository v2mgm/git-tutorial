---
layout: post
title: Removing Files
date: 2022-11-08 12:01:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**:‌ وقتی فایلی رو با دستورِ `rm` از مسیرِ‌کاری حذف می‌کنیم باید همون فایل یا فایل‌ها یا period با دستورِ `git add` از staging area هم حذف کنیم. بجای این دوباره کاری می‌تونیم از دستورِ `git rm` استفاده کنیم. 

---

بیاین بگیم که متوجه شدیم که دیگه file2 رو در پروژه‌مون نمی‌خوایم چون کد‌هایِ بلااستفاده داره. 

دستورِ زیر رو برای حذفِ این فایل می‌نویسیم. دستورِ زیر یه دستورِ گیت نیست چون با گیت شروع نمی‌شه. دستور زیر دستورِ استاندارد یونیکس هست. 

```bash
rm file2.txt
```

حالا مسیرِ کاری‌مون dirty شده. `git status` رو اجرا می‌کنیم.

```
On branch master
Changes not staged for commit:
	(use "git add/rm <file>..." to update what will be committed)
	(use "git restore <file>..." to discard changes in working directory)
		
			deleted:     file2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

فقط یه دونه تغییر داشتیم که هنوز برای کامیت شدن stage نشده. File2.txt رو از Working Directory پاک کردیم ولی هنوز در Staging area هستش. با دستور زیر این رو ثابت می‌کنیم.

```bash
git ls-files
```

```bash
file1.txt
file2.txt
```

هر موقع که تغییراتی رو انجام می‌دیم باید اون تغییرات رو با `git add` به اصطلاح Stage کنیم.

```bash
git add file2.txt
```

 حالا با دستورِ بالا file2.txt در staging area هم دیگه نیست. خروجیِ `git status` هم زیری خواهد بود.

```bash
On branch master
Changes to be committed:
	(use "git restore -—staged <file>..." to unstage)
		deleted: file2.txt
```

یه تغییر داریم که آماده‌ی کامیت هست. 

```bash
git commit -m "Remove unused code."
```

```
[master 138c8ef] Remove unused code.
1 file changed, 1 deletion(—)
delete mode 100644 file2.txt
```

پس باید file2.txt رو هم از مسیرِکاری پاکش کنیم و هم از staging area. چون این یک عملِ رایجه. گیت به ما یک دستور برای انجام هر دوشون بصورتِ یکجا می‌ده. 

```bash
git rm file2.txt
```

بجایِ استفاده از `rm` استانداردِ یونیکس از `git rm` استفاده می‌کنیم. و البته می‌تونیم این دستور رو رویِ چندین فایل انجام بدیم.

```bash
git rm file2.txt file1.txt
```

همچنین می‌تونیم از pattern هم استفاده کنیم.

```bash
git rm *.txt
```

با این دستور، گیت فایلِ مورد نظر رو هم از working directory و هم از staging area پاک می‌کنه.