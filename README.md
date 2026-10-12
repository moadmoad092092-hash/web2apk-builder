# قالب Web2APK — مستودع بناء APK عبر GitHub Actions

هذا المستودع هو القالب الذي تستخدمه منصة Web2APK AI لبناء تطبيقات Android حقيقية.

## خطوات الإعداد

1. أنشئ مستودعًا جديدًا على GitHub (عام أو خاص — البناء مجاني على العامة).
2. انسخ كل ملفات هذا المجلد إلى المستودع بنفس البنية:
   - `.github/workflows/build-apk.yml`
   - `build.gradle`, `settings.gradle`
   - مجلد `app/` كاملًا
   - مجلد `inputs/`
3. أنشئ رمز وصول (Personal Access Token):
   - GitHub → Settings → Developer settings → Personal access tokens → Fine-grained.
   - اختر المستودع الجديد فقط، وبصلاحيات:
     - Contents: Read and write
     - Actions: Read and write
4. أضف القيمتين في صفحة Secrets في لوحة تحكم تطبيق Web2APK AI:
   - `GITHUB_REPO` بصيغة `اسم_المستخدم/اسم_المستودع`
   - `GITHUB_TOKEN` الرمز السري
5. جرّب أول تحويل من الموقع — سيبدأ البناء في تبويب Actions بالمستودع، وعند اكتماله يظهر رابط تنزيل APK في صفحة المشروع.

## كيف يعمل

- دالة Web2APK AI ترفع الأيقونة وشاشة البداية إلى مجلد `inputs/` ثم تُطلق سير العمل `build-apk.yml` عبر `workflow_dispatch`.
- سير العمل يعدّل اسم التطبيق ومعرّف الحزمة واللون، يبني APK بـ Gradle، ثم ينشئ Release باسم `build-<run_id>` ويُرفق ملف APK فيه.
- دالة المتابعة تستعلم عن حالة العملية، وعند النجاح تجد أصل (asset) ملف APK في الـ Release وتُسجّل رابط تنزيل آمن.