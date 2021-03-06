---
layout:     post
title:      IIS 8.0 na Windows Server 2012 - instalacja i nowości
date:       2012-12-01 17:19:00
summary:    Windows Server 2012 wprowadza wiele zmian i nowości nie tylko w funkcjonalnościach, ale także w samym interface. Wystarczy nadmienić, że do serwerowej wersji okienek trafia pulpit Modern, który jest tam wsadzony nie wiadomo po co. Jego jednak nie musimy oglądać (w przeciwieństwie do wersji desktopowej, domyślnie po zalogowaniu pojawia się klasyczny pulpit). Warto zauważyć, że wita nas odmieniony i...
categories: windows oprogramowanie serwery
slug: IIS-na-Windows-Server--instalacja-i-nowosci,37627.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130182712_0.png
---



Windows Server 2012 wprowadza wiele zmian i nowości nie tylko w funkcjonalnościach, ale także w samym interface. Wystarczy nadmienić, że do serwerowej wersji okienek trafia pulpit Modern, który jest tam wsadzony nie wiadomo po co. Jego jednak nie musimy oglądać (w przeciwieństwie do wersji desktopowej, domyślnie po zalogowaniu pojawia się klasyczny pulpit). Warto zauważyć, że wita nas odmieniony i odświeżony  *Menedżer Serwera* , który wygląda dość nowatorsko i przyjemnie dla oka. To jednak nie o tym jest ten wpis. Chciałbym przedstawić jak w nowym Windows Server 2012 zainstalować IIS 8.0 pod aplikacje dla ASP.NET i pokazać kilka najciekawszych nowości, które znajdziemy w tym wydaniu Internet Information Services.



## Instalacja



Nowe okienko nie powinno nikogo przerażać. Aby dodać IISa, wystarczy w wejść w  *Menedżer Serwera* , tam jeśli zobaczymy okno powitalne, wystarczy kliknąć na  *Dodaj role i funkcje* . To samo można zrobić z menu  *Zarządzaj* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130182712_0.png)




W kreatorze wybieramy odpowiedni typ instalacji i serwer docelowy.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130184100_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130184234_0.png)



Następnie odszukujemy w rolach  *Web Server (IIS)*  i zaznaczamy. W tym miejscu można jeszcze rozwinąć gałąź dla IISa i wybrać  *Ograniczenia adresów IP i domen*  ( *Web Server*  ->  *Security*  ->  *IP and Domain Restrictions* ) - nowość w IIS 8.0 do wykrywania ataków DoS i blokowania podejrzanych adresów IP. Jeśli będziemy posiadać certyfikaty SSL to zaznaczmy:  *Centralized SSL Certificate Support* , do zarządzania nimi. W gałęzi dla  *Web Server (IIS)*  znajdziemy także możliwość dodania FTP ( *FTP Server* ).


Jeśli pojawi się okienko z pytaniem, czy dodać wymagane funkcje, potwierdzamy wybór. W kroku  *Wybierani usług ról*  należy zaznaczyć odpowiednie wersje ASP.NET, jakie będą używane na serwerze (4.5/3.5), znajdziemy je w gałęzi  *Application Development* . Jeśli pojawi się okno z pytaniem o dodanie powiązanych funkcjonalności, zaakceptujmy poprzez  *Dodaj funkcje* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130190501_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130190452_0.png)



W sumie to już wszystko. Przejdźmy do końca kreatora i przyciskiem Zainstaluj, dokończmy proces dodawania IIS 8.0 na serwerze. Jeśli wszystko zostało zainstalowane poprawnie, po wpisaniu w pasku adresu  *localhost*  powinniśmy ujrzeć logo nowego IISa:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130191054_0.png)



Teraz możemy już odpalić nowego IIS 8.0. Tutaj na szczęście nie ma interface Modern! Wszystko wygląda po staremu, możemy odetchnąć. Jeszcze tylko sprawdźmy, czy na pewno wybrana wersja ASP.NET została zainstalowana, poprzez przejście do  *Puli aplikacji*  w  *Menedżerze IIS* . 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130192007_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130192013_0.png)






## Nowości w IIS 8.0



 *Menedżerze IIS*  na szczęście nie został zmieniony, jak  *Menedżer Serwera* . Nowy IIS to kilka modułów, które coraz mocniej skupiają się na serwerach o zwiększonej wydajności i obciążeniu.



### CPU Throttling



Coraz bardziej zaawansowane usługi www i rosnący ruch, spowodował zapotrzebowanie na funkcję do ustawienia wykorzystania CPU dla poszczególnych aplikacji. Nie tylko można wyłączyć usługę, gdy jest ona przeciążona, ale również przydzielić czas CPU jaki dostanie. Można zatem dla poszczególnej puli: 



  * przydzielić odgórnie ograniczenie procesu dla dostępu do CPU ( *Throttle* )

  * ograniczyć dostęp do CPU, gdy jest on silniej obciążony, ale jednocześnie zwiększyć dostęp, w przypadku bezczynności



Nowe opcje pozwalają na ograniczenie monopolu jednej aplikacji, w przypadku serwera-chmury, hostującego aplikacje i jednolity dostęp do CPU dla wszystkich.  Z drugiej strony jeśli jest to wymagane, czas CPU jest przydzielany dla aplikacji, która wymaga więcej zasobów w przypadku, gdy inne aplikacje nie obciążają CPU.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130193447_0.png)





### Ograniczenia adresów IP i domen
 *IP Address and Domain Restrictions* 



Kolejna funkcja dla serwerów narażonych na ataki DoS. Dzięki  *Ograniczenia adresów IP i domen*  dla danej aplikacji administrator jest w stanie ustawić dla IP:




  * ograniczenie ze względu na ilość równoczesnych zapytań

  * ograniczenie na ilość zapytań w danym czasie 



Ograniczeniem może być zarówno odmowa wyświetlenie strony, albo tylko logowanie takich zdarzeń i ich późniejsza analiza w celu udaremnienia ataku w przyszłości. Co więcej, istnieje możliwość skonfigurowania tego, jaki rodzaj błędu/informacji ma się wyświetlać dla danego IP, gdy zostanie ograniczone.  *Ograniczenia adresów IP i domen*  pozwala także na wykrywanie łączenia się przez proxy. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130203806_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121130203809_0.png)





### Scentralizowane certyfikaty
 *Centralized Certificate* 


IIS 8.0 wprowadzam mechanizm do zarządzania certyfikatami SSL, który niesamowicie ułatwia pracę. Nie trzeba już oddzielnie kopiować i importować certyfikatów. Teraz wszystkie pliki certyfikatów maja wspólny folder i tworząc witrynę z https, wybieramy istniejący już plik do uwierzytelnienia SSL. Prosto i przyjemnie, bez zabawy z kreatorami itp.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121201164738_0.png)





### Ograniczenie prób logowania na koncie FTP
 *FTP Logon Attempt Restriction* 


Jeśli korzystamy z FTPa, w nowym IIS otrzymujemy OOTB blokowanie adresów IP, z których były nieudane prób logowania (lub będziemy tylko to rejestrować). Dzięki temu ograniczymy możliwość ataków metodą  *brutal force* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-1-_129_/g_-_-x-_-_-_x20121201170835_0.png)





Nie są to wszystkie nowości w IIS 8.0, a jedynie te które wydały się bardziej ciekawe. Niektóre z nich, zaś wymagają dłuższego przedstawienia. W następnych wpisach postaram się je przedstawić.