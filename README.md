# Onlayn-do-kon-katalogi-interfeys-va-type-alias
// 1. Mahsulot interfeysi (readonly id va ixtiyoriy chegirma bilan)
interface Mahsulot {
    readonly id: number;
    nomi: string;
    narx: number;
    chegirma?: number; // Ixtiyoriy (?) xususiyat
}

// 2. Type alias yordamida Kategoriya turini belgilash
type KategoriyaTuri = "Elektronika" | "Kiyim-kechak" | "Kitoblar";

type Kategoriya = {
    id: number;
    nomi: KategoriyaTuri;
    faolmi: boolean;
};

// 3. Interfeerni extends orqali kengaytirish (RaqamliMahsulot Mahsulot'dan meros oladi)
interface RaqamliMahsulot extends Mahsulot {
    faylHajmiMb: number;
    yuklabOlishHavolasi: string;
}

// --- Obyektlarni yaratish va sinovdan o'tkazish ---

// Oddiy mahsulot obyekti
const fizikaMahsulot: Mahsulot = {
    id: 1,
    nomi: "Mexanik klaviatura",
    narx: 450000,
    chegirma: 10 // Ixtiyoriy xususiyatdan foydalanildi
};

// 4. Readonly xususiyatni o'zgartirishga urinish va uning xatosi:
// fizikaMahsulot.id = 2; 
/* 
  IZOH: Yuqoridagi amal xato beradi, chunki 'id' xususiyati 'readonly' (faqat o'qish uchun) 
  deb belgilangan. Uni obyekt yaratilgandan keyin o'zgartirib bo'lmaydi. 
  TypeScript bu yerda kompilyatsiya xatosini chiqaradi: 
  "Cannot assign to 'id' because it is a read-only property."
*/

// Raqamli mahsulot obyekti (extends qilingan interfeys asosida)
const elektronKitob: RaqamliMahsulot = {
    id: 2,
    nomi: "TypeScript Bo'yicha Qo'llanma",
    narx: 75000,
    faylHajmiMb: 15,
    yuklabOlishHavolasi: "https://example.com/download/ts-guide"
};

// Kategoriya obyekti (Type alias asosida)
const mahsulotKategoriyasi: Kategoriya = {
    id: 10,
    nomi: "Kitoblar",
    faolmi: true
};

// Natijalarni ekranga chiqarish
console.log("--- Oddiy mahsulot ---", fizikaMahsulot);
console.log("--- Raqamli mahsulot ---", elektronKitob);
console.log("--- Kategoriya ---", mahsulotKategoriyasi);
Kodning qisqacha tushuntirishi:
readonly id: Mahsulot ID raqami faqat bir marta e'lon qilinadi va uni keyinchalik o'zgartirib bo'lmaydi.

chegirma?: So'roq belgisi (?) bu xususiyat majburiy emasligini, xohishga ko'ra qo'shilishi mumkinligini bildiradi.

extends: RaqamliMahsulot interfeysi Mahsulot interfeysining barcha xususiyatlarini (id, nomi, narx, chegirma) meros qilib oladi va o'ziga xos qo'shimcha xususiyatlar bilan boyitiladi.

type alias: KategoriyaTuri va Kategoriya orqali ma'lumotlar tuzilishi qat'iy cheklangan holda maxsus tur yaratildi.
