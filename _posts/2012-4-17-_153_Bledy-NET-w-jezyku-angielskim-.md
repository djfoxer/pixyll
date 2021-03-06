---
layout:     post
title:      Błędy .NET w języku angielskim 
date:       2012-04-17 17:26:00
summary:    Pisząc aplikacje w .NET często spotykamy się z wyjątkami (ktoś złośliwy mógłby napisać, że nie  — P ). Dzięki polu Message w obiekcie Exception, dostajemy w postaci stringa opis błędu. Polski język nie jest obcy dla frameworku, co za tym idzie, wszelkie komunikaty otrzymujemy w  naszej ojczystej mowie. Dużym plusem tego, jest możliwość "wyrzucenia" komunikatu z błędem, dzięki czemu każdy, bez znajom...
categories: porady programowanie
slug: Bledy-NET-w-jezyku-angielskim,31465.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-17-_153_/g_-_-x-_-_-_x20120412112102_0.png
---



Pisząc aplikacje w .NET często spotykamy się z wyjątkami (ktoś złośliwy mógłby napisać, że nie :P ). Dzięki polu Message w obiekcie Exception, dostajemy w postaci stringa opis błędu. Polski język nie jest obcy dla frameworku, co za tym idzie, wszelkie komunikaty otrzymujemy w  naszej ojczystej mowie. Dużym plusem tego, jest możliwość "wyrzucenia" komunikatu z błędem, dzięki czemu każdy, bez znajomości języka angielskiego, może szybko (lub nie) zdiagnozować błąd.



Są jednakże i minusy. Otóż niektóre komunikaty błędów nie są tak oczywiste w języku polskim, jak w angielskim, co nie jest jeszcze dużym problemem. Większym problemem jest wyszukanie informacji (rozwiązania) o błędzie. Można być pewnym, że wpisując w google błąd w języku polskim, nie natrafimy na satysfakcjonujące nas rezultaty.

Powinniśmy zatem przetłumaczyć tekst na angielski i dopiero taki ciąg znaków szukać. I teraz zaczyna się "bajka". Wiadomo, iż tłumaczenia nie zawsze są jednoznaczne, ale co gorsze, można przecież dany zwrot przetłumaczyć na kilka sposobów.

Np. wyjątek w języku polskim:



> Nie można odnaleźć wartości literału.


Można przetłumaczyć na:


> Can not find the literal value.


Ale czy znajdziemy szybko, rozwiązanie? Niestety pewnie nie. Gdyż w oryginalnej wersji językowej (angielskiej) wyjątek ma opis:



> Literal value was not found.




Zatem czy my, osoby korzystające z polskich komunikatów w .NET, jesteśmy na straconej pozycji? Oczywiście nie :)



## Zmiana komunikatów z błędami w .NET na język angielski



Jest kilka wyjść, które pomogą nam uporać się z polskimi komunikatami z błędami w .NET. 



### FindErr.NET / Unlocalize





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-17-_153_/g_-_-x-_-_-_x20120412112102_0.png)



Gdy nie możemy/nie chcemy zmieniać komunikatów w oryginalnej aplikacji (bez naruszania kodu po stronie klienta/serwera), warto skorzystać ze strony FindErr.NET ([http://finderr.net/](http://finderr.net/) ), gdzie wystarczy wkleić komunikat w języku polskim, aby otrzymać oryginalną wersję w języku angielskim. Dostajemy również katalog, z możliwością przejrzenia/wyszukania zgromadzonych komunikatów. W taki oto sposób, łatwo wyszukamy źródłową wersję komunikatu w języku angielskim.

Podobną funkcjonalność oferuje Unlocalize: [http://www.unlocalize.com](http://www.unlocalize.com) 



### Zmiana bezpośrednio w wątku



Mając taką możliwość, podmianę języka komunikatów można zrobić wstawiając do kodu:



```csharp
Thread.CurrentThread.CurrentCulture = new CultureInfo("en-us");
Thread.CurrentThread.CurrentUICulture = Thread.CurrentThread.CurrentCulture;
```






### Zmiana w  *web.configu* 



Jeśli chcemy w naszej aplikacji ASP.NET zmienić język komunikatów z błędami na np. angielski, wystarczy dodać do  *web.configu*  w sekcji  *<system.web>*  :


```xml
 <globalization culture="en-US" uiCulture="en-US" />
```







![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-17-_153_/g_-_-x-_-_-_x20120416132655_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-17-_153_/g_-_-x-_-_-_x20120416132701_0.png)




Oczywiście jest jeszcze możliwość odinstalowania "spolszczeń" do .NETa i/lub zabawy z językiem w systemie, jednakże nie zawsze te chwyty działają. A wymienione wyżej wyjścia pozwolą w miarę szybko i bezstresowo uporać się z angielskimi komunikatami w .NET.