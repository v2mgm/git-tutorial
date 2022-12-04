---
layout: post
title: Pull Requests
date: 2022-11-19 10:20:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---
اغلب، در پیاده‌سازیِ feature یا رفعِ باگ، تمایل داریم که دیگر اعضایِ تیم نیز در مورد کدمون فیدبک بدن. و اینجا همون جایی هست که از pull request استفاده می‌کنیم. 

با pull request قبل از ادغامِ کد به master تیم در موردش بحث و بررسی انجام می‌دن.

برای مثال، فرض کنیم اِمی داره featureای رو پیاده‌سازی می‌کنه. پس اِمی تو ماشینِ خودش، یه branch جدیدی رو می‌سازه، کامیتی رو بهش اضافه می‌کنه و سپس اون رو به گیت‌هاب push می‌کنه. 

```bash
git switch -C feature/login
echo hello > file3.txt
git add .
git commit -m "Write Hello to file3"
```

پس از کدهایِ بالا، با دستورِ‌ زیر branch رو push می‌کنیم. برای بار اول، آپشنِ u- رو برای سِت کردن upstream branch استفاده می‌کنیم. سپس آرگومان‌هایِ origin و branch رو مشخص می‌کنیم. 

```bash
git push —u origin feature/login
```

حالا در گیت‌هاب با پیغامِ زیر روبرو می‌شیم.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-1.png#center){:width="600px" height="96px"}

می‌تونیم Compare & pull request کنیم و یا می‌تونیم همین کار رو از طریقِ تبِ Pull request و دکمه‌ی New pull request استفاده کنیم. 

در صفحه‌ی pull request دو branch رو مشخص می‌کنیم: base branch و compare branch.

اغلب base branch همون master هست و compare branch یا target branch رو هم feature/login branch انتخاب می‌کنیم. 

![Pull-Requests]({{ page.imgPath }}Pull-Requests-2.png#center){:width="600px" height="132px"}

البته چون در این branch فقط یه فایل جدید قرار دادیم همانطور که در تصویرِ بالا می‌بینید conflictای رو نداریم و آماده هست برای merge. ولی قبل اینکه این branch رو به master ادغام کنیم می‌خواهیم pull request و یا با تیم در مورد این تغییرات بررسی‌ای رو داشته باشم.

اگه صفحه‌ی compare (تصویرِ بالا) رو در مرورگر به سمتِ پایین اسکرول کنیم (تصویر پایین) خلاصه‌ای از تغییرات رو خواهیم دید. در این مثال، یک کامیت داریم، یه فایل تغییر داده شده، هیچ کامنتی نیست و یه contributer هستش.

سپس، کامیتی رو داریم که pushش کردیم. سپس خلاصه‌ی تغییرات رو می‌بینیم.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-3.png#center){:width="600px" height="293px"}

حالا برای pull request کردن، رویِ دکمه‌ی Create pull request کلیک می‌کنیم. 

با توجه به اینکه در این feature branch فقط یه کامیت هست گیت‌هاب از پیامِ همین یه دونه کامیت برای عنوانِ pull request استفاده می‌کنه. که البته می‌تونیم اون رو تغییر بدیم. و سپس اون چیزایی رو که مشخصاً می‌خواهیم توسطِ دیگر افراد بررسی بشه رو توی توضیحاتِ pull request، لیست می‌کنیم و در نهایت رویِ دکمه‌ی Create pull request کلیک می‌کنیم.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-4.png#center){:width="600px" height="426px"}


 حالا یه دونه pull request داریم. همانطور که در تصویرِ زیر می‌بینید مشخص شده که در این pull request، کاربر codewithmosh می‌خواد یه کامیت رو از feature/login به master ادغام کنه.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-5.png#center){:width="600px" height="162px"}

حالا باید یکی از collaboratorها رو به عنوانِ reviewer انتخاب کنیم و بهش درخواستِ بررسیِ تغییرات رو بدیم. برای این کار از بخشِ Reviewers استفاده می‌کنیم.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-6.png#center){:width="400px" height="145px"}


آیکون زرد رنگ به این معنی است که این درخواست از reviewer (در این مثال mosh-hamedani) در حالت انتظار هست. حالا این reviewer یک ایمیل با این محتوا که «امی نیاز به بررسی‌ات داره» دریافت می‌کنه. 

حالا اگه از دیدِ reviewer گیت‌هاب رو باز کنیم این شخص یه open pull request داره. حالا این mosh-hamedani می‌تونه review خودش رو در مورد تغییرات بنویسه. می‌تونه برای هر خط از تغییرات به صورتِ جدا review قرار بده. این کار رو می‌تونه با کلیک رویِ علامتِ plus در کنارِ هر خط کد انجام بده. 

در نهایت رویِ دکمه‌ی Finish your review کلیک می‌کنه و توضیحاتِ کلی‌ش رو می‌نویسه. می‌تونه این توضیح کلی رو به عنوانِ Comment در نظر بگیره یا با این pull request موافقت کنه و این توضیح رو به عنوانِ approve مشخص کنه و یا با انتخابِ گزینه‌ی Request changes درخواستِ تغییراتی رو داشته باشه.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-7.png#center){:width="600px" height="313px"}

در این مثال گزینه‌ی Reuest Changes انتخاب می‌شه.

حالا اگه به تَبِ Conversation بریم Time line مربوط به چیزایی که تا حالا اتفاق ا

در ابتدا اِمی (البته در اینجا codewithmosh) یه pull request داشته. سپس initial commit (کامیتِ اولیه) رو مشخص می‌کنیم. سپس، اِمی از mosh-hamedani درخواستِ review کرده. بعدش، mosh-hamedani درخواستِ تغییراتی رو داشته که جزئیاتِ مربوطه رو هم می‌‌بینیم.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-8.png#center){:width="600px" height="358px"}

دوباره برگردیم به سیستمِ شخصیِ اِمی. دوباره تغییراتی رو بدیم و push کنیم. 

```bash
echo Hello > file3.txt
git commit -am "Capitalize Hello."
git push
```

دوباره برگردیم به گیت‌هاب. امی این‌بار رویِ دکمه‌ی Re-request review کلیک می‌کنه تا دوباره درخواستِ بررسی کد رو کنه. و این کار دوباره برای mosh-hamedani نوتیفیکیشن و ایمیلِ جدیدی رو ارسال می‌کنه.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-9.png#center){:width="600px" height="112px"}

حالا mosh-hamedani دوباره تغییرات رو review می‌کنه و رویِ دکمه‌ی Review Changes کلیک می‌کنه تا final reviewش رو پیشنهاد بده و این بار این توضیحات رو با انتخابِ گزینه‌ی Approve ارائه می‌ده.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-10.png#center)


حالا کنارِ اسمِ reviewer علامت تیک رو می‌بینیم. 

حالا در انتهایِ Time line می‌تونیم رویِ دکمه‌ی Merge pull requst کلیک کنیم و این pull request رو close کنه.

به سه نوع می‌شه این merge انجام بشه.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-11.png#center){:width="600px" height="96px"}

حالا که merge انجام شد می‌تونیم این branch رو حذف کنیم.

![Pull-Requests]({{ page.imgPath }}Pull-Requests-12.png#center){:width="600px" height="78px"}


البته اگه مشکلی بود می‌تونیم دوباره همین branch رو restore کنیم. 

![Pull-Requests]({{ page.imgPath }}Pull-Requests-13.png#center)

حالا برگردیم به سیستمِ امی. اِمی به master branch سوئیچ می‌کنه، سپس pull می‌کنه.

```bash
git switch master
git pull
git log --oneline --all --graph
```

البته همانطور که origin/feature/login branch رو در سمتِ گیت‌هاب حذف کردیم در local repository نیز اون رو حذف می‌کنیم. برای این کار ابتدا از دستورِ زیر استفاده می‌کنیم. این دستور، اون brachهایی که در origin نیستن رو از local نیز حذف می‌کنه. در اینجا ابتدا با دستورِ زیر origin/feature/login رو از لوکال حذف می‌کنیم.

```bash
git remote prune origin
```

حالا اگه دستورِ `git remote -r` رو اجرا کنیم خواهیم دید که remote tracking branchای به اسمِ origin/feature/login رو نداریم.

در نهایت feature/login رو از local هم حذف می‌کنیم.

```bash
git branch -d feature/login
```

### چه کسی باید pull request رو merge کنه؟

دو دیدگاه در این مورد هست. برخی از تیم‌ها بر این نظر هستن که همون فردی که pull request رو کرده نباید این request رو ببنده. pull request همیشه باید توسطِ شخصِ دیگری بسته بشه. در غیر اینصورت این pull request بی‌معنی خواهد بود. 

نظر دیگه‌ای که در این مورد هست اینه که همون شخصی که pull request رو کرده باید همون هم این درخواست رو پایان بده. چون همون شخص از تغییرات آگاه‌تره و در صورتِ وجودِ conflictها می‌تونه اون‌ها رو رفع کنه. 

هیچ یک از این دو نظر رو نمی‌شه خوب و بد دانست و انتخاب هر یک بستگی به روشِ کار تیم داره.