---
description: Nodirbek Abdulaxadov
---

# Using statement (using bayonoti)

C# va .NET - managed obyektlar uchun resurslarni boshqarishni Garbage Collector(GC) orqali ta'minlaydi. Ya'ni managed obyektlar uchun xotirani aniq ajratish va bo'shatish shart emas.
Boshqa har qanday unmanaged resurslarni tozalash operatsiyalari C# da destruktorda (yoki **Dispose** metodi yordamida) bajarilishi kerak.

Keling bunga bir misol ko'ramiz:

```csharp
string filePath = "example.txt";
//faylni FileStream orqali ochish
FileStream fileStream = new(filePath, FileMode.OpenOrCreate);
try
{
    string textToWrite = "Hello, World!";
    byte[] data = Encoding.UTF8.GetBytes(textToWrite);
    //matnni byte array ko'rinishida faylga yozish
    fileStream.Write(data, 0, data.Length);
}
catch (Exception ex)
{
    //xatolik haqida xabar berish
    Console.WriteLine(ex.Message);
}
finally
{
    //faylni yopish yoki xotiradan o'chirish
    fileStream.Dispose();
}
```

Yuqoridagi kodni soddalashtirish (avtomatlashtirish) uchun C# da **using statement** ishlatiladi. Ya'ni biz using statement orqali foydalangan obyektlarimizni avtomatik Dispose(tozalashga) qilinishga erishamiz.


```csharp
string filePath = "example.txt";
//faylni FileStream orqali ochish
FileStream fileStream = new(filePath, FileMode.OpenOrCreate);

//using statementdan foydalanish
using (fileStream)
{
    string textToWrite = "Hello, World!";
    byte[] data = Encoding.UTF8.GetBytes(textToWrite);
    fileStream.Write(data, 0, data.Length);
}
```

Ho'sh, bo'ldimi? Bu shunchalik osonmi? Avtomatik Dispose qilinganini qayerdan bilamiz?

Buni bilish uchun kodimizning davomida huddi shu **fileStream** obyektidan o'qish uchun foydalanib ko'ramiz:

```csharp
using (fileStream)
{
    byte[] readBytes;
    readBytes = new byte[fileStream.Length];
    fileStream.Read(readBytes, 0, readBytes.Length);
    string readText = Encoding.UTF8.GetString(readBytes);
    Console.WriteLine(readText);
}
```

Bu yerda System.ObjectDisposedException degan xatolik hosil bo'ladi va 'Cannot access a closed file.' degan xabar chiqadi.

KARL!!! Axir ikkinchi usinga kelguncha **fileStream** obyekti Dispose qilindi-ku?! 🪓degandek!

{% hint style="warning" %}
Bir kam dunyo deganlaridek using statement hech qanday exceptionlarni catch qilmaydi! Ya'ni **using statement** ichida qandaydir exception hosil bo'lsa, o'ylab o'tirmay shunchaki otvoradi, tamom!
{% endhint %}


[Bu yerdagi](https://www.twilio.com/blog/c-8-making-use-of-using-declarations) maqolada shunday deyilgan ekan:

_**using statement** obyektni xavfsiz utilizatsiya qilishda kodni **"Clean Code"** darajasini oshiradi. Garchi bu sizning hayotingizda katta inqilob yaratmasa-da, bu kabi kichik yangilanishlar C# tilini kundalik rivojlanish orqali ajoyib tilga aylantiradi. Keyingi safar bir martalik ishlatiladigan unmanaged obyektlarni xavfsiz ishlatishingiz kerak bo'lganda, jingalak qavslarni **o'chirib yuboring** va **using statement**ni sinab ko'ring._

Ho'sh-ho'sh! Jingalak qavslarni o'chirib tashlang deydimi?

Ha, to'g'ri o'qidingiz. C# 8 dan boshlab **using statement**dan yanada soddaroq ko'rinishda, jingalak qavslarsiz foydalansak bo'ladi. Buning uchun using kalit so'zini hech qanday qavslarsiz obyekt tipi oldidan yozish kifoya!

Misol:

```csharp
string connectionString = "Server=(localdb)\\mssqllocaldb; Database=TestDB";
using var dbConnection = new SqlConnection(connectionString);
//qandaydir database bilan ishlar
```
