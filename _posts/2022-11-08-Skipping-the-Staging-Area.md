---
layout: post
title: Skipping the Staging Area
date: 2022-11-08 11:54:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

**خلاصه**: مستقیم کامیتش کن بدون نیاز به بازبینی و قرار دادن در staging area. پس بجایِ `git add` از دستورِ `git commit` با آپشن‌هایِ a (همه‌ی تغییرات) و m (پیام) استفاده می‌کنیم.

```bash
git commit -a -m "Fix some bugs"
git commit -am "Fix some bugs"
```

---

یکی از مهم‌ترین سوالاتی که خیلی از تازه‌کارها دارن اینه که آیا همیشه باید تغییرات رو قبل از کامیت کردن بررسی کنیم؟ 

خُب، جواب خیر هستش.

قراره نشونتون بدم که چطور می‌تونین staging area رو رد یا skip کنین و ازش چشم‌پوشی کنین. اما اینکار رو فقط موقعی انجام بدین که می‌دونین دارین چکار می‌کنین. اگر صددرصد مطمئن هستین که تغییراتتون نیازی به بازبینی و بررسی نداره. چون این کلِ هدف داشتنِ staging area هست. 

خُب بیاین file1 رو تغییر بدیم و بعدش فقط توی یه مرحله کامیتش کنیم.

```bash
echo test >> file1.txt
```

حالا مسیرِ‌کاری‌مون کثیفه (منظور از کثیف اینه که تغییرات داشته، این یه اصطلاحِ انگلیسی هستش). پس بجایِ اجرایِ `git add` از دستورِ زیر استفاده می‌کنیم.

```bash
git commit -a -m "Fix the bug that prevented the users from signing up."
```

آپشنِ a یعنی تمامیِ فایل‌هایی که تغییر داشته. 

می‌تونیم آپشن‌ها رو بصورتِ `am-` با هم ترکیب کنیم.

```bash
git commit -am "Fix the bug that prevented the users from signing up."
```

```
[master 8f092f7] Fix the bug that prevented the users from signing up.
1 file changed, 1 insertion(+)
```

خُب کدمون کامیت شد. یه فایل تغییر داشته و یک درج رو هم داشتیم. 

این‌طوری می‌تونیم staging area رو رد کنیم اما دوباره، فقط وقتی این‌کار رو بکنین که می‌دونین چکار دارین می‌کنین. 99% مواقع باید همیشه کدتون رو قبل از کامیت کردن به ریپو stage کنین.