# Aqlli Shahar Xo'jaligi — LITE (Docker'siz, mahalliy sinov versiyasi)

Bu versiya `smart-city-project.zip` (to'liq, production) versiyaning
soddalashtirilgan nusxasi — natijani tezda localhost'da ko'rish uchun:

| To'liq versiya           | LITE versiya                  |
|---------------------------|--------------------------------|
| PostgreSQL + PostGIS       | SQLite (fayl asosida)          |
| Redis                      | Jarayon-ichi xotira keshi       |
| GeoDjango (Point/Polygon)  | Oddiy latitude/longitude ustunlari |
| Docker Compose (7 servis)  | Kerak emas                      |
| Sentry, Prometheus, Grafana| Kerak emas                      |

Telegram bot, HeatMap API, barcha modellar va frontend sahifalar — bir xil ishlaydi.

## Ishga tushirish (5 daqiqa)

Talab: kompyuteringizda **Python 3.10+** o'rnatilgan bo'lishi kifoya.

```bash
cd smart-city-lite

# 1. Virtual muhit yaratish
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 2. Kutubxonalarni o'rnatish
pip install -r requirements.txt

# 3. Sozlamalar fayli
cp .env.example .env

# 4. Bazani yaratish
python manage.py migrate

# 5. Admin foydalanuvchi
python manage.py createsuperuser

# 6. Test ma'lumotlari (100 ta murojaat)
python manage.py seed_data --count 100

# 7. Serverni ishga tushirish
python manage.py runserver
```

Endi brauzerda oching:
- **Hokimiyat Dashboard** (xarita + filtrlar): http://127.0.0.1:8000/dashboard/hokimiyat/
- **Operator Paneli** (jadval, saralash): http://127.0.0.1:8000/panel/operator/
- **Xarita test sahifasi**: http://127.0.0.1:8000/test/yandex-map/
- **Admin panel**: http://127.0.0.1:8000/admin/
- **API (HeatMap)**: http://127.0.0.1:8000/api/v1/requests/heatmap_data/

> Eslatma: Yandex Maps xaritasini ko'rish uchun `.env` faylidagi
> `YANDEX_MAPS_API_KEY`ni to'ldirish kerak (bepul kalitni
> https://developer.tech.yandex.ru dan olish mumkin). Kalit bo'lmasa ham
> sahifa ochiladi, faqat xarita ko'rinmaydi — jadval va API baribir ishlaydi.

## Ishlab chiqarishga (production) o'tish

Bu LITE versiya faqat mahalliy ko'rib chiqish uchun. Real foydalanish uchun
`smart-city-project.zip` dagi to'liq versiyani (PostGIS + Docker Compose)
ishlating — u yerda geografik indekslash, PgBouncer, Redis kesh va
monitoring to'liq sozlangan.
