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

{% hint style="info" %} 
Izoh: C# da _threading_ga oid bo'lgan barcha sinflar **System.Threading** namespacega tegishlidir.
{% endhint %}

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

#### Endi savol: Yuqoridagi dastur ishga tushirilganda Thread dan foydalanadimi?

Ha, **Main Thread** deb nomlangan thread mavjud va u kodimizni ishga tushiradi. Keling, buni isbotini ko'rishamiz. Dasturimizning 5-qatori boshiga **breakpoint** qo'yamiz va dasturni ishga tushiramiz. Dastur bajarilishi 5-qatorga kelib, pauza bo'ladi:

![](<assets/threading1.png>)

Endi threadlar holatini ko'rish uchun Visual Studio menyular qatoridan Debug => Windows => Threads opsiyalarini tanlaymiz:

![](<assets/threading2.png>)

Debug => Windows => Threads opsiyalarini tanlaganingizdan so'ng , u quyidagi oynani ochadi. Bu yerda siz Main Thread hozirda Program sinfining Main metodini bajarayotganini ko'rishingiz mumkin:

![](<assets/threading3.png>)


### C# da Multithreading nima?

Agar dastur kodini bajarish uchun bir nechta thread ishlatilsa, bu **Multithreading** deb ataladi. **Multithreading** - bu bir vaqtning o'zida bir nechta threadlar bilan ishlash orqali dasturni ishlash mexanizmi. _Thread_dan foydalanish dasturning samaradorligini oshiradi va protsessor ishlash vaqtini qisqartiradi. _Multithreadingdan foydalanishning asosiy afzalligi protsessor resurslaridan maksimal darajada foydalanishdir._


### C# da Thread class nima?

_**C# da Thread class - threadlar yaratish va ularni boshqarish uchun ishlatiladi.**_

Quyida **multithreading** bo'yicha aniq misolni ko'ramiz:

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("Main thread ishlashni boshladi!");

        //2 ta thread yaratamiz
        Thread thread1 = new Thread(DoTask1);
        Thread thread2 = new Thread(DoTask2);

        //threadlarni ishga tushiramiz
        thread1.Start();
        thread2.Start();

        //main threadda biror vazifani bajaramiz
        for (int i = 1; i <= 4; i++)
        {
            Console.WriteLine($"Main thread: {i}-natija");
            Thread.Sleep(1000);
        }

        Console.WriteLine("Main thread ishni yakunladi!");
    }

    static void DoTask1()
    {
        Console.WriteLine("Thread1 ishni boshladi!");
        for (int i = 1; i <= 4; i++)
        {
            Thread.Sleep(500);
            Console.WriteLine($"Thread1: {i}-natija");
        }
        Console.WriteLine("Thread1 ishni yakunladi!");
    }

    static void DoTask2()
    {
        Console.WriteLine("Thread2 ishni boshladi!");
        for (int i = 1; i <= 3; i++)
        {
            Thread.Sleep(800);
            Console.WriteLine($"Thread2: {i}-natija");
        }
        Console.WriteLine("Thread2 ishni yakunladi!");
    }
}
```

Natija quyidagi ko'rinishda bo'ladi:

![](<assets/threading4.png>)

{% hint style="info" %} 
Xulosa o'rnida shuni aytishimiz mumkinki, agar siz bir vaqtning o'zida bir nechta vazifalarni bajarmoqchi bo'lsangiz **Multithreading**ni qo'llashingiz mumkin.
{% endhint %}
