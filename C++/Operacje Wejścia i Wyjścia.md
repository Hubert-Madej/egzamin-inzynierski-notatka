Operacje wejścia/wyjścia (I/O) w C++ są realizowane za pomocą standardowej biblioteki strumieniowej. Strumienie pozwalają na czytanie danych od użytkownika (wejście) i wyświetlanie ich (wyjście), a także na pracę z plikami i innymi źródłami danych. 

Najczęściej używane strumienie to:
- `std::cin` – wejście standardowe (zazwyczaj klawiatura).
- `std::cout` – wyjście standardowe (zazwyczaj konsola).
- `std::cerr` – wyjście standardowe do raportowania błędów.
- `std::clog` – wyjście standardowe do logowania.

# Podstawowe operacje wejścia / wyjścia
#### **Wejście – `std::cin`**
`std::cin` służy do pobierania danych od użytkownika. Używa operatora `>>` (operator ekstrakcji).

```cpp
#include <iostream>
#include <string>

int main() {
    int liczba;
    std::string tekst;

    std::cout << "Podaj liczbę: ";
    std::cin >> liczba;

    std::cout << "Podaj tekst: ";
    std::cin.ignore(); // Pomija znak nowej linii pozostały w buforze
    std::getline(std::cin, tekst); // Pobiera cały wiersz

    std::cout << "Podana liczba: " << liczba << "\n";
    std::cout << "Podany tekst: " << tekst << "\n";
    return 0;
}
```

`std::cin` ignoruje białe znaki (spacje, tabulatory) przy pobieraniu pojedynczych wartości. Funkcja `std::getline` umożliwia wczytanie całej linii tekstu, łącznie z białymi znakami.

#### **Wyjście – `std::cout`**
`std::cout` służy do wyświetlania danych na standardowym wyjściu. Używa operatora `<<` (operator wstawiania).

```cpp
#include <iostream>

int main() {
    int liczba = 42;
    std::cout << "Witaj w C++!\n";
    std::cout << "Liczba: " << liczba << "\n";
    return 0;
}
```

`std::endl` służy do zakończenia linii i wymuszenia opróżnienia bufora wyjścia (flush). Znak `\n` kończy linię, ale nie wymusza opróżnienia bufora.

#### **Strumienie do błędów – `std::cerr` i `std::clog`**
`std::cerr` służy do raportowania błędów, wypisuje natychmiast (bez buforowania):

```cpp
std::cerr << "Wystąpił błąd!\n";
```

`std::clog` służy do logowania komunikatów, wypisuje z buforowaniem:

```cpp
std::clog << "Log: Program rozpoczął działanie.\n";
```

### **Formatowanie wyjścia**
Do formatowania wyjścia w C++ służą funkcje z biblioteki `<iomanip>`.

### Przykład:
```cpp
#include <iostream>
#include <iomanip>

int main() {
    double liczba = 123.456789;
    std::cout << std::fixed << std::setprecision(2) 
    << liczba << "\n"; // 123.46
    return 0;
}  
```

---
# Operacje na plikach
Do operacji na plikach używa się bibliotek `<fstream>`, `<ifstream>` (do odczytu), i `<ofstream>` (do zapisu).

#### **Podstawowy zapis do pliku:**
```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream plik("dane.txt");
    if (plik.is_open()) {
        plik << "Zapisujemy dane do pliku.\n";
        plik.close();
    } else {
        std::cerr << "Nie można otworzyć pliku!\n";
    }
    return 0;
}
```

#### **Podstawowy odczyt z pliku:**

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ifstream plik("dane.txt");
    std::string linia;

    if (plik.is_open()) {
        while (std::getline(plik, linia)) {
            std::cout << linia << "\n";
        }
        plik.close();
    } else {
        std::cerr << "Nie można otworzyć pliku!\n";
    }
    return 0;
}
```

#### **Strumienie binarne:**
Do odczytu i zapisu binarnego używa się flagi `std::ios::binary`.

```cpp
std::ofstream plik("dane.bin", std::ios::binary);
```