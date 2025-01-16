Spis treści
1. Mechanizm wywołania funkcji
2. Heap vs Stack
3. Deklaracja i definicja funkcji
4. Typ zwracany i argumenty
5. Typy parametrów
6. Funkcje specjalne
	1. Inline
	2. Constexpr
	3. Lambda

---
Funkcje w C++ są kluczowym mechanizmem modularności, umożliwiającym podział kodu na mniejsze, wielokrotnie używane fragmenty. Ich zrozumienie obejmuje kilka aspektów: mechanizm wywołania, różnicę między deklaracją a definicją, sposób przekazywania argumentów, obsługę typów zwracanych oraz zastosowanie rekursji.

---
### Mechanizm Wywołania:

1. Przekazywanie argumentów:
	1. Argumenty są przekazywane do funkcji zgodnie z konwencją wywołania (np. cdecl, stdcall, fastcall), która określa:
	2. Czy argumenty są przekazywane na stos, czy w rejestrach.
	3. Kolejność przekazywania argumentów (od lewej do prawej lub odwrotnie).
	4. Kto odpowiada za oczyszczenie stosu (wywołujący czy funkcja).
2. Zapis kontekstu:
	1. Obecny stan programu (rejestry, wskaźnik stosu) jest zapisywany, aby umożliwić powrót na miejsce wywołania po zakończeniu funkcji.
3. Przejście sterowania:
	1. Procesor przechodzi do adresu początku funkcji.
	2. Wykonanie kodu funkcji:
	3. Funkcja wykonuje swój kod, korzystając z argumentów i zmiennych lokalnych.
4. Zwrócenie wyniku i oczyszczenie stosu:
	1. Wynik zwracany przez funkcję jest umieszczony w odpowiednim rejestrze np. EAX dla liczb całkowitych w architekturze x86.
	2. Sterowanie wraca do miejsca wywołania a stos jest oczyszczany.

---
### Mechanizm Wywołania (uproszczony)

1. Na stosie zostaje utworzona ramka funkcji
2. Następnie do niej trafiają:
    - Parametry funkcji w odwrotnej kolejności niż podane
    - Adres miejsca do którego ma wrócić program po zakończeniu funkcji
    - Jest rezerwowane miejsce na zmienne lokalne, które pojawiają się w funkcji
    - Funkcja jest wykonywana
  
Źródła
1. https://www.youtube.com/watch?v=aCPkszeKRa4
2. https://www.youtube.com/watch?v=Q2sFmqvpBe0
3. https://www.youtube.com/watch?v=uG_JOJgwbco

---
### Heap vs Stack

Stos - lokalna pamięć wykorzystywana przy wywołaniu funkcji. To tutaj trafiają zmienne, które deklarujemy.

Heap - pamięć przeznaczona do dynamicznej alokacji funkcji. To stąd zostaje przyznana pamięć programowi, który używa wskaźników.

---
### Deklaracja, i definicja funkcji:
1. Deklaracja funkcji:
	1. Deklaracja informuje kompilator o istnieniu funkcji i jej sygnaturze (nazwie, typie zwracanym i parametrach), ale nie zawiera implementacji. Używamy ją często w plikach nagłówkowych.
2. Definicja funkcji:
	1. Definicja zawiera pełną implementację funkcji.

```cpp
int dodaj(int a, int b); // Deklaracja
int dodaj(int a, int b) { return a + b; } // Definicja
```

---
### Typ zwracany i argumenty

Funkcja może zwracać wartość dowolnego typu, w tym:
- Typy proste (`int`, `float`, `double`).
- Obiekty użytkownika (np. klasy). 
- Wskaźniki i referencje.

Funkcja może również nie zwracać wartości, używają słowa kluczowego void.

---
### Typy parametrów:

W języku C++ parametry funkcji można przekazywać na różne sposoby, zależnie od potrzeb: przez wartość, referencję lub wskaźnik. Każde z tych podejść ma swoje zalety i ograniczenia.

**Przez wartość** - Argument jest kopiowany do zmiennej lokalnej wewnątrz funkcji. Funkcja operuje na kopii, a zmiany dokonane na parametrze nie wpływają na oryginalną zmienną. Używamy wtedy kiedy chcemy zapewnić bezpieczeństwo oryginalnych danych i nie pozwalać funkcji na ich modyfikację, lub dla prostych typów gdzie kopia nie jest kosztowna. Zaletą tego typu parametru jest bezpieczeństwo dla oryginalnych danych oraz eliminacja ryzyka zmiennych spoza funkcji, wada natomiast koszt kopiowania dla złożonych typów.  
  
### Przykład:   
```cpp
void zmienWartosc(int x) {
	x = 10; //Zmienna 'x' to lokalna kopia.
}

int liczba = 5;
zmienWartosc(liczba);
std::cout << liczba; // 5 (oryginalna zmienna nie została zmieniona).
```

**Przez referencje** - Funkcja otrzymuje referencje do oryginalnej zmiennej. Zmiany w parametrze wpływają na oryginalną zmienną. Stosujemy ją, gdy chcemy aby funkcja modyfikować dane, lub dla dużych obiektów gdzie kopiowanie jest kosztowne. W porównaniu do przekazywania parametru przez wartości, jest to podejście wymagające większej ostrożności (jeżeli nie użyjemy `const`)  
  
Przykład:  
```cpp
void zmienWartosc(int& x) {
	x = 10; // Modyfikacja oryginalnej zmiennej.
}

int liczba = 5;
zmienWartosc(liczba);
std::cout << liczba; // 10 (oryginalna zmienna została zmieniona).
```
  
Przekazywanie dużych obiektów przez referencje:
```cpp
void pokazDane(const std::string& dane) { // 'const' zapobiega modyfikacji
	std::cout << dane << std::endl;
}

std::string tekst = "Tekst";
pokazDane(tekst);
```
  
**Przez wskaźnik** - Funkcja przyjmuje wskaźnik (adres zmiennej). Wymaga to jawnego operatora & podczas wywołania funkcji oraz dereferencji (\*) w ciele funkcji. Stosujemy, gdy chcemy aby funkcja zmodyfikowała oryginalną zmienną, lub przekazać wskaźnik null (np. Opcjonalne przekazywanie wartości). Kolejnym przypadkiem użycia jest kod, w którym używamy dynamicznie alokowanej pamięci.  
  
### Przykład:  
```cpp
void zmienWartosc(int* x) {
	*x = 10; // Dereferemcka wskaźnika i modyfikacja wartości.
}

int liczba = 5;
zmienWartosc(&liczba); // Przekazanie adresu zmiennej.
std::cout << liczba; // 10 (oryginalna zmienna została zmieniona).
```
  
### Przekazywanie wskaźnika na null:  
```cpp
void sprawdzWskaznik(int* x) {
	if (x == nullptr) {
		std::cout << "Wskaznik jest null." << std::endl;
	} else {
		std::cout << "Wartość: " << *x << std::endl;
	}
}

int liczba = 5;
sprawdzWskaznik(&liczba); // 5
sprawdzWskaznik(nullptr); // Wskaźnik jest null.
```

### Dynamiczna alokacja pamięci przez wskaźnik:  
```cpp
void utworzTablice(int** ptr, int rozmiar) {
	*ptr = new int[rozmiar]; // Alokacja tablicy
}

int *tablica = nullptr;
utworzTablice(&tablica, 5);
tablica[0] = 42;
delete[] tablica; // Zwolnienie pamięci
```

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXep6MgsvAXa1Yu1-jyLxymWMkvC6cDxsW5FUNulO7DoaevHk0uOoU227A6d57okHUhZEBjY-_ZgaEDZ0-gqsk_toTQInxUXZd2TZ1P5qNYmlOhQKrQ_nTkZ--KrhiPX7NCRlfyT?key=LhzamKR2PARjwTU86rGUktuQ)  
  

Przeciążanie funkcji

Można zdefiniować funkcje o tej samej nazwie, ale o różnych listach parametrów czy typie.

## Funkcje specjalne

### Inline
Funkcja oznaczona jako inline jest rozwijana przez kompilator w miejscu wywołania, zamiast tworzenia standardowego mechanizmu wywołania funkcji (przechowywania argumentów na stosie, przechodzenie do funkcji, powrót). Eliminuje to narzut związany z wywołaniem funkcji, ale zwiększa rozmiar kodu. Dodatkowo inline jest tylko sugestia dla kompilatora, jeśli sama funkcja będzie za długa, inline zostanie zignorowany i zostanie wdrożona standardowa procedura.

```cpp
inline int kwadrat(int x) { return x * x ;}
```

### Constexpr
To słowo kluczowe, które oznacza, że funkcja lub zmienna może (i powinna) być obliczana w czasie kompilacji jeśli jest to możliwe. W kontekście funkcji oznacza to, że funkcja zostanie wywołana w czasie kompilacji, jeśli wszystkie jej argumenty są w tym czasie znane. W najnowszym standardzie funkcje  `constexpr` mogą zawierać bardziej złożone instrukcje takie jak `if`, `for`, itp.

```cpp
constexpr int potega(int podstawa, int wykladnik) {
	return (wykladnik == 0) ? 
	1 :
	podstawa * potega(podstawa, wykladnik - 1);
}

int wynik = potega(2, 5); // 32
```

### Lambda
Lambdy to wyrażenia wprowadzające funkcje anonimowe (bez nazwy) w C++. Wprowadzone w C++11, lambdy pozwalają na szybkie definiowanie funkcji w miejscu, gdzie są potrzebne, bez konieczności ich jawnego deklarowania.

```cpp
[przechwycenia](parametry) -> typ_zwrotny { // ciało lambdy };
```

**Przechwycenia (`[]`)**:
- Określają, jakie zmienne z otaczającego zakresu mogą być używane w lambdzie.
- Przykłady:
    - `[x]`: Przechwytuje zmienną `x` przez wartość.
    - `[&x]`: Przechwytuje zmienną `x` przez referencję.
    - `[=]`: Przechwytuje wszystkie zmienne z otaczającego zakresu przez wartość.
    - `[&]`: Przechwytuje wszystkie zmienne z otaczającego zakresu przez referencję.
    - `[=, &x]`: Przechwytuje wszystkie zmienne przez wartość, ale `x` przez referencję.

```cpp
auto suma = [](int x, int y) { return x + y; };
int wynik = suma(3, 4); // 7
```

**Typ zwrotny (`->`)**:
Opcjonalny; jeśli można wywnioskować typ zwracany, nie trzeba go podawać.

```cpp
auto suma = [](int x, int y) -> int { return x + y; };
```

**Lambda z przechwyceniem:**

```cpp
int x = 10; auto mnoznik = [x](int a) { return a * x; }; 
int wynik = mnoznik(5); // 50
```

**Lambda jako parametr:**

```cpp
std::vector<int> liczby = {1, 2, 3, 4, 5};
std::for_each(liczby.begin(), liczby.end(), [](int liczba) {
    std::cout << liczba << " ";
});
```

**Mutable Lambda:**
Domyślnie lambda nie pozwala na modyfikowanie przechwyconych wartości. Można to zmienić korzystając ze słowa kluczowego `mutable`

```cpp
int liczba = 10;
auto lambda = [liczba]() mutable {
    liczba += 5;
    return liczba;
};
std::cout << lambda(); // 15
```