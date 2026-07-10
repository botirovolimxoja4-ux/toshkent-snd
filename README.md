# Toshkent SND — Efir yordamchisi

Teleko'rsatuv uchun jonli efir yordamchisi. Mavzu va tezis (PDF yoki matn) hamda mehmonlar
kiritilganda, sun'iy intellekt har bir mehmon uchun **iliq, mutaxassislikni namoyon etuvchi 5 ta savol**,
**so'zlab ketish uchun 2–3 ta fakt** va (tezis bo'lganda) efir bo'shliqlari uchun **3 ta ma'lumot bloki**
(Yigit–Qiz navbatlashib) tayyorlaydi. **TAYYOR** bosilganda efir barcha qatnashchilarda bir vaqtda ochiladi;
**TAMOM** bilan yakunlanadi.

Bitta fayl — `index.html`. Build (yig'ish) shart emas.

---

## 1. GitHub'ga qo'yish va ochish (GitHub Pages)

1. GitHub'da yangi **repository** yarating (masalan `toshkent-snd`), **Public**.
2. `index.html` faylini repozitoriyga yuklang (Add file → Upload files).
3. **Settings → Pages** bo'limiga o'ting.
4. *Build and deployment* → *Source*: **Deploy from a branch**; *Branch*: **main** / **/(root)** → **Save**.
5. Bir daqiqadan so'ng havola paydo bo'ladi:
   `https://<foydalanuvchi>.github.io/toshkent-snd/`
6. Har bir boshlovchi shu havolani telefonda ochib, brauzer menyusidan
   **"Bosh ekranga qo'shish" (Add to Home Screen)** ni bossa, ilova alohida dastur kabi ishlaydi.

---

## 2. Anthropic API kaliti (savollar ishlashi uchun SHART)

1. https://console.anthropic.com → **API Keys** → yangi kalit yarating (`sk-ant-…`).
2. Ilovada yuqori o'ngdagi **⚙ (Sozlamalar)** ni oching.
3. **Anthropic API kaliti** maydoniga kalitni joylang.
4. **Model** — sukut bo'yicha `claude-sonnet-5`. Tejamkorroq/tezroq variant uchun
   `claude-haiku-4-5-20251001` yozishingiz mumkin.
5. **Saqlash**.

> Kalit faqat shu qurilma brauzerida (localStorage) saqlanadi, hech qayerga yuborilmaydi.
> Uni faqat ishonchli qurilmalarda kiriting.

---

## 3. Ko'p qurilmada sinxron efir (Firebase — ixtiyoriy, ammo kerakli)

Firebase ulanmasa, ilova **faqat bitta qurilmada** ishlaydi. Barcha boshlovchilar
telefonida efir **bir vaqtda bir xil** ko'rinishi uchun bepul **Firebase Realtime Database** ulang:

1. https://console.firebase.google.com → **Add project** (bepul, Spark reja).
2. Chap menyu → **Build → Realtime Database → Create Database** →
   hudud tanlang → **Start in test mode** (sinov rejimi) → yoqing.
3. **Project settings (⚙) → General → Your apps → Web (</>)** → ilova qo'shing →
   `firebaseConfig` obyektini nusxalang. U shunga o'xshaydi:
   ```json
   {
     "apiKey": "AIza…",
     "authDomain": "loyiha.firebaseapp.com",
     "databaseURL": "https://loyiha-default-rtdb.firebaseio.com",
     "projectId": "loyiha",
     "appId": "1:…:web:…"
   }
   ```
4. Ilovadagi **⚙ Sozlamalar → Firebase config** maydoniga shu JSON'ni joylang → **Saqlash**.
5. **Aynan shu configni** barcha boshlovchilar o'z qurilmasida kiritadi.
   Shundan so'ng biri **TAYYOR** bossa — hammada efir bir vaqtda ochiladi,
   savol/ma'lumot **OK** belgilansa hammada yangilanadi, **TAMOM** bosilsa hammada bosh sahifaga qaytadi.

> **Muhim:** `databaseURL` bo'lishi shart (Realtime Database, Firestore emas).
> Test rejimidagi qoidalar ochiq bo'ladi — bu faqat sinov uchun.
> Jiddiy foydalanishda Realtime Database **Rules** ni cheklang.

---

## Ishlash tartibi

1. **Mavzu** nomini yozing.
2. **Tezis** — PDF yuklang yoki matn kiriting. Bo'sh qoldirsangiz, savollar mehmon
   mutaxassisligi va aniq faktlar asosida tuziladi (bu holda efir ma'lumotlari bo'lmaydi).
3. **O'ng / Chap / Auditoriya** bo'limlariga mehmonlarni (ism sharifi + lavozimi) qo'shing.
4. **TAYYOR — efirni boshlash**. AI hamma narsani oldindan tayyorlaydi.
5. Efirda: mehmon ustiga bossangiz — savollar va faktlar to'liq ekranda katta shriftda chiqadi;
   **OK** bilan o'qilganini belgilaysiz. Bo'shliqda **Efir ma'lumotlari**ni ochib o'qiysiz.
   **Aa / Аа** bilan lotin yoki kirill alifbosini tanlaysiz.
6. Efir tugagach **TAMOM**.

## Texnik eslatma

- Ilova React + Firebase (ixtiyoriy) + pdf.js dan foydalanadi, hammasi CDN orqali yuklanadi —
  shuning uchun ochilganda internet kerak.
- Savollar to'g'ridan-to'g'ri brauzerdan Anthropic API'ga yuboriladi
  (`anthropic-dangerous-direct-browser-access`). Xarajat sizning API kalitingiz hisobidan.
