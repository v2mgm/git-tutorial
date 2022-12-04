---
layout: post
title: Three-way Merges
date: 2022-11-12 18:27:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

ابتدا یه historyمون نگاهی بندازیم.

```
* f1f1c6f (HEAD -> master) Merge branch 'bugfix/login-form' into master
|\
| * b4697d1 (bugfix/login-form) Update toc.txt
|/
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
...
```

برای پیاده‌سازیِ feature جدید یه branch جدیدی رو می‌سازیم. 

```bash
git switch -C feature/change-password
```

دوباره به historyمون نگاهی بندازیم.

```
* f1f1c6f (HEAD -> feature/change-password, master) Merge branch 'bugfix/login-form' into master
|\
| * b4697d1 (bugfix/login-form) Update toc.txt
|/
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
...
```

حالا هر دویِ `feature/change-password` و `master` به کامیتِ یکسانی اشاره می‌کنند. حالا می‌خواهیم تجربه کنیم که چطور دو branch از هم مسیرشون از هم جدا می‌شه. 

حالا که در `feature/change-password` هستیم درش یه کامیتی رو ثبت می‌کنیم. 

```bash
echo hello > change-password.txt
git add .
git commit -m "Build the change password form."
```

حالا دوباره به historyمون نگاهی بندازیم.

```

* 03f30a6 (HEAD -> feature/change-password) Build the change password form.
* f1f1c6f (master) Merge branch 'bugfix/login-form' into master
|\
| * b4697d1 (bugfix/login-form) Update toc.txt
|/
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
...
```

با توجه به خروجیِ بالا، `feature/change-password` یک کامیت از `master` branch جلوتر هستش. ولی هنوز مسیرشون از هم جدا نشده چونکه از `feature/change-password` به `master` مسیرِ مستقیمی هست. برای اینکه مسیرِ این دو branch رو از هم جدا کنیم به `master` branch سوئیچ می‌کنیم و درش یه کامیتِ جدیدی رو می‌سازیم. 

```bash
git commit -m "Update objectives.txt"
```

حالا هر دو branch کامیتِ جدیدی رو دارن. 

```
* B0bf5c1 (HEAD -> master) Update objectives.txt
| * 03f30a6 (feature/change-password) Build the change password form.
|/
* f1f1c6f Merge branch 'bugfix/login-form' into master
|\
| * b4697d1 (bugfix/login-form) Update toc.txt
|/
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
...
```

با توجه به خروجیِ بالا `feature/change-password` branch حالا از مسیر منحرف شده و مسیرِ مستقیمی از این branch به master branch نداریم. اگه از `feature/change-password` branch شروع کنین نمی‌تونین به master برین. 

در این شرایط وقتی تغییرات رو merge می‌کنیم گیت از three-way merge استفاده می‌کنه. اگه به ابتدایِ خطوط در خروجیِ بالا نگاه کنین (ستاره‌ها) متوجهِ والدِ یکسانِ کامیت‌هایِ `03f30a6` و `B0bf5c1` خواهید شد. والدِ هردوشون `f1f1c6f` هستش. 

قراره چطوری این تغییرات با هم merge بشن و در یه کامیتِ جدیدی که merge commit هست بصورت ترکیبی قرار بگیرن.

با توجه به اینکه در master branch قرار داریم برای merge کردنِ دستورِ زیر رو می‌نویسیم.

```bash
git merge feature/change-password
```

با اجرایِ دستورِ بالا ادیتور برای نوشتنِ پیامِ کامیت اجرا می‌شه. 

اگه به خروجیِ کد بالا نگاه کنین در اینجا دیگه از fast-forward merge استفاده نشده. 

بار دیگه به historyمون نگاهی بندازیم.

```
* f4a72b2 (HEAD -> master) Merge branch 'feature/change—password' into master
|\
| * 03f30a6 (feature/change-password) Build the change password form.
* | B0bf5c1 Update objectives.txt
|/
* f1f1c6f Merge branch 'bugfix/login-form' into master
|\
| * b4697d1 (bugfix/login-form) Update toc.txt
|/
* f882c5c (bugfix/signup-form) Fix the bug that prevented the users from signing up.
...
```

با توجه به خروجیِ بالا،‌ `feature/change-password` branch به کامیتِ `03f30a6` اشاره داره `master` branch هم به `B0bf5c1` اشاره داشت. این دو تا با هم ترکیب شدن و کامیتِ جدیدِ `f4a72b2` بوجود اومده.