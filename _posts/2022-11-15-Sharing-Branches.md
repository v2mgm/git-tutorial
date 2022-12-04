---
layout: post
title: Sharing Branches
date: 2022-11-15 11:16:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

تا حالا همه‌ی کارهامون رو رویِ master انجام دادیم. حالا بیایید روی دیگر branchها کار کنیم.

خب، مشابهِ تگ‌ها، branchها نیز private و local هستن. پس اگه می‌خواهید branchای رو با اعضایِ تیم به اشتراک بذارید مجبوریم که مثلِ تگ‌ها اون رو مستقیماً push کنیم. 

در ترمینال، branchای رو می‌سازیم و بهش سوئیچ می‌کنیم.

```bash
git switch -C feature/change-password
```

سپس دستورِ `git push` رو اجرا می‌کنیم که با خطا مواجه می‌شیم:

```
fatal: The current branch feature/change-password has no upstream brach.
To push the current branch and set the remote as upstream, use

	git push ——set-upstream ortgtn feature/change—password
```

معنایِ خطای بالا اینه که این branch با هیچ branchای در origin لینک نشده. گیت در خطایِ بالا دستوری رو برای push کردنِ این branch پیشنهاد داده. ولی قبل اجرای اون دستور بیایید دستورِ زیر رو اجرا کنیم.

```
> git branch -vv
* feature/change—password 478ac2a Add ftle1
  master                  478ac2a [origin/master] Add file1
```

همانطور که در خروجیِ دستورِ بالا مشخصه، local branch و remote tracking branch رو می‌بینیم. master همون local branch به origin/master لینک شده ولی feature/change-password branch به remote tracking branch لینک نشده. 

حالا، برای اینکه همه‌ی remote tracking branchها رو ببینیم دستورِ زیر رو اجرا می‌کنیم.

```
> git branch -r
origin/HEAD -> origin/master
origin/master
```

خب، برای لینک کردنِ private pranch به branchای در origin، برای دفعه‌ی اول مجبوریم دستورِ زیر رو بنویسیم. 

در دستورِ، آپشنِ‌ `u-` مخففِ‌ set Upstream هست. بعدِ این آپشن، remote رو مشخص می‌کنیم و سپس اسمِ private branchمون رو مشخص می‌کنیم. 

```
git push —u origin feature/change—password
```

حالا اگه دستورِ `git branch -vv` رو اجرا کنیم، خروجی‌ش بصورتِ زیر خواهد بود.

```
* feature/change—password 478ac2a [origin/feature/change—password] Add file1
  master                  478ac2a [origin/master] Add file1
```

همانطور که می‌بینید حالا local branchمون به اسمِ‌ feature/change-password با origin branch به اسمِ  origin/feature/change-password لینک شده. 

همچنین اگه دستورِ `git branch -r` رو بنویسیم خروجی‌ش بصورتِ زیر خواهد بود.

```
origin/HEAD —> origin/master
origin/feature/change—password
origin/master
```

حالا می‌تونیم مثلِ master branch با این branch هم کار کنیم. پس از اینکه کارمون با این branch تموم شد باید اون رو حذف کنیم. برای این کار از دستورِ زیر استفاده می‌کنیم.

```bash
git push -d origin feature/change—password
```

دستورِ بالا feature/change-password branch رو از origin حذف کرد. به همین خاطر خروجیِ دستورِ `git branch -r` حالا تغییر کرده.

```
origin/HEAD —> origin/master
origin/master
```

ولی در خروجیِ دستورِ `git branch -vv` همچنان feature/change-password باقی‌ست. اما عبارتِ gone مقابلِ origin/feature/change-password نوشته شده که این رو می‌رسونه که این branch حذف شده.

```
* feature/change—password 478ac2a [origin/feature/change—password: gone] Add file1
  master                  478ac2a [origin/master] Add file1
```

با وجود اینکه در origin اون branch رو حذف کردیم ولی همچنان در localمون باقی‌ست. خروجیِ دستورِ `git branch` بصورتِ زیر هست.

```
* feature/change—password
	master
```

همانطور که می‌بینید در feature/change-password قرار داریم (علامتِ *) پس نمی‌تونیم الان اون رو حذف کنیم. پس به master سوئیچ می‌کنیم.

```bash
git switch master
```

و در نهایت با دستورِ زیر feature/change-password رو حذف می‌کنیم.

```bash
git branch -d feature/change—password
```