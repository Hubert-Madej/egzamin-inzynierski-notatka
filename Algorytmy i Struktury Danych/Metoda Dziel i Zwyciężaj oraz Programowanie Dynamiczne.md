### Metoda Dziel i Zwyciężaj

Jedna z głównych metod projektowania algorytmów w informatyce, prowadząca do bardzo efektywnych rozwiązań. Metoda ta, polega na rekurencyjnym podziale problemu, na dwu lub więcej mniejszych pod-problemów, tak długo aż fragmenty staną się wystarczające do samodzielnego rozwiązania problemu. Następnie otrzymane rozwiązania pod-problemów są scalane, uzyskując rozwiązanie całego zadania.

**Przykłady algorytmów opartych na tej metodzie:**
- Sortowanie przez scalanie (Merge Sort)
- Sortowanie szybkie (Quick Sort)
- Wyszukiwanie Binarne (Binary Search)

Projektowanie efektywnych algorytmów metodą dziel i zwyciężaj może być skomplikowane, podobnie jak dowodzenie indukcyjne. Często konieczne jest uogólnienie problemu, aby dostosować go do rekurencyjnego rozwiązania. Poprawność algorytmów opartych na metodzie Dziel i Zwyciężaj dowodzi się poprzez indukcje matematyczną, a złożoność obliczeniową poprzez rozwiązanie [rekurencyjnych relacji](https://en.wikipedia.org/wiki/Recurrence_relation) i [teorię mistrza](https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms).

**Zalety metody dziel i zwyciężaj:**
- Ułatwianie rozwiązywania skomplikowanych problemów - wymaga jedynie znalezienia sposobu na rozbicie problemu na mniejsze pod-problemy.
- Pomaga w znalezieniu optymalnych rozwiązań - dzięki zastosowaniu tej metody algorytmy takie jak Quick Sort, Merge Sort, Algorytm Strassena (mnożenie macierzy) pozwoliły polepszyć złożoność asymptotyczną rozwiązań danego problemu.
- Równoległość - dzięki zastosowaniu podziału na mniejsze izolowane od siebie pod-problemy, możemy dokonywać ich obliczeń równolegle, dbając przy tym o właściwe złączenie wyników.

**Problemy Implementacyjne:**
Jak wcześniej wspomniano, Dziel i Zwyciężaj opiera się na rekurencji. Może również opierać się na nie rekurencyjnych rozwiązaniach opartych na jawnym stosie, kolejce, lub kolejce priorytetowej. Takie rozwiązanie pozwala na większą elastyczność , które pod-problem ma zostać rozwiązany jak następny.

W przypadku korzystania z podejścia rekurencyjnego, odpowiednia ilość pamięci musi zostać zaalokowana na stos rekurencyjny, w przeciwnym wypadku wykonanie programu może zakończyć się błędem (StackOverflow). Wydajne czasowo algorytmy D&Z często mają niewielką głębokość rekurencji. Przykładowo algorytm sortowania szybkiego (quick sort) może zostać zaimplementowany w taki sposób, że nigdy nie będzie potrzeba więcej niż $\log_{2}{n}$ zagnieżdżonych wywołań rekurencyjnych do posortowania $n$ elementów. Uniknięci przepełnienia stosu, może nie być takie proste, ze względu na to, że wiele kompilatorów zakłada, że stos rekurencyjny jest ciągła przestrzenią adresową i z tego względu alokują stałą przestrzeń w pamięci. Kompilator może również przechowywać na stosie rekurencyjnym więcej informacji, niż to faktycznie potrzebne (np. niezmienne parametry, wartości zmiennych lokalnych procedury). Zatem ryzyko przepełnienia stosu może zostać zminimalizowane przez zmniejszenie ilości parametrów i zmiennych lokalnych procedur, lub poprzez użycie jawnego stosu.

**Wybór przypadku bazowego**
W jakimkolwiek rekurencyjnym algorytmie, istnieje znaczna swoboda wyboru podstawowym przypadków, które rozwiązywane są bezpośrednio w celu zakończenia rekurencji.

Pierwszym ze sposób jest wybór najmniejszego (lub najprostszego przypadku), ze względu na prostotę i estetykę program, ponieważ jest mniej warunków do rozpatrzenia. Przykładowo, algorytm sortowania szybkiego kończy swoje działanie, jeśli trzyma jako wartość argumentu pustą listę. Mamy tu jest prosty base-case i nie wymaga, on żadnego przetwarzania.

Drugim sposobem, jest rozszerzenie przypadku bazowego. Polega to na zwiększeniu wydajności algorytmu, poprzez zwiększenie zakresu, który uważany jest za wystarczająco prosty pod-problem i rozwiązanie go w nie-rekurencyjny sposób, tworząc przy tym rozwiązanie hybrydowe. Takie podejście pozwala uniknąć narzutu związanego z rekurencyjnymi wywołaniami, które wykonują bardzo małą ilość pracy, lub tej pracy nie wykonują wcale. Ogólnym podejściem tego typu jest prosty algorytm hybrydowy, który pozwala na zwarcie przypadków bazowych ([Arm's-length Recursion](https://en.wikipedia.org/wiki/Arm%27s-length_recursion)). W takim przypadku, sprawdzamy, czy następne wywołanie funkcji, spowoduje wywołanie przypadku bazowego, zamiast wykrywać to bezpośrednio na początku. Dzięki temu, unikamy niepotrzebnego wywołania funkcji. Przykładowo, w strukturze drzewiastej, zamiast wywoływać funkcje dla węzła dziecka i sprawdzać, czy jest NULLem, wykonujemy to przez wywołaniem i ew. przerywamy działanie w tym samym wywołaniu. Niektóre biblioteki implementując szybkie sortowanie, przełączają się na proste oparte na pętli sortowanie przez wstawianie, jak tylko liczba elementów do posortowania będzie wystarczająco mała. Dodatkowo, jeśli zastosujemy poszerzony przypadek bazowy, unikniemy niepotrzebny wywołań samych bazowych. Możemy stosować również **unrolling**, czyli zamiast wykonywać rekurencje dla określonych przypadków bazowych, wykonujemy bezpośrednie obliczenia w zadanym kontekście, lub korzystam z pre-definiowanych wartości.

Dla niektórych problemów, rekurencja, może obliczać ten sam pod-problem wiele razy. Warto zidentyfikować takie przypadki i zachowywać rozwiązanie takich pod-problemów do ponownego użycia (Memoizacja). W skrajnych przypadkach prowadzi to do Programowania dynamicznego.

**Przykład Algorytmu - Merge Sort:**

```python
def merge(arr, s, m, e):
	left = arr[s:m+1]
	right = arr[m+1:e+1]

	i = j = 0
	k = s

	while i < len(left) and j < len(right):
		if left[i] <= right[j]:
			arr[k] = left[i]
			i += 1
		else:
			arr[k] = right[j]
			j += 1
		k += 1

	while i < len(left):
		arr[k] = left[i]
		i += 1
		k += 1

	while j < len(right):
		arr[k] = right[j]
		j += 1
		k += 1


def merge_sort(arr, s, e):
	if e - s + 1 <= 1:
		return arr

	m = (s + e) // 2
	merge_sort(arr, s, m)
	merge_sort(arr, m+1, e)
	merge(arr, s, m, e)

	return arr

arr = [5,2,9,0,1,3,8,6,5,2]
s = 0
e = len(arr) - 1
merge_sort(arr, s, e)
```

```python
def get_partition_index(arr, s, e):
	target_index = e
	target = arr[e]
	slow_ptr = s - 1

	for fast_ptr in range(s, e):
		if arr[fast_ptr] <= target:
			slow_ptr += 1
			(arr[fast_ptr], arr[slow_ptr]) = (arr[slow_ptr], arr[fast_ptr])

	slow_ptr += 1
	(arr[slow_ptr], arr[target_index]) = (arr[target_index], arr[slow_ptr])

	return slow_ptr

def quick_sort(arr, s, e):
	if e - s + 1 <= 1:
		return arr
	
	pi = get_partition_index(arr, s, e)
	quick_sort(arr, s, pi - 1)
	quick_sort(arr, pi + 1, e)

arr = [5,2,9,0,1,3,8,6,5,2]
s = 0
e = len(arr) - 1
quick_sort(arr, s, e)
```

### Programowanie Dynamiczne
Programowanie dynamiczne to technika projektowania algorytmów, która polega na rozkładaniu problemu na mniejsze podproblemy i przechowywaniu wyników rozwiązań tych podproblemów. Dzięki temu unikamy ponownego obliczania tych samych podproblemów, co prowadzi do optymalizacji czasu obliczeń. Technika ta jest szczególnie przydatna w przypadkach, gdy podproblemy nakładają się (tzn. są powtarzane w różnych częściach algorytmu) lub kiedy problem ma strukturę optymalnościową, czyli jego rozwiązanie opiera się na rozwiązaniach jego podproblemów.

Kluczowe cechy programowania dynamicznego:
1. Optymalna podstruktura (Optimal Substructure) - Problem można rozwiązać poprzez rozwiązanie jego podproblemów. Oznacza to, że optymalne rozwiązanie większego problemu składa się z optymalnych rozwiązań jego mniejszych cześci.
2. Nakładające się podproblemy (Overlapping Subproblems) - Ten sam pod-problem jest rozwiązywany wielokrotnie. Programowanie dynamiczne zapamiętuje wyniki wcześniej rozwiązanych podproblemów, aby uniknąć ich ponownego rozwiązaywania.
3. Memoizacja i Tabulacja:
	- Memoizacja (Memoization) - Podejście "top-down" polegające na zapamiętywaniu wyników podproblemów podczas ich obliczania (rekurencja + cache).
	- Tabulacja (Tabulation) - Podejście "bottom-up" polegające na wypełnieniu tabeli wynikami podproblemów, zaczynając od najprostszych.

**Przykład klasyczny - Ciąg Fibonacciego**

Ciąg Fibonacciego definiujemy, jako:
$$
F(n) = F(n-1) + F(n-2)
$$
dla $n$ > 1, z wartościami początkowymi $F(0) = 0$ i $F(1) = 1$.

Najprostszym podejściem do obliczenia $n-tego$ składnika ciągu jest zastosowanie rekurencji:
```python
def fib(n):
	if n <= 1:
		return n
	return fib(n-1) + fib(n-2)
```

Jest to rozwiązanie nieoptymalne, ze złożonością czasową $O(2^n)$.

Można je zoptymalizować korzystając z podejścia "top-down" i zastosować memoizację:
```python
def fib(n, memo={}):
	if n in memo:
		return memo[n]
	if n <= 1:
		return n 

	memo[n] = fib(n-1, memo) + fib(n-2, memo)

	return memo[n]
```

W tym momencie uzyskujemy złożoność $O(n)$, przy czym czas dostępu do `memo` jest stały.
Można również zrezygnować z rekurencji i przejść na podejście "bottom-up" z wykorzystaniem tabeli i pętli:

```python
def fib(n):
	if n <= 1:
		return n

	dp = [0,1]
	for i in range(2, n):
		dp.append(dp[i-1] + dp[i-2])

	return dp[n]
```

Złożoność to ponownie $O(n)$, pamięciowa to również $O(n)$, jednak istnieje możliwość optymalizacji złożoności pamięciowej do $O(1)$, poprzez przejście na dwie zmienne i śledzenie tylko wartości $n-1$ i $n-2$ (bo tak naprawdę tylko one są potrzebne do uzyskania kolejnych rozwiązań dla $n$):

```python
def fib(n):
	if n <= 1:
		return n

	a, b = 0, 1 # fib(0), fib(1)
	for i in range(2, n+1):
		a, b = b, a + b

	return b
```

