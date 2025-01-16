Zarządzanie pamięcią w C++ jest kluczowym aspektem programowania, ponieważ język daje programiście dużą kontrolę nad alokacją i zwalnianiem pamięci. Wraz z wprowadzeniem wskaźników inteligentnych w C++11 i dalszym ich rozwojem, zarządzanie pamięcią stało się bardziej bezpieczne i wygodne.

---
# Zarządzanie pamięcią

Pamięć w C++ dzieli się na:
1. Pamięć stosu (**stack**): Używana do przechowywania zmiennych lokalnych i parametrów funkcji. Pamięć jest zwalniana automatycznie po zakończeniu zakresu zmiennej. Zapewnia szybki dostęp, ale jest ograniczona wielkościowo.
   
```cpp
void funkcja() {
    int x = 10; // Zmienna `x` jest na stosie
} // Pamięć `x` jest automatycznie zwalniana
```
   
2. Pamięć sterty (**heap**): Używana jest do dynamicznego przydzielania pamięci. Zarządzana jest ręcznie przy pomocy operatorów `new` i `delete`. Zapewnia większą elastyczność w rozmiarze, ale istnieje większe ryzyko błędów.

```cpp
int* ptr = new int(10); // Alokacja na stercie
delete ptr; // Zwalnianie pamięci
```

Problemy w zarządzaniu pamięcią:
- Wycieki pamięci - niezwolniona pamięć po jej użyciu.
- Podwójne zwolnienie - próba zwolnienia tej samej pamięci więcej niż jeden raz.
- Dereferencja pustego wskaźnika - próba użycia wskaźnika wskazującego na `nullptr`.

---
# Wskaźniki (raw pointers)

Wskaźniki to zmienne, które przechowują adres innej zmiennej. Są podstawowym mechanizmem zarządzania pamięcią i dostępem do zasobów w C++.

### Deklaracja i użycie wskaźników - Podstawowe wskaźniki

```cpp
int x = 10;
int * ptr = &x; // Wskaźnik do `x`.

std::cout << *ptr << "\n"; // Dereferecnja, wyświetla wartość `x`
```

### Deklaracja i użycie wskaźników - Dynamiczna alokacja pamięci

```cpp
int *ptr = new int(20); // Alokacja dynamiczna
std::cout << *ptr << "\n"; // 20
delete ptr; // Zwolnienie pamięci
```

### Deklaracja i użycie wskaźników - Pusty Wskaźnik

Wprowadzono w C++11, `nullptr` reprezentuje wskaźnik, który niczego nie wskazuje.

```cpp
int* ptr = nullptr;
if (!ptr) {
    std::cout << "Wskaźnik jest pusty\n";
}
```

### Przykłady operacji na wskaźnikach - Tablice

```cpp
int* tab = new int[5]; // Dynamiczna tablica
tab[0] = 10;
delete[] tab; // Zwolnienie pamięci
```

### Przykłady operacji na wskaźnikach - Wskaźniki do funkcji

```cpp
void funkcja() {
    std::cout << "Wywołano funkcję!\n";
}
void (*wskFunkcja)() = funkcja;
wskFunkcja(); // Wywołanie przez wskaźnik
```

### Przykłady operacji na wskaźnikach - Wskaźniki wielowymiarowe

```cpp
int** tablica2D = new int*[3];
for (int i = 0; i < 3; ++i) {
    tablica2D[i] = new int[4];
}
for (int i = 0; i < 3; ++i) {
    delete[] tablica2D[i];
}
delete[] tablica2D;
```

# Wskaźniki Inteligentne (smart Pointers)

Wskaźniki inteligentne to obiekty zarządzające dynamicznie przydzieloną pamięcią, eliminując ryzyko wycieków pamięci i innych błędów związanych z zarządzaniem pamięcią.

### Rodzaje wskaźników inteligentnych

`std::unique_ptr` - Wskazuje na zasób, który ma tylko jednego właściciela. Automatycznie zwalnia pamięć po zakończeniu zakresu. Przypisanie wskaźnika jest niemożliwe (brak kopiowania), ale można go przenieść. 

```cpp
#include <memory>
std::unique_ptr<int> ptr = std::make_unique<int>(10);
std::cout << *ptr << "\n";
```

`std::shared_ptr` - Wskazuje na zasób, który może mieć wielu współdzielonych właścicieli. Zarządza referencją i zwalnia pamięć, gdy liczba właścicieli spadnie do 0.

```cpp
#include <memory>
std::shared_ptr<int> ptr1 = std::make_shared<int>(20);
std::shared_ptr<int> ptr2 = ptr1; // Współdzielony zasób
std::cout << *ptr2 << "\n";
```

`std::weak_ptr` - Wskazuje na zasób współdzielony przez `std::shared_ptr`, ale nie zwiększa liczby referencji. Stosowany jest w celu uniknięcia cyklicznych zależności.

```cpp
#include <memory>
std::shared_ptr<int> shared = std::make_shared<int>(30);
std::weak_ptr<int> weak = shared;
if (auto ptr = weak.lock()) {
    std::cout << *ptr << "\n";
}
```

```cpp
struct Node {
    std::shared_ptr<Node> next;
    std::weak_ptr<Node> prev; // Słaby wskaźnik unika cyklu
};

auto node1 = std::make_shared<Node>();
auto node2 = std::make_shared<Node>();

node1->next = node2;
node2->prev = node1;
```
---
# Referencje

Referencje to aliasy dla istniejących zmiennych. W przeciwieństwie do wskaźników, referencje muszą być inicjalizowane w momencie deklaracji i nie mogą być `nullptr`.

```cpp
int x = 10;
int& ref = x; // Referencja do `x`
std::cout << ref << "\n"; // Wyświetla 10
ref = 20; // Modyfikacja `x` przez referencję
std::cout << x << "\n"; // Wyświetla 20
```

### Rodzaje referencji

**Referencje do wartości** - odnoszą się do zmiennych, które istnieją w pamięci.

```cpp
int x = 42;
int& ref = x;
```

**Referencje do r-wartości** - odnoszą się do obiektów tymczasowych, które nie mają nazwy. Używane są do przenoszenia zasobów.

```cpp
int&& rref = 42; // Referencja do tymczasowej wartości
```

```cpp
std::string str = "Hello"; 
std::string moved = std::move(str); // Przenosi zasób, `str` staje się pusty
```

### Zastosowanie referencji

Przekazywanie argumentów przez referencje - przekazywanie argumentów przez referencje pozwala na modyfikacje oryginalnych danych:

```cpp
void zmien(int& liczba) {
    liczba *= 2;
}
int x = 10;
zmien(x);
std::cout << x << "\n"; // Wyświetla 20
```

Przekazywanie obiektów bez kopiowania:

```cpp
void wypisz(const std::string& tekst) {
    std::cout << tekst << "\n";
}
```

Wskaźniki inteligentne w C++ mają wiele zalet, takich jak automatyczne zarządzanie pamięcią i zwiększenie bezpieczeństwa kodu, jednak nie są wolne od wad. Oto główne ograniczenia i potencjalne wady wskaźników inteligentnych:

### **1. Narzut wydajności**

- **Zarządzanie licznością referencji (dla `std::shared_ptr`)**:
    - `std::shared_ptr` zarządza licznikiem referencji, co wymaga dodatkowych operacji przy kopiowaniu, tworzeniu i usuwaniu wskaźników.
    - W kontekście wielowątkowym licznik referencji jest atomowy, co może być kosztowne w systemach o dużej równoległości.
- **Złożoność konstrukcji i destrukcji**:
    - `std::shared_ptr` oraz `std::unique_ptr` mogą wprowadzać narzut czasowy podczas tworzenia i niszczenia obiektów w porównaniu do surowych wskaźników (`raw pointers`).

### **2. Możliwość cyklicznych zależności (`std::shared_ptr`)**

- **Problem**:
    - Jeśli dwa obiekty posiadają `std::shared_ptr` do siebie nawzajem, tworzy to cykl, w którym licznik referencji nigdy nie spadnie do zera, a pamięć nigdy nie zostanie zwolniona.
- **Rozwiązanie**:
    - Użycie `std::weak_ptr` do przełamywania cyklicznych zależności, ale wymaga to dodatkowej uwagi i planowania przez programistę.
- **Przykład problemu:**

```cpp
struct A {
    std::shared_ptr<B> ptr;
};
struct B {
    std::shared_ptr<A> ptr;
};

auto a = std::make_shared<A>();
auto b = std::make_shared<B>();
a->ptr = b;
b->ptr = a; // Cykl, który prowadzi do wycieku pamięci 
```
### **3. Ograniczona elastyczność**

- **Brak wsparcia dla wskaźników "weak ownership" w `std::unique_ptr`**:
    - `std::unique_ptr` nie obsługuje słabych referencji (`weak ownership`), co oznacza, że zasób może być dostępny tylko przez jednego właściciela. W niektórych przypadkach wymaga to dodatkowej logiki, aby uzyskać współdzielony dostęp.
- **Niezgodność z niektórymi interfejsami i API**:
    - Wiele starszych bibliotek C++ i interfejsów wymaga tradycyjnych wskaźników (`raw pointers`), co wymusza konwersję wskaźników inteligentnych, np. przez użycie metody `.get()`. Może to prowadzić do potencjalnych błędów:
        
```cpp
auto ptr = std::make_unique<int>(42);
funkcjaAPI(ptr.get()); // Funkcja oczekuje `int*`
```