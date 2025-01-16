System operacyjny (SO) jest podstawowym elementem oprogramowania każdego komputera, pełniącego role pośrednika miedzy sprzętem a użytkownikiem oraz zapewniając środowisko do uruchamiania aplikacji. Jego głównym zadaniem jest zarządzanie zasobami sprzętowymi, takimi jak procesor, pamięć operacyjna, urządzenia wejścia-wyjścia oraz pliki.

# Typy Systemów Operacyjnych
Systemy operacyjne można klasyfikować na różne sposoby w zależności od ich zastosowania, struktury i sposobu zarządzania zasobami. W systemach ***jednoużytkownikowych***, takich jak **MS-DOS**, jedna osoba ma pełny dostęp do zasobów komputera. W przeciwieństwie do nich, systemy wieloużytkownikowe, takie jak **Unix** czy **Linux**, pozwalają na jednoczesne korzystanie z maszyny przez wielu użytkowników, dzieląc między nich zasoby w sposób kontrolowany.

Kolejną istotną kategorią są systemy jednozadaniowe i wielozadaniowe. W systemach jednozadaniowych, jak MS-DOS, jednocześnie można uruchomić tylko jedno zadanie. Systemy wielozadaniowe, takie jak współczesne wersje **Windows** czy **macOS**, potrafią przełączać procesor między różnymi zadaniami, sprawiając wrażenie ich równoczesnego wykonywania.

Szczególną grupą są systemy czasu rzeczywistego (**RTOS**), które muszą spełniać określone wymagania czasowe. Twarde RTOS, takie jak **VxWorks**, gwarantują, że zadania zostaną wykonane w wyznaczonym czasie, co jest kluczowe w systemach sterowania, np. w przemyśle lotniczym. Miękkie RTOS, np. w niektórych aplikacjach multimedialnych, są bardziej elastyczne i dopuszczają opóźnienia, jeśli nie zakłócają ogólnego działania systemu.

Systemy wbudowane, takie jak **FreeRTOS**, działają na urządzeniach z ograniczonymi zasobami, jak mikroprocesory w sprzęcie AGD. Z kolei systemy rozproszone, np. **Apache Hadoop**, współpracują na wielu maszynach, tworząc iluzję jednolitego środowiska. Ostatnią kategorią są systemy mobilne, jak **Android** czy **iOS**, zoptymalizowane pod kątem urządzeń przenośnych.

# Funkcje Systemu Operacyjnego
System operacyjny spełnia wiele kluczowych funkcji, które można podzielić na kilka głównych kategorii. Pierwszą z nich jest zarządzanie procesami, które obejmuje tworzenie, planowanie i synchronizację procesów. SO decyduje, które zadanie otrzyma dostęp do procesora, zapewniając jednocześnie, że procesy współdzielące zasoby nie powodują konfliktów.

Drugą funkcją jest zarządzanie pamięcią. System operacyjny alokuje i zwalnia pamięć dla procesów oraz kontroluje mechanizmy takie jak stronicowanie czy segmentacja, aby optymalnie wykorzystać dostępne zasoby. Wirtualizacja pamięci umożliwia uruchamianie procesów, które wymagają więcej pamięci, niż faktycznie jest dostępne.

SO zarządza również urządzeniami wejścia-wyjścia, które stanowią interfejs między oprogramowaniem a sprzętem. Obsługuje sterowniki urządzeń, zapewniając jednolity sposób komunikacji z różnorodnymi urządzeniami. Kolejną kluczową funkcją jest zarządzanie systemem plików. System operacyjny umożliwia tworzenie, usuwanie i organizowanie plików, a także obsługuje różne systemy plików, takie jak NTFS czy ext4.

Bezpieczeństwo i ochrona są kolejnymi istotnymi aspektami działania systemu operacyjnego. SO zapobiega nieautoryzowanemu dostępowi do zasobów oraz chroni procesy przed wzajemnym zakłócaniem. Umożliwia również komunikację między procesami za pomocą mechanizmów takich jak pamięć współdzielona, kolejki komunikatów czy sygnały.

### **Budowa Systemu Operacyjnego**
System operacyjny składa się z kilku warstw. Jądro (ang. kernel) jest jego centralną częścią, odpowiedzialną za zarządzanie pamięcią, procesami, urządzeniami i komunikacją. Jądro może być monolityczne, jak w systemie Linux, gdzie cały kod jądra działa w jednej przestrzeni adresowej, co zapewnia wysoką wydajność, ale utrudnia debugowanie. Alternatywnie, może to być mikrojądro, które minimalizuje swoją funkcjonalność, delegując wiele zadań do przestrzeni użytkownika, co zwiększa stabilność, ale kosztem wydajności.

Powłoka (ang. shell) to interfejs użytkownika systemu operacyjnego, który może być tekstowy (CLI) lub graficzny (GUI). Biblioteki systemowe zapewniają aplikacjom dostęp do funkcji jądra, a aplikacje użytkownika stanowią warstwę najwyższą, działającą na systemie operacyjnym.

### **Modele Komunikacji Międzyprocesowej**
Komunikacja między procesami (IPC) to mechanizmy umożliwiające procesom wymianę danych i współpracę. Pamięć współdzielona pozwala procesom na szybki dostęp do wspólnego obszaru pamięci, ale wymaga mechanizmów synchronizacji, takich jak semafory czy muteksy, aby zapobiec konfliktom. Kolejki komunikatów umożliwiają procesom wysyłanie i odbieranie komunikatów w sposób bardziej uporządkowany niż pamięć współdzielona, ale są wolniejsze.

Potoki (pipes) to jednokierunkowe kanały komunikacyjne między procesami, podczas gdy gniazda (sockets) umożliwiają komunikację zarówno lokalną, jak i sieciową. Sygnalizacja (signals) jest prostym mechanizmem pozwalającym procesom informować się nawzajem o zdarzeniach. Semafory i muteksy to narzędzia do synchronizacji procesów i wątków, zapewniające, że zasoby są używane w kontrolowany sposób.