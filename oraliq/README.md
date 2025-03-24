# Ma'lumotlar bazasi fanidan oraliq

## Vazifa

Ushbu vazifada siz PostgreSQL ma'lumotlar bazasi boshqaruv tizimidan foydalanib musiqa ma'lumotlar bazasini yaratishingiz kerak. Birinchi har bir jadval uchun
berilgan talablarni oqib chiqing. Undan keyin esa siz shu jadvallarni berilgan talabga kora PostgreSQL MBBT da yarating (pgAdmin orqali).
Keyin esa shu jadvallarni toldirishingiz kerak. Jadvalni toldirish uchun berilgan qiymatlardan foydalaning. Keyin esa yaratilgan ma'lumotlar bazisiga
moslangan 10ta mashq bor siz shu mashqlarga sorov yozishingiz kerak. Natijalarni Hemis tizimiga yuklaysiz va ularni quyidagi usulda yuklaysiz:

Har bir yozgan sorovingizga paydo bolgan natijani screenshot qilib va usha sorovni word file ga mashq tartib raqamiga moslab qoyasiz va Hemisga yuklaysiz.

Masalan:

Mashq 1
------- Yartilgan SQLSorov -------
------- Natija rasmi -------

Mashq 2
------- Yartilgan SQLSorov -------
------- Natija rasmi -------

Mashq 3
------- Yartilgan SQLSorov -------
------- Natija rasmi -------

...

Baholash mezoni quyidagicha DDL code uchun yani jadvallarni yaratish uchun yozilgan code bu 20 ball degani, va qolgan 10ta mashqga 8 balldan har biriga
5 baho bu - 90 ball va undan yuqori
4 baho bu - 75 - 89
3 baho bu - 60 - 74

ESLATMA:

Agar kimniki yechilishi uhshash bo'lsa barcha ohshashlar togri 2 oladi. Masalan Eshmat bilan Toshmatni javoblari bir hil bu degani Eshmat aqlli bo'lib ozi qilgan
lekn Toshmatga rahmi kelib 5ta mashqda kochirtirgan va DDL da yordam bergani lekn fan boyicha ustoz Boltavoy buni tekshirishda sezib qolgan va Eshmatga ham Toshmatga
ham o'raliqga 2 qo'ygan.

Chatgpt va boshqa chatbot, LLM lardan foydalangan oquvchilarga to'g'ridan to'g'ri 2 baho qo'yiladi. Oddiy dasturchi ham osongina code kim tomondan yozilganini bemalol sezadi. Umuman ishlatmanglar.

### Masala yechish uchun silarga 3 kun vaqt. Kimda kim mening savol so'rab kelsa o'raliq bo'yicha -12 ball oraliqga oladi.

## Jadvallar tavsifi

Ma'lumotlar bazasida quyidagi jadvallar bo'lishi kerak:

### 1. Artist (Qo'shiqchi) jadvali

**Maqsad**: Bu jadval qo'shiqchilar haqidagi asosiy ma'lumotlarni saqlaydi.

**Maydonlar**:
- `artist_id`: Har bir qo'shiqchining noyob identifikatori (birlamchi kalit / primary key)
- `name`: Qo'shiqchining to'liq ismi
- `country`: Qo'shiqchining vatani/kelib chiqqan mamlakati
- `formed_date`: Qo'shiqchi yoki guruhning tashkil topgan sanasi
- `genre`: Qo'shiqchining asosiy musiqa janri

### 2. Album (Albom) jadvali

**Maqsad**: Bu jadval qo'shiqchilar tomonidan chiqarilgan albomlar haqidagi ma'lumotlarni saqlaydi.

**Maydonlar**:
- `album_id`: Har bir albomning noyob identifikatori (birlamchi kalit / primary key)
- `title`: Albomning nomi
- `artist_id`: Albomni yaratgan qo'shiqchining identifikatori (Artist jadvaliga bog'lovchi tashqi kalit / foreign key)
- `release_date`: Albomning chiqarilgan sanasi
- `genre`: Albomning musiqa janri

### 3. Song (Qo'shiq) jadvali

**Maqsad**: Bu jadval qo'shiqlar haqidagi ma'lumotlarni saqlaydi.

**Maydonlar**:
- `song_id`: Har bir qo'shiqning noyob identifikatori (birlamchi kalit)
- `title`: Qo'shiqning nomi
- `album_id`: Qo'shiq qaysi albomga tegishli ekanligi (Album jadvaliga bog'lovchi tashqi kalit)
- `duration`: Qo'shiqning davomiyligi (sekundlarda)
- `release_date`: Qo'shiqning chiqarilgan sanasi (agar alohida chiqarilgan bo'lsa)

### 4. Rating (Baholash) jadvali

**Maqsad**: Bu jadval foydalanuvchilar tomonidan qo'shiqlarga berilgan baholarni saqlaydi.

**Maydonlar**:
- `rating_id`: Har bir baholashning noyob identifikatori (birlamchi kalit)
- `song_id`: Baholangan qo'shiqning identifikatori (Song jadvaliga bog'lovchi tashqi kalit)
- `user_name`: Baholagan foydalanuvchining ismi
- `score`: Berilgan baho (1 dan 5 gacha)
- `comment`: Foydalanuvchi tomonidan qoldirilgan izoh (majburiy emas)
- `rating_date`: Baholash sanasi

### 5. Stats (Statistika) jadvali

**Maqsad**: Bu jadval qo'shiqlar bo'yicha statistik ma'lumotlarni saqlaydi.

**Maydonlar**:
- `stats_id`: Har bir statistik yozuvning noyob identifikatori (birlamchi kalit)
- `song_id`: Statistika qaysi qo'shiqqa tegishli ekanligi (Song jadvaliga bog'lovchi tashqi kalit)
- `play_count`: Qo'shiqning tinglashlar soni
- `download_count`: Qo'shiqning yuklab olishlar soni
- `like_count`: Qo'shiqning "yoqdi" belgilari soni
- `last_updated`: Statistika oxirgi yangilangan sana

## Jadvallar orasidagi munosabatlar

- Bir **Artist** ko'p **Album**larni yaratishi mumkin (one-to-many)
- Bir **Album**da ko'p **Song**lar bo'lishi mumkin (one-to-many)
- Bir **Song** ko'p **Rating**larni olishi mumkin (one-to-many)
- Har bir **Song** bitta **Stats** yozuviga ega (one-to-one)

## Ma'lumotlar kiritish

Quyidagi SQL skriptlarini bajarib, jadvallaringizga ma'lumotlarni kiriting:

```sql
-- Artist jadvaliga ma'lumotlar kiritish
INSERT INTO Artist (name, country, formed_date, genre) VALUES
('Sevara Nazarxon', 'Ozbekiston', '1995-05-15', 'Folk'),
('Yulduz Usmonova', 'Ozbekiston', '1985-10-12', 'Pop'),
('Coldplay', 'Buyuk Britaniya', '1996-03-15', 'Rock'),
('The Weeknd', 'Kanada', '2010-01-20', 'R&B'),
('Shahzoda', 'Ozbekiston', '2000-07-18', 'Pop');

-- Album jadvaliga ma'lumotlar kiritish
INSERT INTO Album (title, artist_id, release_date, genre) VALUES
('Yol Bolsin', 1, '2005-06-20', 'Folk'),
('Biyo', 2, '2010-03-15', 'Pop'),
('A Head Full of Dreams', 3, '2015-12-04', 'Rock'),
('After Hours', 4, '2020-03-20', 'R&B'),
('Baxt', 5, '2018-09-10', 'Pop');

-- Song jadvaliga ma'lumotlar kiritish
INSERT INTO Song (title, album_id, duration, release_date) VALUES
('Yol Bolsin', 1, 240, '2005-06-20'),
('Yor-yor', 1, 195, '2005-06-20'),
('Biyo', 2, 210, '2010-03-15'),
('Sogindim', 2, 180, '2010-03-15'),
('Adventure of a Lifetime', 3, 260, '2015-11-06'),
('Hymn for the Weekend', 3, 258, '2016-01-25'),
('Blinding Lights', 4, 200, '2019-11-29'),
('Save Your Tears', 4, 215, '2020-08-09'),
('Baxt', 5, 230, '2018-09-10'),
('Hayot', 5, 185, '2018-09-10');

-- Rating jadvaliga ma'lumotlar kiritish
INSERT INTO Rating (song_id, user_name, score, comment, rating_date) VALUES
(1, 'Azizbek', 5, 'Ajoyib qo''shiq!', '2023-01-15'),
(1, 'Malika', 4, 'Menga yoqdi', '2023-01-20'),
(2, 'Doniyor', 5, 'Eng sevimli qo''shig''im', '2023-01-25'),
(3, 'Lola', 4, 'Zo''r qo''shiq', '2023-02-01'),
(5, 'Sarvar', 5, 'Ajoyib ritm', '2023-02-05'),
(5, 'Nodira', 4, 'Yaxshi qo''shiq', '2023-02-10'),
(7, 'Javohir', 5, 'Eng yaxshi qo''shiqladan biri', '2023-02-15'),
(7, 'Kamola', 5, 'Ajoyib!', '2023-02-20'),
(9, 'Bobur', 4, 'Yoqimli ovoz', '2023-03-01'),
(10, 'Gulnora', 3, 'Yomon emas', '2023-03-05');

-- Stats jadvaliga ma'lumotlar kiritish
INSERT INTO Stats (song_id, play_count, download_count, like_count, last_updated) VALUES
(1, 15000, 2500, 12000, '2023-03-01 10:15:00'),
(2, 10000, 1800, 8500, '2023-03-01 10:15:00'),
(3, 25000, 5000, 20000, '2023-03-01 10:15:00'),
(4, 12000, 2000, 9800, '2023-03-01 10:15:00'),
(5, 50000, 15000, 45000, '2023-03-01 10:15:00'),
(6, 48000, 14000, 40000, '2023-03-01 10:15:00'),
(7, 100000, 30000, 95000, '2023-03-01 10:15:00'),
(8, 85000, 25000, 80000, '2023-03-01 10:15:00'),
(9, 18000, 4000, 15000, '2023-03-01 10:15:00'),
(10, 15000, 3500, 12500, '2023-03-01 10:15:00');
```

## So'rovlar topshiriqlari

### Vazifa 1: Barcha qo'shiqlarni ko'rish

**Topshiriq:** Musiqa ma'lumotlar bazasidagi barcha qo'shiqlar ro'yxatini chiqaring, ularning nomlarini alifbo tartibida saralang.

### Vazifa 2: O'zbekistonlik qo'shiqchilar

**Topshiriq:** O'zbekistondan bo'lgan barcha qo'shiqchilarni va ularning janrlarini chiqaring.

### Vazifa 3: Qo'shiqlarni davomiyligi bo'yicha saralash

**Topshiriq:** Barcha qo'shiqlarni muallifi va davomiyligi chiqraing. Davomiyligi bo'yicha kamayish tartibida chiqaring.

### Vazifa 4: Albomlar va ularning qo'shiqlari

**Topshiriq:** Har bir albomdagi qo'shiqlar ro'yxatini chiqaring. Natijada albom nomi, qo'shiq nomi va davomiyligi ko'rsatilsin.

### Vazifa 5: Qo'shiqchilar va ularning albomlari

**Topshiriq:** Har bir qo'shiqchi yaratgan albomlar sonini chiqaring, albomlar soni bo'yicha kamayish tartibida saralang.

### Vazifa 6: Eng mashhur 5 ta qo'shiq

**Topshiriq:** Eng ko'p tinglangan 5 ta qo'shiqni chiqaring, ularning qo'shiqchisi, albom nomi va tinglanishlar sonini ko'rsating.

### Vazifa 7: Baholari bo'yicha o'rtacha qo'shiqlar

**Topshiriq:** Qo'shiqlarning o'rtacha baholarini hisoblab, o'rtacha bahosi 4 dan yuqori bo'lgan qo'shiqlarni chiqaring.

### Vazifa 8: Qo'shiqchilar va ularning statistikasi

**Topshiriq:** Har bir qo'shiqchi uchun umumiy statistikani chiqaring: qo'shiqlar soni, jami tinglashlar soni va o'rtacha "yoqdi" belgilar soni.

### Vazifa 9: Janrlar analitikasi

**Topshiriq:** Musiqa janrlari bo'yicha statistikani chiqaring: har bir janrdagi qo'shiqchilar soni, albomlar soni, qo'shiqlar soni va o'rtacha baholari.

### Vazifa 10: Batafsil qo'shiq ma'lumotlari

**Topshiriq:** Berilgan qo'shiq haqida (Ichki sorovlarni eslang, biz hohlagan qoshiq nomini bersak usha haqida ma'lumot chiqsin. Lekn bizni holatimizda siz JOIN va WHERE buyruqdan foydlansangiz bo'ladi.) to'liq ma'lumot olish uchun so'rov tuzing. So'rov qo'shiq nomi, qo'shiqchi, albom, davomiyligi, sanasi, o'rtacha bahosi, tinglanishlar soni, yuklab olishlar soni va "yoqdi" belgilari sonini qaytarishi kerak.


Bollar omad!
