---
layout:     post
title:      Xamarin.Forms Tips — WCF, Intellisense, PCL Profile, build i inne bolączki
date:       2016-11-05 15:43:00
summary:    Rozpoczynając przygodę z Xamarin.Forms można natknąć się czasami na sytuacje, które mogą przyprawić o ból głowy. Postanowiłem zebrać kilka często spotykanych problemów i przedstawić ich rozwiązania.<!----><!---->Reaktywacja Intellisense w Xamarin.Forms XAMLNajwiększą bolączką w przypadku pracy z Xamarin.Forms bywa... brak Intellisense w dokumentach XAML Xamarin.Forms w Visual Studio. <!----><!----...
categories: windows programowanie urządzenia mobilne
slug: Xamarin.Forms-Tips-WCF-Intellisense-PCL-Profile-build-i-inne-bolaczki,76735.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-11-5-_42_/g_-_-x-_-_-_x20161105144704_0.png
---



Rozpoczynając przygodę z Xamarin.Forms można natknąć się czasami na sytuacje, które mogą przyprawić o ból głowy. Postanowiłem zebrać kilka często spotykanych problemów i przedstawić ich rozwiązania.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-11-5-_42_/g_-_-x-_-_-_x20161105144704_0.png)



## Reaktywacja Intellisense w Xamarin.Forms XAML


Największą bolączką w przypadku pracy z Xamarin.Forms bywa... brak Intellisense w dokumentach XAML Xamarin.Forms w Visual Studio. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-11-5-_42_/g_-_-x-_-_-_x20161103002057_0.png)


Problem nie występuje zawsze i nie pojawia się na samym początku pracy z XAML pod Xamarin.Forms. W moim przypadku po kilku godzinach nagle Intellisense przestał działać bez żądnego powodu. Co jeszcze dziwniejsze, na innym komputerze ze świeżym Visual Studio, podpowiedzi działają wyśmienicie.

Jeśli zatem coś zacznie szwankować w Intellisense warto sprawdzić następujące rozwiązania:



  * zamiast otwierać plik xaml dwuklikiem, klikam prawym przyciskiem myszy na dokumencie i wybieramy  *Open With...* . W otwartym oknie z menu wybieramy  *Source Code (Text) Editor*  (zaznaczając przy okazji opcję  *Set as Default* )

  * alternatywą może być instalacja dodatku [Enable XAML Language for Xamarin.Forms](https://visualstudiogallery.msdn.microsoft.com/8195a8e2-a842-4389-a8cb-34e4672e2e13), który w wielu przypadkach przywraca podpowiedzi w edytorze

  * problem może rozwiązać również odinstalowanie (nie dezaktywacja) ReSharpera, jeśli takowego posiadamy



## WCF i zmiana profilu PCL


Często spotykanym problemem w Xamarin.Forms (PCL) jest dodanie referencji do WCFa (ręcznie wygenerowanie ich przy pomocy  *SLsvcUtil.exe*  również nic nie da). W domyślnej konfiguracji nie jest to możliwe. Przyczyną takiego stanu jest to, iż tworząc nowy projekt w Xamarin.Forms do solucji dorzucany jest projekt pod Windows Phone 8.1. To sprawia, że profil PCL ustawiany jest na kompatybilny z WP8.1 (dokładniej jest to Profile 111), co skutkuje brakiem wsparcia dla WCFa. 

Wszyscy wiemy, że Microsoft pogrzebał Windows Phone 8.1 (Windows 10 Mobile jeszcze oficjalnie żyje), zatem rezygnując z wsparcia dla tego systemu, możemy uzyskać dostęp do WCFa. Można to zrobić szybko poprzez zmianę profilu PCL. Listę dostępnych profili, ze szczegółowym opisem, znajdziemy pod adresem: [Notes on Using Various PCL Profiles with Xamarin](http://danrigby.com/2014/04/16/xamarin-pcl-profile-notes/). W tym przypadku śmiało przejść można na najnowszy profil 44.

Warto nadmienić, że instalując Visual Studio 2015, otrzymując wszystkie niezbędne profile PCL, zatem nie musimy nic ręcznie doinstalowywać.

Załóżmy, że mamy już solucję z Xamarin.Forms, w której znajdują się projekty na wiele platform.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-11-5-_42_/g_-_-x-_-_-_x20161104190643_0.jpg)


Zacznijmy zatem od usunięcia projektu pod Windows Phone 8.1, który blokuje nam możliwość zmiany profilu (przy okazji usuwam też projekt pod Windows 8.1, a z  *okienek*  zostawiam tylko Universal Windows Platform).

Teraz wejdźmy we właściwości biblioteki PCL, do której dodać chcemy referencję do WCFa, a następnie otwórzmy okienko z docelowymi platformami (prawy klik na projekcie:  *Properties*  ->  *Library*  i przycisk  *Change*  w polu  *Targeting* ).

W tym miejscu wybieramy konfigurację jak na załączonym obrazku (można pokusić się też o ASP .NET Core 1.0). Takie ustawienie opcji ustawi profil PCL na 44.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-11-5-_42_/g_-_-x-_-_-_x20161104185720_0.JPG)


W tym momencie dostaniemy pełne wsparcie dla WCF w Xamarin.Forms. Dokładny profil można podejrzeć i zmienić ręcznie poprzez edycję pliku csproj projektu PCL. Znajdziemy w nim dwa interesujące nas pola  *TargetFrameworkVersion*  i  *TargetFrameworkProfile* . Pierwsze informuje o wersji frameworka do PCL, drugie o nazwie profilu.


## Deploy aplikacji na Androida utknął na połączeniu z emulatorem


W przypadku, gdy SDK do Androida było instalowane/aktualizowane ręcznie (czy to po instalacji Visual Studio poprzez instalator Xamaina lub ręcznie, pobierając SDK z sieci), można napotkać na dość nieoczekiwany i trudny do zdiagnozowania błąd.

Przy próbie wrzucenia naszej aplikacji z Visual Studio na emulator Androida, konsola w VS zatrzyma się na (wraz z odpalonym i działającym emualtorem):




```xml
1>Starting deploy 4.5" KitKat (4.4) HDPI Phone ...
1>Starting emulator 4.5" KitKat (4.4) HDPI Phone ...
1>Validating emulator arguments...
1>Determining if emulator is already running...
1>Preparing virtual machine...
1>Launching emulator...
1>Emulator launched successfully
```


Problemem w tym przypadku jest ścieżka do SDK, a dokładniej ADB (Android Debug Bridge). Aby to objeść, w Visual Studio przechodzimy do  *Tools*  ->  *Options*  ->  *Xamarin*  ->  *Android Settings*  i zapamiętujemy  *Android SDK Location* . Następnie otwieramy rejestr (regedit.exe) i przechodzimy do gałęzi:




```xml
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Android SDK Tools
```


W tym miejscu wartość klucza  *Path*  ustawiamy na taką, jaka widnieje w VS w polu  *Android SDK Location* .


## Jak przebiega build projektu Xamarin.Forms na Androida iOS?


Pracując z Xamarinem warto wiedzieć w jaki sposób buildowane są poszczególne aplikacje do ich natywnych wersji.


> Build aplikacji na iOS: kompilator Xamarin C# generuje C# IL (Intermediate Language), a następnie używając kompilatora Apple na macOS generuje natywny kod maszynowy na iOS, niczym kompilator Objective-C.


> Build aplikacji na Androida: kompilator Xamarin C# generuje C# IL. Kod odpalany jest przez Mono na urządzeniu wraz z silnikiem Javy.


## Kilka rad na koniec


Zamykając ten wpis chciałbym jeszcze dodać kilka uwag, o których warto pamiętać przy rozpoczęciu pracy z Xamarin.Forms:



  * nie ma sensu aktualizować na siłę poprzez NuGeta wszystkich pakietów związanych z Xamarinem; część z nich w najnowszej wersji nie jest zgodna z Xamarin.Forms, a jedynie z "natywnym Xamarinem" 

  * mając w sieci komputer z macOS + Xcode, można skorzystać z [iOS Simulator (for Windows)](https://developer.xamarin.com/guides/cross-platform/windows/ios-simulator/) ; narzędzie umożliwi odpalenie w okienku Windowsa emulatora iOS, bez potrzeby łączenia się z pulpitem zdalnym macOS

  * pliki resources w Androidzie nie powinny zawierać znaków specjalnych

  * system Windows Phone 8.1 (nie mylić z Windows 10 Mobile) nawet Microsoft uznaje już za martwy, zatem jeśli nie warto spalać się i zachowywać kompatybilność z starszą wersją mobilnych okienek

  * Emulator Androida na Hyper-V działa o wiele szybciej niż odpowiednik od Google

  * Xamarin.Forms został niemalże stworzony do MVVM (MVVM Light Toolkit, MvvmCross)

  * Xamarin.Forms nie jest idealny, ale potrafi bardzo dużo

  * w Xamarin.Forms nie mamy, aż tak dużego wpływu na UI, jak w natywnym Xamarinie

  * chcąc zyskać na szybkości w ListView warto stworzyć kod w CS niż XAML



 