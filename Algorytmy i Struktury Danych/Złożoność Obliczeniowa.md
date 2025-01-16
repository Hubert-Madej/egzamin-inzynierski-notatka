Dziedzina informatyki i matematyki, która bada efektywność algorytmów, mierząc, ile zasobów (czasowych i pamięciowych) jest potrzebnych do rozwiązania danego problemu. Określa, jak szybko rośnie ilość wymaganych operacji lub pamięci w zależności od wielkości danych wejściowych.

Możemy wyróżnić dwa rodzaje złożoności: czasową i pamięciową. Złożoność czasowa określa jak długo działa algorytm w zależności od rozmiaru danych wejściowych, mierzy to na podstawie liczby podstawowych operacji (np. porównań, dodawań) wykonywanych przez algorytm. Pamięciowa natomiast określa ile pamięci jest potrzebne do wykonania algorytmu, uwzględnia ona dodatkowe struktury danych i zmienne pomocnicze używane podczas obliczeń.

### Notacja Asymptotyczna
Do wyrażenia złożoności algorytmów używa się notacji asymptotycznej, która opisuje jak zachowuje się algorytm dla dużych danych wejściowych ($n \to \infty$):
- O-Wielkie (Big-O) - O(n): Opisuje górne ograniczenie złożoności i określa najgorszy możliwy przypadek działania algorytmu.
-  Ω-Wielkie (Big-Omega) - Ω(n): Opisuje dolne ograniczenie złożoności i określa najlepszy możliwy przypadek działania algorytmu.
-  Θ-Wielkie (Big-Theta) - Θ(n): Opisuje dokładną złożoności algorytmu, określając, że algorytm zawsze działa w czasie proporcjonalnym do $n$.

### **Przykłady złożoności czasowej**
- **O(1)** – Stała złożoność: czas wykonania nie zależy od wielkości danych.  
    _Przykład:_ Dostęp do elementu tablicy po indeksie.
- **O(log n)** – Logarytmiczna złożoność: czas rośnie powoli wraz z rozmiarem danych.  
    _Przykład:_ Wyszukiwanie binarne.
- **O(n)** – Liniowa złożoność: czas rośnie proporcjonalnie do wielkości danych.  
    _Przykład:_ Przeszukiwanie listy.
- **O(n log n)** – Liniowo-logarytmiczna złożoność: typowa dla wydajnych algorytmów sortowania.  
    _Przykład:_ Sortowanie szybkie (**QuickSort**), sortowanie przez scalanie (**MergeSort**).
- **O(n²)** – Kwadratowa złożoność: czas rośnie kwadratowo wraz z rozmiarem danych.  
    _Przykład:_ Proste algorytmy sortowania, jak sortowanie bąbelkowe (**Bubble Sort**).
- **O(2ⁿ)** – Wykładnicza złożoność: czas rośnie bardzo szybko.  
    _Przykład:_ Rozwiązywanie problemu komiwojażera metodą brute-force.

### **Znaczenie złożoności obliczeniowej**
1. **Wydajność algorytmów:**  
    Złożoność obliczeniowa pozwala porównać, które algorytmy są bardziej efektywne dla dużych danych.
2. **Dobór algorytmu:**  
    Znając złożoność, można dobrać algorytm odpowiedni do danego problemu i dostępnych zasobów.
3. **Ocena skalowalności:**  
    Pomaga ocenić, jak algorytm będzie się zachowywał przy rosnących danych wejściowych.

![[Pasted image 20250111171410.png]]

```python
def example_algorithm(n):
    total = 0                      
    for i in range(n):             
        for j in range(n):         
            total += i + j         
    return total                   
```

Krok 1: Przypisanie wartości do zmiennej `total` jest wykonywane tylko raz, na początku wywołania algorytmu. Złożoność tego kroku wynosi $O(1)$.

Krok 2: Wykonanie pętli `for` $n$ razy. Złożoność kroku $O(n)$.

Krok 3: Wykonanie pętli `for` $n$ razy, dla każdej iteracji pętli zewnętrznej. Złożoność kroku $O(n*n) = O(n^2)$.

Krok 4: Zwiększenie wartości `total`, o sumę wartości zmiennych `i` i `j`. 
Złożoność kroku: $O(1)$.

Krok 5: Zwrócenie wartości `total`. Złożoność kroku: $O(1)$.

Całkowita Złożoność Algorytmu (Wynikiem jest dominujący składnik, czyli ten o największej złożoności): $O(1) + O(n) + O(n^2) + O(1) + O(1) = O(n^2)$
