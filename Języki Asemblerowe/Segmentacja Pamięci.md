### **Wprowadzenie**
Segmentacja [1](https://en.wikipedia.org/wiki/X86_memory_segmentation) [2](https://en.wikipedia.org/wiki/Virtual_8086_mode) [3](https://en.wikipedia.org/wiki/Real_mode) [4](https://www.eejournal.com/article/mastering-x86-memory-segmentation/) pamięci w architekturze x86 to mechanizm umożliwiający podział przestrzeni adresowej na logiczne segmenty, co pozwala na efektywne zarządzanie pamięcią oraz ochronę danych. W zależności od trybu pracy procesora, segmentacja realizowana jest w różny sposób, oferując odmienne funkcje i możliwości.

---

### **Tryb rzeczywisty (Real Mode)**
Tryb rzeczywisty, znany również jako tryb adresowania rzeczywistego, jest podstawowym trybem operacyjnym wszystkich procesorów zgodnych z architekturą x86. Nazwa pochodzi od faktu, że adresy w tym trybie bezpośrednio odpowiadają rzeczywistym lokalizacjom w pamięci. Tryb ten charakteryzuje się:
- **20-bitową przestrzenią adresową**, umożliwiającą dostęp do maksymalnie 1 MB pamięci.
- **Bezpośrednim dostępem** oprogramowania do całej adresowalnej pamięci, adresów I/O oraz sprzętu peryferyjnego.
- **Brakiem wsparcia** dla ochrony pamięci, wielozadaniowości czy poziomów uprawnień kodu.

W trybie rzeczywistym procesor rozpoczyna pracę po włączeniu zasilania, aby zapewnić kompatybilność wsteczną z wcześniejszymi procesorami x86.
##### **Mechanizm adresowania**
W trybie rzeczywistym adres fizyczny obliczany jest poprzez kombinację:
- **Rejestru segmentowego**: zawiera adres segmentu przesunięty o 4 bity w lewo.
- **Offsetu**: określa przesunięcie wewnątrz segmentu.

Obliczenie adresu fizycznego odbywa się według wzoru:
$$
Adres \ Fizyczny \ = \ (Rejestr Segmentowy \ \times \ 16) \ + \ Offset
$$
Taki sposób adresowania pozwala na dostęp do 1 MB pamięci, jednak brak mechanizmów ochrony pamięci i wielozadaniowości stanowi istotne ograniczenie tego trybu.

---

### **Tryb chroniony (Protected Mode)**

Tryb chroniony, znany również jako tryb chronionego adresowania wirtualnego, to zaawansowany tryb operacyjny procesorów zgodnych z x86, wprowadzony w procesorze Intel 80286. Umożliwia on systemowi operacyjnemu korzystanie z funkcji takich jak:
- **Segmentacja**: podział pamięci na segmenty z określonymi prawami dostępu.
- **Pamięć wirtualna**: umożliwia korzystanie z większej przestrzeni adresowej niż dostępna fizycznie.
- **Stronicowanie**: mapowanie adresów liniowych na fizyczne, umożliwiające efektywne zarządzanie pamięcią.
- **Bezpieczna wielozadaniowość**: izolacja procesów i ochrona zasobów systemowych.

Po włączeniu zasilania procesor rozpoczyna pracę w trybie rzeczywistym. Przejście do trybu chronionego następuje po odpowiedniej konfiguracji przez system operacyjny, w tym ustawieniu tablicy deskryptorów i ustawieniu bitu PE (Protection Enable) w rejestrze kontrolnym CR0.

###### **Mechanizm adresowania**
W trybie chronionym adresowanie odbywa się poprzez:
1. **Selektor segmentu**: 16-bitowa wartość w rejestrze segmentowym, wskazująca na deskryptor w tablicy deskryptorów (GDT lub LDT).
2. **Offset**: przesunięcie względem początku segmentu.

Adres liniowy obliczany jest jako suma bazowego adresu segmentu (pobrany z deskryptora) i offsetu:
$$
Adres \ Liniowy \ = \ Adres \ Bazowy \ + \ Offset
$$

Adres liniowy może być następnie przekształcony na adres fizyczny za pomocą mechanizmu stronicowania.

**Deskryptor segmentu** to struktura danych używana w trybie chronionym procesorów x86 do opisu właściwości segmentu pamięci. Jest przechowywany w specjalnych tabelach, takich jak **Globalna Tabela Deskryptorów (GDT)** lub **Lokalna Tabela Deskryptorów (LDT)**.

Deskryptor segmentu zawiera informacje niezbędne do zidentyfikowania segmentu i jego właściwości, takie jak:
- **Bazowy adres segmentu** – początek segmentu w przestrzeni adresowej.
- **Limit segmentu** – rozmiar segmentu.
- **Prawa dostępu** – określające operacje, jakie mogą być wykonywane na segmencie.
- **Flagi** – dodatkowe informacje, takie jak granularność segmentu i jego zachowanie.
### **Definicja deskryptora segmentu**

**Deskryptor segmentu** to struktura danych używana w trybie chronionym procesorów x86 do opisu właściwości segmentu pamięci. Jest przechowywany w specjalnych tabelach, takich jak **Globalna Tabela Deskryptorów (GDT)** lub **Lokalna Tabela Deskryptorów (LDT)**.

Deskryptor segmentu zawiera informacje niezbędne do zidentyfikowania segmentu i jego właściwości, takie jak:

- **Bazowy adres segmentu** – początek segmentu w przestrzeni adresowej.
- **Limit segmentu** – rozmiar segmentu.
- **Prawa dostępu** – określające operacje, jakie mogą być wykonywane na segmencie.
- **Flagi** – dodatkowe informacje, takie jak granularność segmentu i jego zachowanie.

| **Bity**  | **Opis**                                                                   |
| --------- | -------------------------------------------------------------------------- |
| **0–15**  | **Limit segmentu (część dolna)** – niskie 16 bitów limitu segmentu.        |
| **16–31** | **Bazowy adres segmentu (część dolna)** – niskie 16 bitów adresu bazy.     |
| **32–39** | **Bazowy adres segmentu (część środkowa)** – bity 16–23 adresu bazy.       |
| **40–43** | **Flagi i limit (część górna)** – 4 wyższe bity limitu oraz flaga G.       |
| **44–47** | **Typ i prawa dostępu** – typ segmentu, poziom uprawnień, status segmentu. |
| **48–55** | **Flagi i baza segmentu (część górna)** – flagi i bity 24–31 adresu bazy.  |
| **56–63** | **Bazowy adres segmentu (część górna)** – najwyższe bity adresu bazy.      |

|**Pole**|**Rozmiar**|**Opis**|
|---|---|---|
|**Limit segmentu**|20 bitów|Określa rozmiar segmentu: od 1 bajta do 1 MB (lub 4 GB przy granularności 4 KB).|
|**Bazowy adres segmentu**|32 bity|Wskazuje początek segmentu w przestrzeni adresowej.|
|**Typ segmentu**|4 bity|Określa rodzaj segmentu: kod, dane, stos itp.|
|**DPL (Descriptor Privilege Level)**|2 bity|Określa poziom uprawnień segmentu (Ring 0–3).|
|**P (Present)**|1 bit|Wskazuje, czy segment jest załadowany do pamięci (1 – obecny, 0 – nieobecny).|
|**Granularity (G)**|1 bit|Określa jednostkę limitu: 0 – bajty, 1 – 4 KB jednostki.|
|**Default operation size (D/B)**|1 bit|Określa rozmiar operacji: 0 – 16-bitowe, 1 – 32-bitowe.|
|**AVL (Available)**|1 bit|Flaga dostępna dla systemu operacyjnego do dowolnego użytku.|

| **Tabela** | **Nr deskryptora** | **Opis segmentu**         | **Bazowy adres** | **Limit** | **Prawa dostępu** |
| ---------- | ------------------ | ------------------------- | ---------------- | --------- | ----------------- |
| **GDT**    | 0                  | Null descriptor           | -                | -         | -                 |
|            | 1                  | Segment kodu (globalny)   | `0x00000000`     | `4 GB`    | Odczyt, wykonanie |
|            | 2                  | Segment danych (globalny) | `0x10000000`     | `2 GB`    | Odczyt, zapis     |
|            | 3                  | Segment stosu (globalny)  | `0x20000000`     | `1 GB`    | Odczyt, zapis     |
| **LDT**    | 0                  | Segment kodu (lokalny)    | `0x30000000`     | `64 KB`   | Odczyt, wykonanie |
|            | 1                  | Segment danych (lokalny)  | `0x30010000`     | `128 KB`  | Odczyt, zapis     |
|            | 2                  | Segment stosu (lokalny)   | `0x30020000`     | `64 KB`   | Odczyt, zapis     |
###### **Poziomy uprawnień (Privilege Levels)**
Tryb chroniony wprowadza koncepcję **pierścieni ochrony** (protection rings), które definiują poziomy uprawnień kodu wykonywanego na procesorze. W architekturze x86 dostępne są cztery poziomy uprawnień, oznaczone jako **Ring 0** (najwyższy poziom uprawnień) do **Ring 3** (najniższy poziom uprawnień). Systemy operacyjne zazwyczaj wykorzystują tylko dwa z tych poziomów:
- **Ring 0**: dla kodu jądra systemu operacyjnego (kernel).
- **Ring 3**: dla aplikacji użytkownika.

Mechanizm ten zapewnia izolację i ochronę między różnymi poziomami kodu, zapobiegając nieautoryzowanemu dostępowi do zasobów systemowych.

---

### **Przejście między trybami**
Procesory x86 rozpoczynają pracę w trybie rzeczywistym po włączeniu zasilania, aby zapewnić kompatybilność wsteczną. Przejście do trybu chronionego wymaga:

1. **Utworzenie i zainicjalizowanie GDT (Global Descriptor Table)**:
    - System operacyjny tworzy Globalną Tabelę Deskryptorów (GDT), która zawiera deskryptory definiujące segmenty używane w trybie chronionym.
    - Każdy deskryptor określa:
        - Bazowy adres segmentu.
        - Limit segmentu.
        - Prawa dostępu.
2. **Załadowanie adresu GDT do rejestru GDTR**:
    - Rejestr GDTR przechowuje adres bazy GDT oraz jej rozmiar.
    - Instrukcja `lgdt` (Load Global Descriptor Table Register) ładuje adres nowej tabeli.
3. **Włączenie trybu chronionego**:
    - Ustawiany jest bit **PE (Protection Enable)** w rejestrze kontrolnym **CR0**.
    - Procesor przechodzi do trybu chronionego, ale musi zostać odpowiednio skonfigurowany (np. przeładowanie segmentów).
4. **Przeładowanie rejestrów segmentowych**:
    - Po przejściu do trybu chronionego, wszystkie rejestry segmentowe muszą zostać przeładowane przy użyciu selektorów wskazujących na poprawne deskryptory w GDT.
5. **Opcjonalne włączenie stronicowania**:
    - Jeśli system korzysta z pamięci wirtualnej, stronicowanie jest aktywowane poprzez ustawienie bitu PG (Paging Enable) w CR0.

###### **Powrót do trybu rzeczywistego**
- Procesor może wrócić do trybu rzeczywistego, wyłączając bit PE w CR0, jednak wymaga to dodatkowej konfiguracji (np. przeładowanie rejestrów segmentowych).

### **Współczesne zastosowania segmentacji**

###### **Płaski model pamięci**
- Nowoczesne systemy operacyjne, takie jak Linux czy Windows, korzystają z **płaskiego modelu pamięci**, w którym segmentacja jest uproszczona:
    - Bazowy adres segmentu ustawiany jest na `0`.
    - Limit segmentu ustawiany jest na maksymalną wartość (np. 4 GB w 32-bitowym systemie).
- Dzięki temu segmentacja staje się przezroczysta dla programów, a zarządzanie pamięcią odbywa się głównie poprzez stronicowanie.

###### **Tryb 64-bitowy (Long Mode)**
- W trybie 64-bitowym segmentacja jest w dużej mierze nieaktywna:
    - Większość rejestrów segmentowych ma stałe wartości.
    - Bazowy adres segmentu jest ignorowany, z wyjątkiem rejestrów **FS** i **GS**:
        - Rejestr FS: używany np. do przechowywania danych specyficznych dla wątku.
        - Rejestr GS: często używany w systemach operacyjnych do przechowywania wskaźników na struktury systemowe.
- Stronicowanie odgrywa kluczową rolę w zarządzaniu pamięcią.

---

### **Historia i ewolucja trybów**
###### **Tryb rzeczywisty (Real Mode)**
- Wprowadzony w procesorach Intel 8086 (1978) jako podstawowy model adresowania.
- Zapewniał zgodność z wcześniejszymi systemami opartymi na 8-bitowych procesorach.

###### **Tryb chroniony (Protected Mode)**
- Wprowadzony w procesorze Intel 80286 (1982) jako odpowiedź na potrzebę ochrony pamięci i wielozadaniowości.
- Rozbudowany w procesorze Intel 80386 (1985) o mechanizmy stronicowania i 32-bitową przestrzeń adresową.
- Stał się fundamentem nowoczesnych systemów operacyjnych.

###### **Tryb 64-bitowy (Long Mode)**
- Wprowadzony przez AMD w architekturze x86-64 (2003).
- Zastąpił segmentację stronicowaniem jako głównym mechanizmem zarządzania pamięcią.

---

### **Podsumowanie**
Segmentacja pamięci w architekturze x86 była jednym z kluczowych mechanizmów zarządzania pamięcią od początków tej architektury. Od trybu rzeczywistego, oferującego prosty model segmentacji, po tryb chroniony z zaawansowaną ochroną i stronicowaniem, segmentacja ewoluowała w odpowiedzi na potrzeby coraz bardziej złożonych systemów operacyjnych. Współczesne systemy operacyjne upraszczają segmentację lub w dużej mierze ją pomijają na rzecz stronicowania, które jest bardziej elastyczne i wydajne w zarządzaniu pamięcią wirtualną.