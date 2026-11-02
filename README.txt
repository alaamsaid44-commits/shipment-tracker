# Shipment Management Cloud

واجهة عربية أولية متصلة بمشروع Supabase:
- Project URL و Publishable Key مضمنان في الواجهة.
- تسجيل دخول بالبريد وكلمة المرور عبر Supabase Auth.
- الشحنات، المصروفات، فواتير الموردين، مكاتب التخليص، المستفيدون، وسجل المتابعة.
- تعتمد على الجداول وسياسات RLS التي أنشأتها في مشروع Supabase.

## تشغيل محلي للاختبار
افتح مجلد المشروع في VS Code وشغّل خادمًا محليًا مثل Live Server. لا تعتمد على فتح الملف مباشرة عبر file://.

## النشر
ارفع `index.html` إلى استضافة صفحات ثابتة مثل Netlify أو Cloudflare Pages أو Vercel (static).
بعد النشر أضف عنوان الموقع إلى Supabase > Authentication > URL Configuration:
- Site URL
- Redirect URLs

## إدارة المستخدمين
أنشئ حساب الموظف من Supabase > Authentication > Users. سيُنشأ له profile بدور viewer تلقائيًا.
لتغيير صلاحية موظف، نفّذ من SQL Editor (استبدل UUID):
UPDATE public.profiles SET role='editor' WHERE id='USER-UUID';
الأدوار المتاحة: admin / editor / viewer.

## تنبيهات مهمة
- هذه نسخة أولية للتجربة وليست اعتمادًا نهائيًا لبيانات مالية حقيقية.
- لا تضع service_role أو Secret Key في الواجهة.
- لا تشارك Database Password.
- راجع سياسات RLS واختبر صلاحيات القراءة والكتابة والحذف بحسابات مختلفة قبل التشغيل الفعلي.
- فواتير الموردين تدعم حاليًا رأس الفاتورة؛ جدول تفاصيل الأصناف supplier_invoice_items موجود في قاعدة البيانات ويحتاج واجهة إدخال متعددة البنود في مرحلة لاحقة.
- لا يوجد ترحيل تلقائي لبيانات localStorage القديمة في هذه النسخة.
