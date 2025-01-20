Sortowanie jest kluczowym zagadnieniem w algorytmice i informatyce. Polega ono na uporządkowaniu elementów w określonej kolejności, najczęściej rosnącej lub malejącej. Jest to fundament dla wielu bardziej złożonych algorytmów i operacji na danych. Wyróżniamy wiele algorytmów sortowania, z których każdy ma swoje zalety i wady pod względem złożoności czasowej i pamięciowej.

### Sortowanie przez wstawianie (Insertion Sort)

To jeden z najprostszych algorytmów sortowania. Działa podobnie do sortowania kart w ręce - każdą kolejną kartę (element) wstawiamy w odpowiednie miejsce w już posortowanej tablicy.

**Algorytm:**
- Wyznacz wolny wskaźnik $i$ (wartość z przedziału $<1;n)$, gdzie $n$ to długość tablicy).
- Zapamiętaj $k$, jako wartość tablicy pod wolnym wskaźnikiem ($i$).
- Wyznacz szybki wskaźnik $j$, jako $i-1$.
- Dopóki $j >= 0$ oraz $tablica[j] > k$ $->$ przesuń wartość spod $j$ na pozycje $j+1$.
- Jeśli pętla przerwana $->$ cofnij wolny wskaźnik w prawo o jedną pozycję ($j+1$) i ustaw wartość tablicy na $k$ ($tablica[j] = k$).

![[egzamin-inzynierski-notatka/Algorytmy i Struktury Danych/attachments/insertion_sort.jpg]]

**Złożoność czasowa:**
- Najlepszy przypadek: $O(n)$ (dla posortowanej tablicy).
- Średni i najgorszy przypadek: $O(n^2)$.

Złożoność pamięciowa: Sortowanie odbywa się w miejscu i nie deklarujemy dodatkowej struktury w pamięci, zatem $O(1)$.

Algorytm ten jest prosty w implementacji i działaniu, i jest wystarczający dla małych zbiorów. Jednak wraz ze wzrostem liczby elementów w zbiorze, następuje wykładniczy wzrost złożoności czasowej algorytmu.

**Kod w Pythonie:**
```python
def insertion_sort(arr):
	size = len(arr)

	if size <= 1:
		return arr

	for i in range(1, size):
		k = arr[i]
		j = i - 1
		while j >= 1 and arr[j] > k:
			arr[j + 1] = arr[j]
			j -= 1
		arr[j + 1] = k
```

---
### Algorytm Shella (Shell Sort) - Sortowanie za pomocą malejących przyrostów

Ulepszona wersja sortowania przez wstawianie. Polega na porównywaniu elementów oddalonych od siebie o przyrost ($gap$) (np. połowa długości tablicy), który stopniowo maleje.

Algorytm:
- Wybierz początkowy przyrost $gap$.
- Posortuj elementy oddalone o $gap$ za pomocą sortowania przez wstawianie.
- Zmniejsz $gap$ i powtarzaj, dopóki $gap > 1$.

**Kod w Pythonie:**
```python
def shell_sort(arr):
    n = len(arr)
    gap = n // 2

    while gap > 0:
        for i in range(gap, n):
            temp = arr[i]
            j = i
            while j >= gap and arr[j - gap] > temp:
                arr[j] = arr[j - gap]
                j -= gap
            arr[j] = temp
        
        gap //= 2
```

**Złożoność czasowa:**
- Średnio: od $O(n^{3/2})$ do O($n\log ^2n$) w zależności od przyrostów.
- Najgorszy przypadek: $O(n^2)$.

Jest szybszy od tradycyjnego sortowania przez wstawianie, jednak należy zauważyć, że wybór przyrostów wpływa na wydajność.

---
### Sortowanie przez wybieranie (Selection Sort)

Algorytm polega na wielokrotnym znajdowaniu najmniejszego (lub największego) elementu i umieszczaniu go na właściwej pozycji.

Algorytm:
- Wyznacz wolny wskaźnik $i$ iterując się po wszystkich elementach tablicy.
- Wyznacz szybki wskaźnik $j$ iterując się po elementach między z przedziału $<i+1, n)$, gdzie $n$ to długość tablicy.
- Korzystając z szybkiego wskaźnika znajdź najmniejszy / największy element w zbiorze $<i+1, n)$ i zamień go z elementem wskazywanym przez wolny wskaźnik $j$.

![[egzamin-inzynierski-notatka/Algorytmy i Struktury Danych/attachments/selection_sort_min.jpg]]

Złożoność czasowa: $O(n^2)$ niezależnie od danych.
Złożoność pamięciowa: $O(1)$.

Zaletą algorytmu jest prosta implementacja, oraz minimalizowana jest liczba operacji zamieniania, natomiast ponownie mamy złożoność $O(n^2)$ co sprawia, że algorytm jest bardzo wolny dla dużych danych.

**Kod w Pythonie:**
```python
def selection_sort(arr):
    size = len(arr)
    
    if size <= 1:
        return arr
    
    for i in range(0, size):
        min_idx = i
        for j in range(i+1, size):
            if arr[j] < arr[min_idx]:
                min_idx = j
        
        (arr[min_idx], arr[i]) = (arr[i], arr[min_idx])
            
    return arr
```
### Sortowanie przez prostą zamianę (Bubble Sort)

Polega na wielokrotnym przechodzeniu przez tablicę i zamienianiu miejscami sąsiadujących elementów, jeśli są w złej kolejności.

**Algorytm:**
- Ustaw początkową wartość $n$, jako długość tablicy.
- Przejdź przez tablicę, porównując i zamieniając sąsiednie elementy, jeśli są w niewłaściwej kolejności (np. jeśli element na lewo jest większy od elementu na prawo). Po przejściu przez całą tablicę, największy element (dla porządkowania rosnącego) "bąbelkuje" na koniec tablicy.
- Po przejściu wszystkich elementów, zmniejsz $n$ o 1 ($n -= 1$).
- Powtarzaj kroki 2, aż $n$ będzie równe 1 (czyli gdy porównania obejmują tylko pierwszy element).

![[egzamin-inzynierski-notatka/Algorytmy i Struktury Danych/attachments/bubble-sort.jpg]]

**Kod w Pythonie:**
```python
def bubble_sort(arr):
    size = len(arr)
    
    if size <= 1:
        return arr
    
    # With each loop run, we will modify `n` value,
    # as with each run largest elment will bubble to the end.
    # Therfore, we can decrease sorting range after each run.
    n = size
    while n > 0:
        for i in range(1, n):
            if arr[i] < arr[i-1]:
                (arr[i], arr[i-1]) = (arr[i-1], arr[i])
        n -= 1
                
    return arr
```

Algorytm należy do najprostszych, natomiast jest bardzo nieefektywny dla dużych zbiorów.

### Sortowanie Szybkie (Quick Sort)

Quicksort to jeden z najszybszych algorytmów sortowania, oparty na metodzie „dziel i zwyciężaj”.

**Algorytm:**
1. Wybierz element pivot (punkt odniesienia).
2. Podziel tablicę na dwie części: mniejsze i większe od pivot.
3. Rekurencyjnie sortuj obie części.

![[egzamin-inzynierski-notatka/Algorytmy i Struktury Danych/attachments/quick-sort.jpg]]

**Złożoność czasowa:**
- Średnio: $O(n \ log \ n)$
- Najgorszy przypadek: $O(n^2)$ (gdy pivot jest źle wybierany)

Algorytm dzięki zastosowaniu metody dziel i zwyciężaj jest jednym z najszybszych algorytmów sortowania. Największym zagrożeniem, jest niewłaściwy wybór pivot'a. Często jako pivot stosuje się np. pierwszy / ostatni element. Aby uniknąć niewłaściwego pivot'a, można wybrać pivot losowo, lub zastosować algorytm z tzw. "medianą trzech". 

**Kod w Pythonie:**
```python
def partition(arr, s, e):
	pivot_idx = e
	pivot = arr[pivot_idx]
	i = s - 1

	for j in range(s, e):
		if arr[j] <= pivot:
			i += 1
			(arr[j], arr[i]) = (arr[i], arr[j])

	i += 1
	(arr[i], arr[pivot_idx]) = (arr[pivot_idx], arr[i])

	return i

def quick_sort(arr, s, e):
	if e - s + 1 <= 1:
		return arr

	pivot_idx = partition(arr, s, e)
	quick_sort(arr, s, pivot_idx - 1)
	quick_sort(arr, pivot_idx + 1, e)

	return arr
```

"Media z trzech" polega na wyborze pivota jako mediany z trzech elementów: pierwszego, środkowego i ostatniego. Taki wybór pivotu jest bardziej reprezentatywny dla danych, co poprawia efektywność sortowania.

```python
def median_of_three(arr, low, high):
    mid = (low + high) // 2
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    if (a - b) * (c - a) >= 0:
        return low
    elif (b - a) * (c - b) >= 0:
        return mid
    else:
        return high
```

Zarówno ta metoda, jak i losowy wybór pivota ***tylko minimalizuje szanse*** na najgorszy przypadek. Nadal jednak jest możliwość uzyskania najgorszej złożoności.