---
layout: post
title: Storing Credentials
date: 2022-11-15 10:20:00 0330
# categories: "Unit1"
imgPath: ../../../assets/img/
---

هر بار که از دستورِ push استفاده می‌کنیم مجبوریم نام‌کاربری و رمز‌عبورِ گیت‌هاب رو وارد کنیم. ولی این خیلی خسته‌کننده و زمان‌بر خواهد بود. خوشبختانه این امکان هست که این دو رو روی حافظه قرار داد تا هر بار نیاز به وارد کردنشون نباشه. 

به همین منظور دستور زیر رو می‌نویسیم. در دستورِ زیر این اطلاعات رو به مدتِ 15 دقیقه کش می‌کنه و در حافظه نگهداری می‌کنه.

```bash
git config --global credential.helper cache
```

برای اینکه بتونید این اطلاعات به طور دائمِ در هاردِ سیستم‌تون نگه‌دارید، اگر سیستم‌تون مَک هست باید از Keychain و اگه سیستم‌تون ویندوز باید از Windows Credential Store استفاده کنین. هر دوشون حافظه‌ای هستند برای ذخیره‌سازیِ اطلاعاتِ مهم. در این روش، اطلاعات بصورتِ رمز‌گذاری‌شده (encrypted) ذخیره می‌شن. 

اگه در مک هستید باید چک کنین که آیا Keychain نصبه یا نه. 

```bash
git credential-osxkeychain
```

سپس، در صورتِ نصب‌ بودن، تنها کاری که باید بکنید اجرایِ دستورِ زیر هست.

```bash
git config ——global credential.helper osxkeychain
```

اگه تو ویندوز هستید باید [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager) رو نصب کنین.