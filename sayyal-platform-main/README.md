# سيّال | Sayyal — Prototype

طبقة سوق ثانوي للاستثمارات غير السائلة الموجودة عبر منصات التمويل الجماعي بالدين.
نموذج تجريبي (Prototype) — وليس منتجًا إنتاجيًا.

---

## التشغيل

```bash
npm install
npm run dev        # http://localhost:3000
```

للإنتاج:

```bash
npm run build && npm run start
```

لا يحتاج المشروع إلى أي API keys أو Backend. كل شيء يعمل محليًا عبر mock data و local state.

---


---

## البنية التقنية

- **Next.js 15** (App Router) + **TypeScript** + **Tailwind CSS**
- **Framer-free**: حركات CSS خفيفة بدل مكتبات ثقيلة، مع `prefers-reduced-motion`
- **lucide-react** للأيقونات
- خط **IBM Plex Sans Arabic** مستضاف ذاتيًا عبر `@fontsource` (يعمل دون إنترنت)
- RTL كامل، Dark mode افتراضي، أرقام جدولية (`tabular-nums`) مع عزل ثنائي الاتجاه

```
src/
  app/
    page.tsx                 الرئيسية / Dashboard
    portfolio/               محفظتي
    investment/[id]/         تفاصيل الاستثمار
    sell/[id]/               إنشاء عرض تخارج
    market/                  سوق سيّال
    market/[id]/             تفاصيل الفرصة (جانب المشتري)
    orders/                  أوامري
    transactions/            المعاملات
    account/                 الحساب
    summary/                 شاشة ملخص العرض
  components/
    Shell.tsx                Sidebar + Topbar + مبدّل الشخصيات + الإشعارات
    BuyFlow.tsx              الدفع + المصرفية المفتوحة + مراحل التسوية
    cards.tsx                بطاقات الاستثمار والفرص
    CashflowTimeline.tsx     مخطط التوزيعات
    PlatformChip.tsx         بطاقة المنصة الأصلية
    ui.tsx                   عناصر مشتركة (Modal, Toast, Skeleton, Tooltip…)
  data/                      platforms · users · investments · listings · transactions · bankAccounts
  lib/
    store.tsx                الحالة العامة (Context + Reducer) ونقل الأصل بين المحفظتين
    format.ts                تنسيق الأرقام والعملة وتقدير عائد المشتري
    types.ts
```

### حساب العائد التقديري للمشتري

```
العائد التقديري = العائد الأصلي + (نسبة الخصم × 12 ÷ المدة المتبقية) × 0.95
```

معادلة مبسطة لأغراض العرض فقط، ولا تمثل حسابًا فعليًا لعائد الاستحقاق (YTM).
مثال مدار: `11.2 + (3.0 × 12 ÷ 18) × 0.95 = 13.1%`

---

