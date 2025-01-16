# **Typ tablicowy**
Tablice w C++ to podstawowy typ danych służący do przechowywania kolekcji elementów tego samego typu. Istnieją dwa główne rodzaje tablic w C++: **tablice statyczne** i **tablice dynamiczne**.

**Tablice statyczne**
**Deklaracja**: Rozmiar tablicy musi być znany w czasie kompilacji. Alokowana jest na stosie. Zaletą jest szybka alokacja, automatyczne zarządzanie pamięcią. Wadą jest brak możliwości zmiany rozmiaru w trakcie działania programu, brak sprawdzania zakresu (np. `tablica[10]` może prowadzić do błędów).

```cpp
#include <iostream>

int main() {
    const int rozmiar = 5; // Rozmiar znany w czasie kompilacji
    int tablica[rozmiar] = {1, 2, 3, 4, 5};

    for (int i = 0; i < rozmiar; i++) {
        std::cout << tablica[i] << " ";
    }
    std::cout << "\n";

    return 0;
}
```

**Tablice dynamiczne**
**Deklaracja**: Rozmiar może być ustalony w czasie działania programu. Alokowana jest na stercie. Główną zaletą jest elastyczność w rozmiarze. Wadą jednak jest wymaganie ręcznego zarządzania pamięcią (alokacja `new`, zwalnianie `delete`). Może prowadzić do wycieków pamięci, jeśli nie zostanie poprawnie zwolniona.

```cpp
#include <iostream>

int main() {
    int rozmiar;
    std::cout << "Podaj rozmiar tablicy: ";
    std::cin >> rozmiar;

    // Dynamiczna alokacja pamięci
    int* tablica = new int[rozmiar];

    // Wypełnianie tablicy
    for (int i = 0; i < rozmiar; i++) {
        tablica[i] = i + 1; // Przykładowe dane
    }

    // Wyświetlanie tablicy
    for (int i = 0; i < rozmiar; i++) {
        std::cout << tablica[i] << " ";
    }
    std::cout << "\n";

    // Zwolnienie pamięci
    delete[] tablica;

    return 0;
}
```

#### **Nowoczesne podejście: `std::array` i `std::vector`**
`std::array` (dla tablic o stałym rozmiarze) i `std::vector` (dla tablic dynamicznych) są bezpieczniejszymi i bardziej funkcjonalnymi odpowiednikami tradycyjnych tablic.

```cpp
#include <array>
std::array<int, 5> tablica = {1, 2, 3, 4, 5};
std::cout << tablica.at(2) << "\n"; // Bezpieczny dostęp (z kontrolą zakresu)
```

Tablice dynamiczne w nowoczesnym C++ są często zastępowane przez `std::vector`, który automatycznie zarządza pamięcią i pozwala na łatwe rozszerzanie tablicy. Pamięć zarządzana jest automatycznie (bez `new` i `delete`), zachowujemy elastyczność w rozmiarze.

```cpp
#include <iostream>
#include <vector>

int main() {
    int rozmiar;
    std::cout << "Podaj rozmiar wektora: ";
    std::cin >> rozmiar;

    // Tworzenie dynamicznego wektora
    std::vector<int> vec(rozmiar);

    // Wypełnianie wektora
    for (int i = 0; i < rozmiar; i++) {
        vec[i] = i + 1;
    }

    // Dodanie dodatkowego elementu
    vec.push_back(rozmiar + 1);

    // Wyświetlanie wektora
    for (int liczba : vec) {
        std::cout << liczba << " ";
    }
    std::cout << "\n";

    return 0;
}
```

---
# Tworzenie własnych typów
C++ pozwala na definiowanie własnych typów danych za pomocą:
- **Typów wyliczeniowych (`enum`)**.
- **Typów zdefiniowanych przez użytkownika (`typedef`, `using`)**.
- **Struktur (`struct`) i klas (`class`)**.

#### **Typy wyliczeniowe (`enum`)**
Typy wyliczeniowe pozwalają na definiowanie zmiennych o ograniczonym zestawie wartości.

```cpp
enum Kolor {CZERWONY, ZIELONY, NIEBIESKI};

Kolor k = CZERWONY;
if (k == CZERWONY) {
    std::cout << "Kolor to czerwony\n";
}
```

Rozszerzone typy wyliczeniowe (`enum class`) wprowadzono w C++11. Zapewniają lepszą kontrolę zakresu i unikanie konfliktów nazw.

```cpp
enum class Dzien {PONIEDZIALEK, WTOREK, SRODA};

Dzien dz = Dzien::WTOREK;
if (dz == Dzien::WTOREK) {
    std::cout << "To jest wtorek\n";
}
```

# Własne typy z użyciem `typedef` i `using`
Zarówno `typedef`, jak i `using` służą do definiowania aliasów typów w C++. Choć na pierwszy rzut oka mogą wydawać się podobne, istnieją różnice między nimi, szczególnie w kontekście nowoczesnego C++ (C++11 i nowsze).

### **`typedef` – alias typu tradycyjny**
- `typedef` jest tradycyjnym mechanizmem definiowania aliasów typów, używanym od początków C++.
- Nie obsługuje szablonów wprost (co jest jego głównym ograniczeniem w nowoczesnym C++).

```cpp
typedef unsigned int wiek;
wiek osobaWiek = 25;

// To nie działa z typedef:
typedef std::vector<int> IntVector;
```

### **`using` – nowoczesny alias typu**
- `using` został wprowadzony w C++11 jako alternatywa dla `typedef`.
- Jest bardziej elastyczny i czytelny, szczególnie w przypadku szablonów.

```cpp
using wiek = unsigned int;
wiek osobaWiek = 30;

template <typename T>
using Wektor = std::vector<T>;

Wektor<int> liczby = {1, 2, 3};
std::cout << liczby[0] << "\n"; // Wyświetla 1

```

### **Kiedy używać `using` zamiast `typedef`?**
- W nowoczesnym C++ (`C++11` i nowsze) **zawsze preferuj `using`**, szczególnie w przypadku szablonów.
- `typedef` może być stosowany w starszym kodzie lub gdy współpracujesz z bibliotekami napisanymi w starszym standardzie C++.
#### **Struktury (`struct`)**
Struktury to grupowanie powiązanych danych w jeden typ.

```cpp
struct Punkt {
    int x;
    int y;
};

Punkt p = {3, 4};
std::cout << "Punkt: (" << p.x << ", " << p.y << ")\n";
```

#### **Klasy (`class`)**
Klasy to bardziej zaawansowane struktury, które mogą zawierać funkcje i enkapsulację.

```cpp
class Punkt3D {
private:
    int x, y, z;

public:
    Punkt3D(int a, int b, int c) : x(a), y(b), z(c) {}

    void wypisz() {
        std::cout << "(" << x << ", " << y << ", " << z << ")\n";
    }
};

Punkt3D p(1, 2, 3);
p.wypisz();
```

---
### **Struktury danych w STL**
Standardowa Biblioteka Szablonów (STL) dostarcza różnorodne struktury danych, które można łatwo wykorzystać w programach.

#### **Kontenery sekwencyjne**
Przechowują dane w sposób liniowy.

**`std::vector`**: Dynamiczna tablica o zmiennym rozmiarze.

```cpp
std::vector<int> vec = {1, 2, 3};
vec.push_back(4);
std::cout << vec.size() << "\n";
```

**`std::deque`**: Dwukierunkowa kolejka (elementy można dodawać i usuwać z obu stron).

```cpp
#include <deque>
std::deque<int> dq = {1, 2, 3};
dq.push_front(0);
dq.push_back(4);
```

**`std::list`**: Lista dwukierunkowa. Wolniejsza od `std::vector` w dostępie, ale szybsza w operacjach wstawiania/usuwania.

```cpp
#include <list>
std::list<int> lst = {1, 2, 3};
lst.push_back(4);
```

#### **Kontenery asocjacyjne**
Przechowują dane w sposób uporządkowany lub według klucza.

**`std::set`**: Zbiór unikalnych elementów w uporządkowanej kolejności.

```cpp
#include <set>
std::set<int> zbior = {3, 1, 4};
zbior.insert(2);
```

**`std::map`**: Przechowuje pary klucz-wartość w uporządkowanym porządku kluczy.

```cpp
#include <map>
std::map<std::string, int> mapa;
mapa["Ala"] = 10;
mapa["Jan"] = 20;
```

#### **Kontenery niesekwencyjne (C++11 i nowsze)**

**`std::unordered_set`**: Zbiór unikalnych elementów bez określonej kolejności.

```cpp
#include <unordered_set>
std::unordered_set<int> zbior = {3, 1, 4};
```

**`std::unordered_map`**: Przechowuje pary klucz-wartość bez określonej kolejności kluczy.

```cpp
#include <unordered_map>
std::unordered_map<std::string, int> mapa;
mapa["Ala"] = 10;
mapa["Jan"] = 20;
```

### **Algorytmy STL**
STL zawiera zestaw gotowych algorytmów, które można stosować na kontenerach:
- **`std::sort`**: Sortowanie elementów.
- **`std::find`**: Szukanie elementu.
- **`std::for_each`**: Iteracja po elementach.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> vec = {5, 1, 4, 2};
    std::sort(vec.begin(), vec.end()); // Sortowanie
    for (int v : vec) {
        std::cout << v << " ";
    }
    return 0;
}
```