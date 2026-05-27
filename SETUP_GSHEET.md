# 🗂️ راه‌اندازی Google Sheets (اختیاری)

اگر میخوای آگهی‌ها علاوه بر تلگرام در Google Sheets هم ذخیره بشن، این مراحل رو دنبال کن.

---

## مرحله ۱ — ساخت Service Account در Google Cloud

1. برو به [console.cloud.google.com](https://console.cloud.google.com)
2. یه **پروژه جدید** بساز (یا از موجود استفاده کن)
3. از منوی کناری برو به:  
   `APIs & Services → Library`  
   - **Google Sheets API** رو فعال کن  
   - **Google Drive API** رو فعال کن
4. برو به:  
   `APIs & Services → Credentials → Create Credentials → Service Account`
5. اسم بده (مثلاً `job-bot`) و بساز
6. روی Service Account کلیک کن → تب **Keys** → **Add Key → JSON**
7. فایل JSON دانلود میشه — این فایل رو نگه دار

---

## مرحله ۲ — ساخت Google Sheet

1. یه [Google Sheet جدید](https://sheets.new) بساز
2. اسم Sheet اول رو به **Jobs** تغییر بده
3. از URL شیت، **ID** رو کپی کن:  
   `https://docs.google.com/spreadsheets/d/` **`این-قسمت-ID-هست`** `/edit`
4. دکمه **Share** رو بزن و ایمیل Service Account رو با دسترسی **Editor** اضافه کن  
   (ایمیل در فایل JSON توی فیلد `client_email` هست — شبیه: `job-bot@project.iam.gserviceaccount.com`)

---

## مرحله ۳ — اضافه کردن Secrets به GitHub

برو به `Settings → Secrets → Actions → New repository secret`:

| نام Secret | مقدار |
|---|---|
| `GSHEET_CREDENTIALS` | **کل محتوای** فایل JSON (کپی همه چیز از `{` تا `}`) |
| `GSHEET_ID` | ID شیت که از URL کپی کردی |

> ⚠️ اگه این دو Secret رو اضافه نکنی، بات بدون مشکل کار میکنه — فقط بخش شیت رو skip میکنه.

---

## خروجی نهایی شیت

| Job Title | Company | Apply Link | Posted Date | City | Country | Salary | Saved At (UTC) |
|---|---|---|---|---|---|---|---|
| Junior SEO Specialist | Acme Inc | https://... | 2025-05-27 | Remote | US | $50,000/yr | 2025-05-27 07:30 |
