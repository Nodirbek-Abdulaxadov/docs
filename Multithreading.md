---
description: Nodirbek Abdulaxadov
---

# Multithreading (Threading)

### Multitasking nima?

C# da Multithreading mohiyatini tushunishdan oldin, keling, birinchi navbatda multitaskingni tushunaylik(multitasking - bir paytning o'zida bir-nechta vazifalarni bajara olish qobiliyati). Windows operatsion tizimi multitasking operatsion tizimdir. Bu bir vaqtning o'zida bir nechta ilovalarni ishga tushirish qobiliyatiga ega ekanligini anglatadi. Misol uchun, men kompyuterimda men bir vaqtning o'zida Google Chrome, Microsoft word, Notepad, Media Player, Visual Studio va boshqalarni ochishim mumkin.

### Operatsion tizim bir vaqtning o'zida bir nechta ilovalarni qanday ishga tushira oladi?

Bir vaqtning o'zida bir nechta ilovalarni ishga tushirish uchun operatsion tizim ichki Proccess(jarayonlar)dan foydalanadi.

### Proccess nima?

{% hint style="info" %} Proccess - bu dastur yoki dasturni bajarish uchun mas'ul bo'lgan operatsion tizimning bir qismi (yoki operatsion tizim ostidagi komponent) hisoblanadi. Shunday qilib, har bir dastur yoki dasturni bajarish uchun alohida Proccess bo'ladi. Ilova kodini ishga tushirish uchun proccess ichki ravishda Thread deb nomlangan kontseptsiyadan foydalanadi. {% endhint %}

### Thread nima?

{% hint style="info" %} Thread - proccesslarni(jarayonlarni) borishi va dastur kodini yurgazish vazifasini bajaradigan ijrochidir. Sodda qilib tushundirganda Thread - dastur kodini bajarilishini ta'minlaydigan ishchi. {% endhint %}

Har bir thread o'zining bajarish muhiti bilan,o'ziga tegishli kodi, datalari va resurslariga ega bo'ladi. Bir xil proccessdagi threadlar mustaqil holda bajarilishi mumkin va vazifalarni parallel bajarish imkoniyatini beradi.

Standart holatda, har bir proccess dasturni bajaradigan kamida bitta threadga ega bo'ladi va u **Main Thread** deyiladi. Shuning uchun standart holatda(by default) har qanday dastur single-threaded (yagona threadli) bo'ladi.

Izoh: C# da _threading_ga oid bo'lgan barcha sinflar **System.Threading** namespacega tegishlidir.

Keling endi C# da Threadingni tushunish uchun misolni ko'rib chiqamiz. Bizda Program deb nomlangan classdan iborat bo'lgan oddiy dastur mavjud. class ichida esa Main deb nomlangan method mavjud bo'lib, u shunchaki Konsol oynasiga "Hello, World!" ni chiqaradi:

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

Endi savol: Yuqoridagi dastur ishga tushirilganda Thread dan foydalanadimi?
Ha, **Main Thread** deb nomlangan thread mavjud va u kodimizni ishga tushiradi. Keling, buni isbotini ko'rishamiz. Dasturimizning 5-qatori boshiga **breakpoint** qo'yamiz va dasturni ishga tushiramiz. Dastur bajarilishi 5-qatorga kelib, pauza bo'ladi:

![](<ssets/threading1.png>)

