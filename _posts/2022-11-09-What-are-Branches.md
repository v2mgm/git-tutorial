---
layout: post
title: What are Branches
date: 2022-11-09 10:56:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

branching به ما اجازه‌ی خروج از خطِ اصلیِ کار (Main line of work) و کار بر روی یک چیزِ دیگه در انزوا (isolation) می‌ده.


![img]({{ page.imgPath }}What-are-Branches-1.gif#center)

به صورتِ مفهومی می‌تونین به branching مثل یک فضایِ کاری مجزا فکر کنین. فضای کاری اصلی‌مون رو همچنان داریم که master نامیده می‌شه. می‌تونیم یک فضایِ کاری دیگه‌ای رو هم داشته باشیم و درش بصورتِ مجزا رویِ یک ویژگی (feature) جدید کار کنیم. زمانی که این ویژگیِ جدید رو توسعه می‌دیم ممکنه کدمون ناپایدار بشه و نمی‌خوایم که اون کد رو در فضایِ اصلیِ کاری‌مون منتشر کنیم. پس روی این فضایِ کاری، بصورتِ جدا کار می‌کنیم تا زمانی که کدمون تست شد و تمامیِ باگ‌ها رفع شد و کدمون بخوبی کار کرد و بعدش تغییرات داخل این فضای کاری رو master می‌بریم که به این کار merging می‌گن. 

پس branching به ما اجازه‌ی کار بر رویِ آیتم‌های مختلفِ کاری بدون به‌هم‌زدن خطِ اصلی کار (main line of work) رو میده. خطِ اصلی رو تا حد ممکن پایدار نگه می‌داریم تا هر زمانی که خواستیم منتشرش کنیم. همچنین هر کسی که به تیم ما می‌پیونده می‌تونه از یک کد پایدار شروع کنه. این ایده‌ی branchingـه.

![img]({{ page.imgPath }}What-are-Branches-2.gif#center)

راهی که گیت برای مدیریت branching در نظر گرفته خیلی با سیستم‌هایِ مدیریتِ نسخه‌ی دیگه مثلِ subversion متفاوته. در subversion زمانی که یک branch جدید می‌سازیم یک کپی کامل از کل مسیرِ کاری‌مون می‌گیره و یه جایِ دیگه ذخیره‌ش می‌کنه. اگر صدها و یا هزاران فایل در پروژه‌مون داشته باشیم چی؟ تمامی این فایل‌ها کپی خواهند شد و این عمل می‌تونه زمان‌بر باشه برای همینم هست که کاربران subversion از branching متنفرن. چون کُند هستش و می‌تونه کلی فضا اشغال کنه. 

branchها در گیت بسیار سریع و ساده هستن. چون **branch کردن در گیت فقط اشاره‌ کردنِ به کامیت هست.** master branch فقط یک اشاره‌گر به آخرین کامیت در خطِ اصلی کار هستش. به محض اینکه کامیت‌های جدیدی می‌سازیم، گیت این اشاره‌گر رو به صورتِ خودکار به جلو حرکت می‌ده. یعنی می‌دونه که در آخرین کدِ خطِ اصلی چی هستش. این snapshotای است که در این کامیت ذخیره می‌شه. 

**زمانی که branch جدیدی رو می‌سازیم گیت یک اشاره‌گر جدید می‌سازه که می‌تونه به اطراف حرکت کنه. این اشاره‌گر فقط یک فایلِ کوچیک هستش که شاملِ یک آی‌دیِ 40بایتی هست.** برای همین هم هست که ساختِ branch در گیت بسیار سریعه.

زمانی که به Feature branch (در تصویر زیر) سوئیچ می‌کنیم و کامیت‌های جدیدی رو می‌سازیم گیت این اشاره‌گر رو به جلو حرکت می‌ده و اشاره‌گر master سرجایِ خودش می‌مونه تا گیت بدونه آخرین کد در هر branch کجاست.

دوباره که به master branch سوئیچ کردیم گیت snapshotای که اشاره‌گرِ master داره به کامیتش اشاره داره رو می‌گیره و مسیرِ‌کاری‌مون رو به اون snapshot ریست می‌کنه تا همیشه یک مسیرِ کاری داشته باشیم.

حالا، گیت چطور می‌فهمه که داریم روی کدوم branch کار می‌کنیم؟‌ با استفاده از یک اشاره‌گر خاص به اسمِ **HEAD**. این اشاره‌گر نیز یک نوع فایل هست که شاملِ نامِ یک branch هست (مثلِ master) 

وقتی که به یه branchی سوئیچ می‌کنیم، گیت اشاره‌گرِ HEAD رو اون branch می‌بره و اون فایلِ کوچیکِ HEAD رو نیز با اسمِ branchای که داره بهش اشاره می‌کنه، آپدیت می‌کنه. و این‌طوری می‌تونیم branchای که داخلش هستیم رو پیدا کنیم.

![img]({{ page.imgPath }}What-are-Branches-3.gif#center)

در طول این بخش قراره که همه چیز رو در مورد کار با branchها یاد بگیرین.