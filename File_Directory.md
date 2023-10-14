---
description: Nodirbek Abdulaxadov
---

# FileInfo va File


FileInfo sinfi - fayllarni yaratish, nusxalash, o'chirish, ko'chirish va ochish uchun xususiyatlar va metodlarni taqdim etadi. Shuningdek, [FileStream](https://docs.microsoft.com/en-us/dotnet/api/system.io.filestream?view=net-5.0) obyektlarini yaratishda yordam beradi.


**FileInfo propertylari:**


| Property nomi | Xususiyati |
| :--- | :--- |
| Directory | Fayl joylashgan katalog nomini qaytaradi |
| DirectoryName | Fayl joylashgan to’liq katalog nomini qaytaradi |
| Exists | Fayl mavjudligini tekshiradi |
| Extension | Fayl turini\(kengaytmasini\) qaytaradi |
| FullName | Faylning to’liq manzilini qaytaradi |
| IsReadOnly | Fayl faqat o’qish uchunligini tekshiradi |
| CreationTime | Fayl yaratilgan vaqtini qaytaradi |
| LastAccessTime | Fayl ishlatilgan oxirgi vaqtni qaytaradi |
| LastWriteTime | Faylning oxirgi o’zgartirilgan vaqtini qaytaradi |
| Length | Fayl hajmini qaytaradi \(baytlarda\) |
| Name | Fayl nomini qayatardi |


**FileInfo metodlari:**

| Metod nomi | Funksionalligi |
| :--- | :--- |
| AppendText | FileInfo ushbu nusxasi tomonidan taqdim etilgan faylga matn qo'shadigan StreamWriter yaratadi. |
| CopyTo | Mavjud faylning ustiga yozishni taqiqlab, mavjud faylni yangi faylga ko'chiradi. |
| Create | Fayl yaratadi |
| CreateText | Yangi matnli faylni yozadigan StreamWriter-ni yaratadi. |
| Delete | Belgilangan faylni o'chiradi. |
| MoveTo | Belgilangan faylni yangi joyga ko'chiradi va yangi fayl nomini ko'rsatish imkoniyatini beradi. |
| Open | Belgilangan FileMode-da ochadi. |
| OpenRead | Faqat o'qish uchun FileStream yaratadi. |
| OpenText | Mavjud matnli fayldan o'qiydigan UTF8 kodlash bilan StreamReader yaratadi. |
| OpenWrite | Faqat yozish uchun FileStream yaratadi. |

_FileInfo xususiyatlardan foydalanish:_

```csharp
//faylga joylashgan path
string path = @"C:\Users\user\Desktop\test.txt";

//FileInfo sinfidan yangi obyekt hosil qilish
FileInfo fileInfo = new FileInfo(path);

//Exist yordamida fayl mavjudligini tekshirish
if (fileInfo.Exists)
{
    //fayl xususiyatlarini chiqarish
    Console.WriteLine($"Fayl joylashgan katalog: \t{fileInfo.Directory}");
    Console.WriteLine($"Fayl kengaytmasi: \t{fileInfo.Extension}");
    Console.WriteLine($"Faylning to'liq nomi: \t{fileInfo.FullName}");
    Console.WriteLine($"Yaratilgan vaqti: \t{fileInfo.CreationTime}");
    Console.WriteLine($"Hajmi: \t{fileInfo.Length} bayt");
}
```

![](../../../.gitbook/assets/image%20%2824%29.png)

_FileInfo metodlaridan foydalanish:_

```csharp
string path = "Example.txt";
var fileInfo = new FileInfo(path);

try
{
    string path2 = "Example_copy.txt";

    // faylni pathdan path2 ga nusxalash
    fileInfo.CopyTo(path2);
    Console.WriteLine($"{path} fayl {path2} ga nusxalandi.");

    // Ensure that the target does not exist.
    fileInfo.Delete();
    Console.WriteLine($"{path} fayl o'chirildi");
}
catch (Exception e)
{
    Console.WriteLine($"Xatolik sodir bo'ldi: {e.Message}");
}
```

**Izohlar:**

Fayllarni ochish, yaratish, ko'chirish, nomini o'zgartirish va o'chirish kabi odatiy operatsiyalar uchun FileInfo sinfidan foydalaning.

Agar bitta faylda bir nechta operatsiyalarni bajarayotgan bo'lsangiz , [File](https://docs.microsoft.com/en-us/dotnet/api/system.io.file?view=net-5.0) sinfining tegishli statik metodlari o'rniga [FileInfo](https://docs.microsoft.com/en-us/dotnet/api/system.io.fileinfo?view=net-5.0) instansiya metodlaridan foydalanish samaraliroq bo'lishi mumkin.
