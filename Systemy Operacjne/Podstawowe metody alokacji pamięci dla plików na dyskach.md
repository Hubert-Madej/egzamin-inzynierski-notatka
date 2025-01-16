W systemach plików [alokacja pamięci](https://www.youtube.com/watch?v=B1_er2nGKao) na dysku jest kluczowym procesem zarządzania przestrzenią dla danych. Każdy plik musi być zapisany w fizycznych blokach dysku, a metoda alokacji wpływa na wydajność operacji, takich jak odczyt, zapis czy modyfikacja plików. Wyróżniamy trzy podstawowe metody alokacji: **alokację ciągłą**, **alokację łańcuchową** oraz **alokację indeksowaną**.

### **1. Alokacja ciągła (Contiguous Allocation)**
Dane pliku są zapisywane w kolejnych, przylegających blokach na dysku.

Każdy plik jest opisany przez:
    - **Początkowy blok** – pierwszy blok zajmowany przez plik.
    - **Rozmiar pliku** – liczba kolejnych bloków zajmowanych przez plik.

![[Pasted image 20250106160937.png]]
#### **Zalety**
1. **Wysoka wydajność odczytu i zapisu** – ponieważ bloki pliku są fizycznie sąsiadujące, można je odczytać sekwencyjnie.
2. **Prosta implementacja** – łatwo ustalić, które bloki są zajęte.
#### **Wady**
1. **Fragmentacja zewnętrzna** – z czasem wolne miejsca na dysku mogą być zbyt małe, aby pomieścić nowe pliki.
2. **Trudności z dynamicznym rozszerzaniem pliku** – jeśli sąsiednie bloki są zajęte, plik nie może być powiększony.
---
### **2. Alokacja łańcuchowa (Linked Allocation)**
Dane pliku są przechowywane w dowolnych blokach na dysku. Każdy blok pliku zawiera wskaźnik do następnego bloku. System plików przechowuje wskaźnik do pierwszego bloku każdego pliku.

![[Pasted image 20250106163932.png]]

#### **Zalety**
1. **Brak fragmentacji zewnętrznej** – pliki mogą być przechowywane w rozproszonych blokach.
2. **Dynamiczne rozszerzanie plików** – nowe bloki można łatwo dodać w dowolnym miejscu.
#### **Wady**
1. **Ograniczona wydajność odczytu** – odczyt pliku wymaga podążania za łańcuchem wskaźników.
2. **Awaria wskaźnika** – uszkodzenie jednego bloku lub wskaźnika powoduje utratę dostępu do całej reszty pliku.

---
### **3. Alokacja indeksowana (Indexed Allocation)**
Każdy plik ma własny **blok indeksowy**, który przechowuje listę wskaźników do bloków danych pliku. Bloki danych nie muszą być sąsiednie.
#### **Zalety**
1. **Brak fragmentacji zewnętrznej** – pliki mogą być przechowywane w dowolnych blokach.
2. **Szybki dostęp do danych** – wskaźniki w bloku indeksowym umożliwiają natychmiastowe odwołanie się do dowolnego bloku pliku.
#### **Wady**
1. **Dodatkowy narzut pamięci** – każdy plik wymaga bloku indeksowego.
2. **Ograniczenie liczby bloków** – liczba bloków, które mogą być skojarzone z plikiem, zależy od rozmiaru bloku indeksowego.

![[Pasted image 20250106163946.png]]

---
### **Metody rozwiązywania problemu alokacji pamięci dla dużych plików**
W przypadku bardzo dużych plików, gdy pojedynczy blok indeksowy nie jest w stanie pomieścić wszystkich wskaźników do bloków danych, stosuje się następujące mechanizmy:

### **1. Schemat połączonych wskaźników (Linked Scheme)**

W tym podejściu używa się wielu bloków indeksowych, które są ze sobą połączone za pomocą wskaźników. Każdy blok indeksowy przechowuje:

1. Wskaźniki do bloków danych pliku.
2. Wskaźnik (lub adres) do następnego bloku indeksowego.

#### **Zalety**
- Prosta implementacja.
- Plik może być rozszerzany dynamicznie w miarę potrzeb, ponieważ wystarczy dodać nowy blok indeksowy i połączyć go z istniejącymi.

#### **Wady**
- Wydajność odczytu jest niższa, ponieważ aby uzyskać dostęp do bloku danych znajdującego się daleko w pliku, trzeba przeszukać wiele bloków indeksowych.

#### **Przykład działania**
- Plik wymaga przechowywania wskaźników do 2000 bloków danych.
- Każdy blok indeksowy przechowuje wskaźniki do 100 bloków danych.
- Mechanizm tworzy 20 połączonych bloków indeksowych, gdzie każdy blok wskazuje na kolejny.

### **2. Wielopoziomowe indeksowanie (Multilevel Index)**

W tym podejściu stosuje się hierarchiczną strukturę wskaźników. Zamiast używać jednego bloku indeksowego, wprowadza się:

1. **Blok indeksowy pierwszego poziomu**, który wskazuje na bloki indeksowe drugiego poziomu.
2. Bloki indeksowe drugiego poziomu wskazują na rzeczywiste bloki danych.
3. Struktura może być rozszerzona do trzeciego lub większej liczby poziomów, co pozwala obsługiwać bardzo duże pliki.

#### **Zalety**
- Efektywna obsługa dużych plików dzięki hierarchicznej strukturze wskaźników.
- Możliwość dynamicznego rozszerzania plików poprzez dodawanie kolejnych poziomów.

#### **Wady**
- Każdy dodatkowy poziom indeksowania zwiększa liczbę operacji wejścia/wyjścia potrzebnych do odczytu danych.
- Narzut na pamięć dla bloków indeksowych.

#### **Przykład działania**
- Plik wymaga 10 000 bloków danych.
- Blok indeksowy pierwszego poziomu przechowuje 100 wskaźników, z których każdy wskazuje na blok indeksowy drugiego poziomu.
- Każdy blok indeksowy drugiego poziomu przechowuje wskaźniki do 100 bloków danych.
- Łącznie potrzebne są:
    - 1 blok indeksowy pierwszego poziomu.
    - 100 bloków indeksowych drugiego poziomu.

### **3. Połączony schemat z wykorzystaniem i-węzłów (Combined Scheme – Inodes)**

W systemach plików takich jak **ext2/ext3** stosuje się zaawansowany mechanizm połączonych schematów indeksowania, znany jako **Inode (information node)**. Inode to specjalny blok, który przechowuje:

1. Informacje o pliku, takie jak nazwa, rozmiar, uprawnienia itp.
2. Wskaźniki do bloków danych pliku.

Wskaźniki w Inode są podzielone na różne kategorie:
- **Wskaźniki bezpośrednie**:
    - Wskazują bezpośrednio na bloki danych.
    - Obsługują małe pliki.
- **Wskaźniki pośrednie**:
    - **Jednopoziomowe wskaźniki pośrednie (Single Indirect)** – Wskazują na bloki indeksowe, które z kolei wskazują na bloki danych.
    - **Dwupoziomowe wskaźniki pośrednie (Double Indirect)** – Wskazują na bloki indeksowe drugiego poziomu, które wskazują na bloki indeksowe pierwszego poziomu, a te na bloki danych.
    - **Trójpoziomowe wskaźniki pośrednie (Triple Indirect)** – Wskazują na bloki indeksowe trzeciego poziomu.

#### **Zalety**
- Łączy zalety wskaźników bezpośrednich (szybki dostęp do małych plików) i pośrednich (obsługa bardzo dużych plików).
- Elastyczna i skalowalna struktura.

#### **Wady**
- Skomplikowana implementacja.
- Narzut pamięciowy dla wskaźników pośrednich.

#### **Przykład działania**
- Inode przechowuje 15 wskaźników:
    - **12 wskaźników bezpośrednich** – obsługują pierwsze 12 bloków danych pliku.
    - **1 wskaźnik jednopoziomowy pośredni** – wskazuje na blok indeksowy, który obsługuje kolejne 1024 bloki danych.
    - **1 wskaźnik dwupoziomowy pośredni** – wskazuje na 1 blok indeksowy drugiego poziomu, który obsługuje kolejne 1024 × 1024 bloki danych.
    - **1 wskaźnik trójpoziomowy pośredni** – obsługuje jeszcze większe pliki.

![[Pasted image 20250106164335.png]]