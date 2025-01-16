Pamięć wirtualna [1](https://www.youtube.com/watch?v=A9WLYbE0p-I) [2](https://www.youtube.com/watch?v=8yO2FBBfaB0) to mechanizm umożliwiający uruchamianie programów, które wymagają większej ilości pamięci niż fizycznie dostępna w systemie. Działa poprzez mapowanie logicznych adresów pamięci na adresy fizyczne i wykorzystuje technikę stronicowania. Strony (ang. _pages_) są jednostkami logicznej pamięci wirtualnej, które są ładowane do ram (ang. _frames_) w pamięci fizycznej. Gdy strona wymagana przez proces nie znajduje się w pamięci fizycznej, występuje **błąd strony** (ang. _page fault_), a system musi zastąpić jedną z już załadowanych stron nową.

![[Pasted image 20250106130507.png]]

Wybór strony do zastąpienia jest realizowany przez **algorytmy zastępowania stron**, które mają na celu zminimalizowanie liczby błędów stron i zapewnienie efektywnego działania systemu.

### **Podstawowe pojęcia**
#### **1. Ramki**
- **Ramki (ang. frames)** to jednostki pamięci fizycznej (RAM), w których przechowywane są strony pamięci wirtualnej.
- Jeśli pamięć fizyczna ma 4 GB, a każda ramka ma rozmiar 4 KB, pamięć fizyczna składa się z **1 048 576 ramek**.
- Każda ramka może przechowywać tylko jedną stronę pamięci wirtualnej w danym momencie.
#### **2. Strony**
- **Strony (ang. pages)** to jednostki pamięci wirtualnej.
- Pamięć wirtualna dzieli przestrzeń adresową procesów na strony o stałym rozmiarze (np. 4 KB).
- Kiedy proces potrzebuje dostępu do strony, system operacyjny sprawdza, czy ta strona znajduje się w ramkach. Jeśli nie, występuje **błąd strony** (ang. _page fault_).
#### **3. Odwołania do stron**
- Procesy podczas wykonywania programu dokonują **odwołań do stron** (np. odczyt lub zapis danych w określonym miejscu pamięci).
- Przykładowo, jeśli proces chce odczytać dane z adresu pamięci wirtualnej należącego do strony 5, następuje odwołanie do strony 5.
- System operacyjny sprawdza, czy strona 5 jest w pamięci fizycznej (ramkach). Jeśli nie jest, następuje załadowanie strony 5 do pamięci fizycznej, a jedna z istniejących stron musi zostać usunięta.

### **Jak działa pamięć wirtualna?**
1. Pamięć wirtualna umożliwia procesom korzystanie z większej przestrzeni adresowej niż dostępna pamięć fizyczna (RAM).
2. Strony pamięci wirtualnej są mapowane na ramki pamięci fizycznej za pomocą **tablicy stron**.
3. Jeśli proces odwołuje się do strony, która nie znajduje się w pamięci fizycznej, następuje błąd strony i system operacyjny musi:
    - Znaleźć stronę w pamięci masowej (dysk twardy, SSD).
    - Załadować ją do dostępnej ramki w pamięci fizycznej.
    - Jeśli wszystkie ramki są zajęte, jedna ze stron musi zostać usunięta – tutaj wkracza **algorytm zastępowania stron**.

![[Pasted image 20250106154936.png]]

![[Pasted image 20250106155047.png]]

![[Pasted image 20250106155102.png]]

![[Pasted image 20250106155116.png]]

### **Cele algorytmów zastępowania stron**
1. **Minimalizacja liczby błędów stron** – zmniejszenie liczby sytuacji, w których konieczne jest ładowanie stron z pamięci masowej.
2. **Efektywne wykorzystanie pamięci fizycznej** – optymalne zarządzanie ograniczonymi zasobami pamięci.
3. **Zgodność z zasadą lokalności** – uwzględnienie tendencji procesów do częstego dostępu do tej samej grupy stron (lokalność czasowa) lub stron bliskich sobie (lokalność przestrzenna).

### **Szczegółowe wyjaśnienie algorytmów z przykładami**

#### **Założenia dla wszystkich przykładów**
- Liczba ramek: 3 (w pamięci fizycznej można przechowywać tylko 3 strony jednocześnie).
- Odwołania do stron: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5.

#### **1. FIFO (First In, First Out)**
- FIFO zastępuje stronę, która została załadowana do pamięci najwcześniej.
- Strony są przechowywane w kolejce – pierwsza załadowana wychodzi jako pierwsza.

**Przykład krok po kroku**:
1. Odwołanie do strony **1** – Strona 1 jest ładowana do ramki (błąd strony).
2. Odwołanie do strony **2** – Strona 2 jest ładowana do ramki (błąd strony).
3. Odwołanie do strony **3** – Strona 3 jest ładowana do ramki (błąd strony).
4. Odwołanie do strony **4** – Strona 1 (najdłużej w kolejce) jest usuwana, a strona 4 jest ładowana (błąd strony).
5. Odwołanie do strony **1** – Strona 2 (najdłużej w kolejce) jest usuwana, strona 1 jest ładowana (błąd strony).
6. Odwołanie do strony **2** – Strona 3 (najdłużej w kolejce) jest usuwana, strona 2 jest ładowana (błąd strony).

**Stan ramek po każdej operacji**:

| Odwołanie | Stan ramek | Błąd strony? |
| --------- | ---------- | ------------ |
| 1         | 1          | Tak          |
| 2         | 1, 2       | Tak          |
| 3         | 1, 2, 3    | Tak          |
| 4         | 4, 2, 3    | Tak          |
| 1         | 4, 1, 3    | Tak          |
| 2         | 4, 1, 2    | Tak          |
| 5         | 5, 1, 2    | Tak          |

#### **2. [LRU (Least Recently Used)**](https://www.youtube.com/watch?v=8Z9-BvSXq_Q)
- LRU zastępuje stronę, która była najmniej używana w przeszłości.
- Uwzględnia historię dostępu do stron.

**Przykład krok po kroku**:
1. Odwołanie do strony **1** – Strona 1 jest ładowana do ramki (błąd strony).
2. Odwołanie do strony **2** – Strona 2 jest ładowana do ramki (błąd strony).
3. Odwołanie do strony **3** – Strona 3 jest ładowana do ramki (błąd strony).
4. Odwołanie do strony **4** – Strona 1 (najmniej używana) jest zastępowana (błąd strony).
5. Odwołanie do strony **1** – Strona 2 (najmniej używana) jest zastępowana (błąd strony).
6. Odwołanie do strony **2** – Strona 3 (najmniej używana) jest zastępowana (błąd strony).

**Stan ramek po każdej operacji**:

| Odwołanie | Stan ramek | Błąd strony? |
| --------- | ---------- | ------------ |
| 1         | 1          | Tak          |
| 2         | 1, 2       | Tak          |
| 3         | 1, 2, 3    | Tak          |
| 4         | 4, 2, 3    | Tak          |
| 1         | 4, 1, 3    | Tak          |
| 2         | 4, 1, 2    | Tak          |
#### **3. [Algorytm Clock (Second Chance)](https://www.youtube.com/watch?v=C26qsPwf-Js)**
- Clock to ulepszony FIFO z dodatkowym bitem użycia. Strony z ustawionym bitem użycia nie są usuwane – zamiast tego ich bit jest zerowany.

**Przykład krok po kroku**:
1. Odwołanie do strony **1** – Strona 1 jest ładowana do ramki (błąd strony, bit=1).
2. Odwołanie do strony **2** – Strona 2 jest ładowana do ramki (błąd strony, bit=1).
3. Odwołanie do strony **3** – Strona 3 jest ładowana do ramki (błąd strony, bit=1).
4. Odwołanie do strony **4** – Strona 1 ma bit=1, więc bit jest zerowany, ale pozostaje w pamięci; każda strona jest ustawiana na 0 i następuje powrót do strony 1 i podmienienie jej.
5. Odwołanie do strony **1** – Strona 2 ma bit=1, więc bit jest zerowany; strona 3 zostaje zastąpiona (błąd strony).

**Stan ramek po każdej operacji**:

| Odwołanie | Stan ramek | Bit użycia | Błąd strony? |
| --------- | ---------- | ---------- | ------------ |
| 1         | 1          | 1          | Tak          |
| 2         | 1, 2       | 1, 1       | Tak          |
| 3         | 1, 2, 3    | 1, 1, 1    | Tak          |
| 4         | 4, 2, 3    | 1, 0, 0    | Tak          |
| 1         | 4, 1, 3    | 1, 1, 0    | Tak          |
| 3         | 4,1,3      | 1,1,1      | Nie          |
