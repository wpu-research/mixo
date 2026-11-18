# Mixo

Mixo Outlet için e-ticaret çalışma alanı: vitrin + yönetim paneli demosu, fiyat karşılaştırma servisi, mobil uygulama, tek sayfalık bilgi sayfası ve karar/analiz belgeleri. Büyük bir monorepo'dur; burada yalnız üst düzey yapı anlatılır.

## Klasör yapısı

| Klasör | İçerik |
| --- | --- |
| `demo/` | Ana uygulama "mixoutlet-demo": vitrin, yönetim paneli (`admin/`), Claude asistanı, sipariş/iade/kargo/kampanya modülleri. Mimari notu: `demo/ARCHITECTURE.md` |
| `karsilastir/` | Fiyat karşılaştırma servisi: tarayıcı (crawler), besleme (CSV/XML) içe aktarma, EAN eşleştirme, genel ve yönetim sayfaları |
| `mobile/` | Müşteri mağaza uygulaması "mixo-outlet-mobile" (Expo + Expo Router, iOS/Android/web) |
| `talep/` | Tek sayfalık statik sayfa (başlangıç için gerekenler), küçük Node sunucusu ve Dockerfile |
| `docs/` | Analiz, karar, güvenlik ve konsey raporları, mobil uygulama kararı |
| `_fiyat/`, `_raw/`, `_verify/` | Fiyat verisi hazırlama ve doğrulama betikleri/girdileri |
| `video/`, `.agents/`, `.github/` | Videolar, ajan beceri tanımları, CI iş akışı |

## Ana özellikler (demo)

- Yaklaşık 45 bin ürünlük katalog, arama, filtre, sepet, ödeme akışı.
- Yönetim paneli: pano, siparişler, iadeler, kargo, B2B, reklam, destek, fiyat kuralları, kiracılar, besleme yönetimi, sistem sağlığı.
- Claude asistanı (araç çağrısı + onay kapısı, günlük limit), değişiklik günlüğü ve geri alma.
- Instagram ve pazarlama entegrasyon modülleri, şifreli yedekleme.

## Teknoloji

Node 22 (yerleşik `node:sqlite`), bağımlılıksız HTTP sunucusu, Anthropic SDK, ESLint, Prettier, TypeScript tip denetimi, `node:test`, Playwright; Docker; mobilde Expo SDK 58 / React Native.

## Kurulum ve çalıştırma

```bash
cd demo && npm install && npm start      # veya: npm run check (lint + tip + test)
cd karsilastir && npm install && npm start
cd mobile && npm install && npx expo start
```

Node >= 22.13 gerekir (`.nvmrc`: 22). Veritabanı `DATA_DIR` altında tutulur; Docker/Railway'de kalıcı diske bağlanır.

## Ortam değişkenleri (yalnız adlar)

- `demo`: `ADMIN_PASSWORD`, `SESSION_SECRET`, `ANTHROPIC_API_KEY`, `ASSISTANT_MODEL`, `ASSISTANT_APPROVAL`, `ASSISTANT_DAILY_LIMIT`, `BACKUP_ENCRYPT_KEY`, `BACKUP_EXPORT_DIR`, `BACKUP_KEEP`, `DATA_DIR`, `ORDER_VERIFY`, `REFUND_APPROVAL_THRESHOLD`, `SITE_URL`, `SUNUM_PROTECT`, `TRUST_PROXY`, `PORT`
- `karsilastir`: `ADMIN_PASSWORD`, `ALLOW_PRIVATE_HOSTS`, `CRAWLER_ENABLED`, `DATA_DIR`, `HOST`, `OFFER_MAX_AGE_DAYS`, `PORT`, `SCHEDULER`, `SITE_URL`

Gerçek değerler depoya konmaz (`.gitignore` `.env*` ve yerel parola dosyasını dışlar).

## Lisans

Kök için lisans belirtilmemiş. `mobile/LICENSE` dosyası MIT lisansıdır.
