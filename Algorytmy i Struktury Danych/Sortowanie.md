Sortowanie jest kluczowym zagadnieniem w algorytmice i informatyce. Polega ono na uporządkowaniu elementów w określonej kolejności, najczęściej rosnącej lub malejącej. Jest to fundament dla wielu bardziej złożonych algorytmów i operacji na danych. Wyróżniamy wiele algorytmów sortowania, z których każdy ma swoje zalety i wady pod względem złożoności czasowej i pamięciowej.

### Sortowanie przez wstawianie (Insertion Sort)

To jeden z najprostszych algorytmów sortowania. Działa podobnie do sortowania kart w ręce - każdą kolejną kartę (element) wstawiamy w odpowiednie miejsce w już posortowanej tablicy.

**Algorytm:**
- Wyznacz wolny wskaźnik $i$ (wartość z przedziału $<1;n)$, gdzie $n$ to długość tablicy).
- Zapamiętaj $k$, jako wartość tablicy pod wolnym wskaźnikiem ($i$).
- Wyznacz szybki wskaźnik $j$, jako $i-1$.
- Dopóki $j >= 0$ oraz $tablica[j] > k$ $->$ przesuń wartość spod $j$ na pozycje $j+1$.
- Jeśli pętla przerwana $->$ cofnij wolny wskaźnik w prawo o jedną pozycję ($j+1$) i ustaw wartość tablicy na $k$ ($tablica[j] = k$).

![[insertion_sort.jpg]]

Złożoność czasowa:
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