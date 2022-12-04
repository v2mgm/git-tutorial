---
layout: post
title: Collaboration Workflow
date: 2022-11-15 11:49:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---
بریم یه سناریوی واقعیِ کار رویِ branchها در یه Collaboration رو ببینیم. 

فرض می‌کنیم من و اِمی، با هم روی featureای کار می‌کنیم. خب، یکی از ما باید برای این ویژگی‌ای که می‌خواهیم روش کار کنیم branchای بسازیم و اون رو به گیت‌هاب push کنیم. این، یکی از راه‌هاست. ولی یه راهِ دیگه‌ هم هست. 

می‌تونیم این branch رو مستقیماً تو خودِ‌ گیت‌هاب بسازیم. 

![Collaboration Workflow]({{ page.imgPath }}Collaboration-Workflow-1.png#center){:width="400px" height="224px"}

پس از ساختِ‌ این branch در گیت‌هاب همین branch به حالت انتخاب‌شده در خواهد آمد. در ابتدا که این branch با main branch به یه کامیتِ یکسانی اشاره دارن گیت‌هاب چنینی پیامی رو برامون نشون می‌ده.

```
This branch is even with master.
```

پیام بالا برابر بودن (اشاره به یه کامیتِ یکسان) branch فعلی رو با master branch مشخص می‌کنه. هر چقدر feature branch از master branch جلوتر بره (درش کامیت ساخته بشه یا بهش push بشه) محتوای این پیام نیز تغییر خواهد کرد.

حالا که این branch جدید رو در گیت‌هاب ساختیم کافیه برگردیم به ترمینال و این branch رو fetch کنیم.

```bash
git fetch
```

ولی اگه `git branch` کنیم فقط master branch رو در خروجی خواهیم داشت. پس چی به سر اون branchای که fetchش کردیم اومد؟

برای اون رو هم در خروجی داشته باشیم باید از آپشنِ `r-` استفاده کنیم.

```bash
> git branch -r
origin/HEAD -> origin/master
origin/feature/change-password
origin-master
```

زمانی که دستورِ fetch رو اجرا می‌کنیم فقط remote tracking branch رو دریافت می‌کنیم.

حالا باید یه private branch در local repositoryمون بسازیم تا به این remote tracking branch ای گه دریافت کردیم map بشه. به همین منظور دستورِ زیر رو می‌نویسیم.

```bash
git switch -C feature/change-password origin/feature/change-password
```

حالا می‌تونیم به این branch کامیت اضافه کنیم و به گیت‌هاب push کنیم.

حالا بریم سمتِ امی:

امی ابتدا از ریپازیتوری یه clone می‌گیره. 

```bash
git clone https://github.com/codewithmosh/Mars.git
```

حالا اگه امی در workspaceش دستورِ git branch رو اجرا کنه فقط master رو خواهد دید. امی نیز باید یه branch بسازه و اون رو با remote tracking branch نگاشت (map) کنه. حالا امی هم می‌تونه در این branch کامیت کنه و اون‌ها رو push‌ کنه.

هر دفعه که امی و من در این branch کامیت‌هایی رو push می‌کنیم باید تغییرات هر کدوم رو pull کنیم و اگه هم تداخل‌هایی وجود داشت اون‌ها رو رفع کنیم و سپس push دیگری رو بکنیم. 

پس از اینکه کارمون با این feature تموم شد باید این branch رو ببندیم.

فرض می‌کنیم که من وظیفه‌ی بستن این branch رو دارم. ابتدا با دستورِ `git pull` تغییرات امی رو دریافت می‌کنم. 

حالا این branch رو با master ادغام می‌کنیم. 

```bash
git switch master
git merge feature/change-password
```

پس از ادغام، هر دوی master branch و feature/change-password branch به آخرین کامیت اشاره خواهند داشت. ولی origin/master یه کامیت قبل‌تر از master branch هست.

برای اینکه این ادغام و تغییرات در گیت‌هاب هم باشن دستورِ `git push` رو اجرا می‌کنیم. با `git push` کردن master و origin/master به کامیتِ آخری اشاره دارن.

حالا نوبتِ بستنِ feature branch هست. 

ابتدا این branch رو (remote tracking branch) از origin حذف می‌کنیم.

```bash
git push -d origin feature/change-password
```

ولی هنوز feature/change-password branch در localمون هست. (`git branch`)

پس بیایید اون رو از local repository هم حذف کنیم.

```bash
git branch -d feature/change-password
```

حالا در سیستمِ من خروجیِ دستورِ `git branch` فقط master branch رو نشون می‌ده و خروجیِ `git branch -r` فقط Master و HEAD رو نشون می‌ده.

ولی سیستمِ امی هنوز feature/change-password رو داره. برای اینکه امی نیز تغییراتی رو که در سیستم‌م اعمال کردم رو داشته باشه `git pull` می‌کنه. حالا امی و من historyمون یکسانه. 

ولی برای اینکه feature/change-password از لوکالِ امی نیز حذف بشه دستور `git branch -d feature/change-password` رو اجرا می‌کنیم. با وجود اینکه origin/feature/change-password در ریموت نیست در خروجیِ دستورِ `git branch -r` سیستمِ امی هستش.

برای حذف remote tracking branchای که در remote نیستش از دستورِ زیر استفاده می‌کنیم.

```bash
git remote prune origin
```

حالا origin/feature/change-password (همون remote tracking branchمون) هرس (prune) شد.