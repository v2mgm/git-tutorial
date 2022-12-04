---
layout: post
title: Cloning a Repository
date: 2022-11-14 13:07:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---
حالا repositoryمون رویِ اینترنت هست. خب، هر شخصی از تیم‌مون باید این ریپو رو clone کنه. این یعنی، باید یک کپی از ریپو تهیه کنه و اون رو در سیستمِ شخصی‌ش قرار بده. و بصورتِ local روی ریپو کار کنه و وقتی که تغییرات برای به اشتراک‌گذاری آماده بودن اون کامیت‌ها رو به Central Repository (ریپویِ‌ مرکزی، یا ریموت ریپو) push کنه.

برای clone کردنِ ریپو، url مربوط به ریپو رو کپی می‌کنیم و سپس از دستورِ `clone` استفاده می‌کنیم.
![Cloning-a-Repository]({{ page.imgPath }}Cloning-a-Repository-1.png#center)

```bash
git clone https://github.com/codewithmosh/Mars.git
```

با اجرایِ دستورِ بالا، گیت یک local repository با همون اسمِ Remote Repository خواهد ساخت ولی اگه می‌خواهید با اسمِ متفاوت‌تری local repository ساخته بشه می‌تونید بصورتِ زیر عمل کنید.

```bash
git clone https://github.com/codewithmosh/Mars.git MarsProject
```

با اجرایِ دستورِ بالا تمامیِ کامیت‌هایِ remote repository در سیستمِ شخصی‌مون بصورتِ local قرار خواهد گرفت.

حالا `git log` می‌کنیم.

```
> git log ——oneline —-all ——graph
* fb3b343 (HEAD -> master, origin/master, origin/HEAD) Initial commit
```

با توجه به خروجیِ بالا، علاوه بر دو تا اشاره‌گر HEAD و master، دو اشاره‌گرِ دیگه‌ای رو هم داریم. 

زمانی که ریپویی رو clone می‌کنیم گیت source repository رو به اسمِ origin درمیاره. origin ارجاعی است به source repository. 

origin/master مشخص می‌کنه که master branch در ریپویِ origin کجا قرار گرفته. و اصطلاحاً این Remote tracking branch نامیده می‌شه. این branch هستش ولی نه از اون branchهایی که قبلاً دیدیم. و این یعنی نمی‌تونیم اون رو check out یا سوئیچ کنیم، یا نمی‌تونیم درش کامیت کنیم. 

برای مثال اگه دستورِ `git switch origin/master` رو اجرا کنیم با خطا روبرو می‌شیم.

اگه با `git branch` بخواهیم branchهامون رو لیست کنیم در خروجی فقط یه دونه master رو خواهیم داشت.

پس، origin/master اصطلاحاً Remote tracking branch هست.

مشابه همین origin/HEAD رو داریم که محلِ اشاره‌گرِ HEAD رو در ریپویِ originمون مشخص می‌کنه.

دستورِ کاربردی‌ای رو داریم که می‌تونیم باهاش remote repositoryها رو لیست کنیم.

```bash
git remote
```

Remote Repository ریپویی هستش که تو سیستم‌ِ شخصیِ ما نیست، دقیق‌تر بخواهیم بگیم داخلِ دایرکتوریِ کنونی‌مون نیست.

برای دیدنِ جزئیاتِ بیشتر در مورد remote repositoryها از آپشنِ `v-` که مخففِ Verbose (طولانی‌مطلب، درازنویس) هست استفاده می‌کنیم.

```bash
git remote -v
```

خروجیِ دستورِ بالا:

```bash
origin https://github.com/codewithmosh/Mars.git (fetch)
origin https://github.com/codewithmosh/Mars.git (push)
```

با توجه به خروجیِ بالا، origin به ریپویِ روبرویِ خودش ارجاع داره. این urlای هست که گیت زمانی که نیاز به این remote repository هست ازش استفاده می‌کنه.