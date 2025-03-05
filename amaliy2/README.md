
## 1. Barcha kurslarni kafedra nomlari bilan ko'rsating
```sql

```
**Maslahat**: Bu so'rov oddiy bo'lib, JOIN inglating shart emas, chunki department ma'lumoti Course jadvalida mavjud.

## 2. Barcha talabalarni ta'lim yo'nalinglari bilan ko'rsating
```sql

```
**Maslahat**: Bu so'rovda JOIN kerak emas, shunchaki bir jadvaldan ma'lumotlar tanlab olinadi.

## 3. Professorlar va ularning kafedralarini ko'rsating
```sql

```
**Maslahat**: Bu so'rov faqat Professor jadvalidagi ma'lumotlarni talab qiladi.

## 4. Ro'yxatdan o'tgan talabalarni o'qiyotgan kurslari bilan ko'rsating
```sql

```
**Maslahat**: Bu yerda uchta jadval bog'laningi kerak: Student, Enrollment va Course.

## 5. Alinger Zokirov o'qitadigan barcha kurslarni toping
```sql

```
**Maslahat**: Course, ClassSchedule va Professor jadvallarini bog'lab, WHERE orqali professor ismini filtrlash kerak.

## 6. Barcha professorlarni ofis raqamlari bilan ko'rsating
```sql

```
**Maslahat**: Professor jadvalidagi ma'lumotlarni tanlash, ofis raqami bo'sh bo'lmagan yozuvlarni oling kerak.

## 7. Kurslarni jadval kunlari va vaqtlari bilan ko'rsating
```sql

```
**Maslahat**: Course va ClassSchedule jadvallarini bog'lash kerak, kurs nomi va dars kunlari bo'yicha saralash.

## 8. "Dasturlash asoslari" kursiga yozilgan barcha talabalarni toping
```sql

```
**Maslahat**: Student, Enrollment va Course jadvallarini bog'lab, kerakli kurs nomini WHERE sharti orqali filtrlang.

## 9. Har bir kafedradagi kurslar sonini hisoblash
```sql

```
**Maslahat**: Course jadvalidan ma'lumotlarni tanlab, GROUP BY orqali kafedralar bo'yicha guruhlab, COUNT(*) funksiyasi orqali hisoblab chiqing.

## 10. Matematika kafedrasi kurslari o'tiladigan xonalarni ko'rsating
```sql

```
**Maslahat**: ClassSchedule va Course jadvallarini bog'lab, Matematika kafedrasiga tegingli kurslarni filtrlang, xona raqamlari takrorlanmasligi uchun DISTINCT so'zidan foydalaning.

## 11. Professorlar va ular o'qitadigan kurslar sonini ko'rsating
```sql

```
**Maslahat**: LEFT JOIN ishlating, chunki ba'zi professorlar hech qanday kurs o'qitmasligi mumkin. COUNT(DISTINCT cs.course_id) orqali har bir professor o'qitadigan noyob kurslar sonini hisoblang.

## 12. Hech bir talaba yozilmagan kurslarni toping
```sql

```
**Maslahat**: LEFT JOIN inglatib, bog'langan jadvalda ma'lumot yo'qligini tekshiring (e.enrollment_id IS NULL).

## 13. Barcha xodimlar va ularning kafedralarini ko'rsating
```sql

```
**Maslahat**: Bu so'rov faqat Employee jadvalidagi ma'lumotlarni ko'rsatadi.

## 14. Dushanba kuni o'tiladigan barcha kurslarni ko'rsating
```sql

```
**Maslahat**: Course va ClassSchedule jadvallarini bog'lab, hafta kunini filtrlash kerak.

## 15. Ham professor, ham xodim inglayotgan kafedralarni toping
```sql

```
**Maslahat**: IN operatori va pastki so'rov orqali ikkala jadvalda ham mavjud bo'lgan kafedra nomlarini toping.
