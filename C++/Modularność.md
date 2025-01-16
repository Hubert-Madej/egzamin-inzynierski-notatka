Modularność w programowaniu odnosi się do podziału kodu na mniejsze, niezależne lub współzależne moduły, które mogą być rozwijane, testowane i utrzymywane oddzielnie. W C++ modularność można osiągnąć poprzez:

- Pliki nagłówkowe (`.h`) i implementacyjne (`.cpp`).
- Użycie funkcji, klas, przestrzeni nazw i modułów (od C++20).

#### **Zalety modularności**:
- **Łatwiejsza konserwacja kodu**: Moduły mogą być modyfikowane bez wpływu na inne części kodu.
- **Reużywalność**: Moduły mogą być używane w różnych projektach.
- **Współbieżne rozwijanie**: Kilku programistów może pracować na różnych modułach równolegle.

```cpp
// funkcje.h

#ifndef FUNKCJE_H
#define FUNKCJE_H

int dodaj(int a, int b);
int mnoz(int a, int b);

#endif
```

```cpp
//funkcje.cpp

#include "funkcje.h"

int dodaj(int a, int b) {
    return a + b;
}

int mnoz(int a, int b) {
    return a * b;
}
```

```cpp
// main.cpp

#include <iostream>
#include "funkcje.h"

int main() {
    std::cout << dodaj(3, 4) << "\n";
    std::cout << mnoz(3, 4) << "\n";
    return 0;
}
```

---
### **Kompilacja rozdzielna (separate compilation)**

Kompilacja rozdzielna polega na kompilowaniu różnych części programu (modułów) oddzielnie, a następnie łączeniu ich w jeden plik wykonywalny. 

Umożliwia to:
- **Szybsze kompilowanie**: Modyfikacja jednego modułu wymaga ponownej kompilacji tylko tego modułu, a nie całego programu.
- **Współdzielenie kodu**: Zależności między modułami są obsługiwane przez pliki nagłówkowe i biblioteki.

#### **Proces kompilacji rozdzielnej**:
1. Każdy moduł jest kompilowany do pliku obiektowego (`.o` lub `.obj`).
2. Pliki obiektowe są łączone w jeden plik wykonywalny podczas konsolidacji.

### Kompilacja:

```bash
g++ -c funkcje.cpp -o funkcje.o
g++ -c main.cpp -o main.o
```

### Konsolidacja (Linking):

```bash
g++ funkcje.o main.o -o program
```

---
### **Konsolidacja (linking)**

Konsolidacja to proces łączenia skompilowanych modułów (`.o`) i bibliotek w jeden plik wykonywalny. 

Może być:
- **Statyczna**: Biblioteki są osadzane w pliku wykonywalnym.
- **Dynamiczna**: Biblioteki są ładowane w czasie wykonywania programu (np. `.dll` w Windows, `.so` w Linux).

#### **Kroki w procesie konsolidacji**:
1. Łączenie symboli (np. funkcji, zmiennych) zdefiniowanych w różnych modułach.
2. Rozwiązywanie zależności między modułami.
3. Tworzenie jednego pliku wykonywalnego.

#### **Przykład statycznej konsolidacji**:

```bash
g++ main.o funkcje.o -o program
```

#### **Przykład dynamicznej konsolidacji**:

```bash
g++ main.o -o program -L./lib -lfunkcje
```

`-L` wskazuje ścieżkę do biblioteki, `-l` dodaje bibliotekę `funkcje`.

---
### **Przestrzenie nazw (`namespaces`)**

Przestrzenie nazw (`namespaces`) służą do grupowania nazw symboli (funkcji, klas, zmiennych) w celu uniknięcia konfliktów nazw w dużych projektach.

#### **Deklaracja przestrzeni nazw**:

```cpp
namespace moje {
    int dodaj(int a, int b) {
        return a + b;
    }
}
```

#### **Użycie przestrzeni nazw**:

```cpp
std::cout << moje::dodaj(3, 4) << "\n";
```

```cpp
using namespace moje;
std::cout << dodaj(3, 4) << "\n";
```

W dużych projektach lepiej unikać globalnego `using namespace`, aby zapobiec konfliktom nazw.

#### **Przestrzenie nazw anonimowe**:

```cpp
namespace {
    int lokalnaFunkcja() {
        return 42;
    }
}
```

Anonimowa przestrzeń nazw w C++ jest używana do ograniczenia widoczności symboli (np. zmiennych, funkcji, klas) do pojedynczego pliku. Działa podobnie jak modyfikator `static` stosowany w deklaracjach zmiennych lub funkcji na poziomie pliku w starszym standardzie C.

Kiedy przestrzeń nazw deklarowana jest bez nazwy, symbole w niej zdefiniowane są dostępne tylko w bieżącym pliku. Oznacza to, że nie mogą być bezpośrednio używane w innych plikach w tym samym projekcie, co eliminuje ryzyko konfliktów nazw.

---
### **Moduły (C++20)**

Moduły to nowa funkcjonalność wprowadzona w C++20, która zastępuje tradycyjne pliki nagłówkowe (`#include`) bardziej nowoczesnym i wydajnym mechanizmem.

#### **Zalety modułów**:
- **Szybsza kompilacja**: Moduły są kompilowane raz i nie wymagają wielokrotnego przetwarzania przez preprocesor.
- **Lepsza enkapsulacja**: Moduły ukrywają szczegóły implementacyjne.
- **Brak konfliktów nazw**: Każdy moduł ma swój własny zakres.

```cpp
export module matematyka;

export int dodaj(int a, int b) {
    return a + b;
}

export int mnoz(int a, int b) {
    return a * b;
}
```

```cpp
import matematyka;

#include <iostream>

int main() {
    std::cout << dodaj(3, 4) << "\n";
    std::cout << mnoz(3, 4) << "\n";
    return 0;
}
```