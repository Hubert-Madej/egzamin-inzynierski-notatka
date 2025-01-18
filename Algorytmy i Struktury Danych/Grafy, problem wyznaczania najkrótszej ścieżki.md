Graf to abstrakcyjna struktura danych używana do modelowania relacji między obiektami. Jest zbiorem wierzchołków (punktów, ang. vertices lub nodes) oraz krawędzi (połączeń, ang. edges), które łączą pary wierzchołków. Istnieje możliwość, że wierzchołki grafu nie są połączone żadną krawędzią i taki graf nadal jest prawidłowy. Nazywamy go grafem pustym (ang. NULL Graph). Liczba krawędzi ($E$), dla liczby wierzchołków ($V$) będzie zawsze mniejsza lub równa $V^2$ 
($E \leq V^2$). To dlatego, że każdy węzeł może co najwyżej wskazywać sam siebie i każdy inny węzeł w grafie.

Graf $G$ można zdefiniować jako parę uporządkowaną:
$$
G = (V,E)
$$
gdzie:
- $V$ - zbiór wierzchołków (np. $V = \{A, B, C, D\}$)
- E - zbiór krawędzi, czyli par wierzchołków (np. $E=\{(A,B), (B,C), (C,D)\}$)

**Rodzaje Grafów:**
1. **Graf nieskierowany** - w tym rodzaju grafu krawędzie nie mają kierunku. Połączenia takie jak $(A,B)$ i $(B, A)$ są sobie równoważne. Przykładem takiego grafu może być sieć ulic dwukierunkowych.
   
   ![[undirected-graph.jpg]]
   
2. **Graf skierowany** - w tym rodzaju grafu krawędzie mają kierunek. Połączenie $(A, B)$ oznacza drogę z $A$ do $B$. Połączenie $(B,A)$ jest zupełnie innym połączeniem tych dwóch punktów. Przykładem takiego grafu może być sieć ulic jednokierunkowych
   
   ![[directed-graph.jpg]]

3. **Graf ważony** - krawędź ma przypisaną wagę (ang. weight), która może oznaczać odległość, koszt, czas, itp. Przykładem takiego grafu może być mapa miast z odległościami.
   
   ![[weighted-graph.jpg]]
   
4. **Graf prosty** - nie zawiera pętli (krawędzi prowadzącej z wierzchołka do samego siebie), ani wielokrotnych krawędzi między tą samą parą wierzchołków.
 ![[simple-graph.jpg]]
 
5. **Graf pełny** - każdy wierzchołek jest połączony z każdym innym. Liczba krawędzi w tym przypadku wynosi: $\frac{n(n-1)}{2}$.


**Sposoby reprezentacji grafów:**
1. Macierz sąsiedztwa - tablica $n \times n$, gdzie $n$ to liczba wierzchołków. Dla standardowego grafu jeśli istnieje krawędź między $i$ i $j$, to umieszczamy $1$ w tablicy w tej pozycji 
   ($A[i][j] = 1$). W przypadku grafu ważonego zamiast $1$ umieszczamy wartość wagi. Zaletą takiej reprezentacji jest szybki dostęp do informacji, natomiast wadą jest ilość pamięci potrzebna dla rzadkich grafów.

2. Lista sąsiedztwa - dla każdego wierzchołka przechowujemy listę jego sąsiadów. Jest to efektywna metoda dla grafów rzadkich, natomiast sprawdzanie połączenia jest wolniejsze.
   
**Przykład dla grafu nieskierowanego:**
$V = \{A,B,C,D\}$
$E = \{(A,B), (A,C), (B,D)\}$
   
**Lista sąsiedztwa:**
$A: B, C$
$B: A, D$
$C: A$
$D: B$

**Macierz sąsiedztwa:**

$\begin{aligned} \begin{array}{c|cccc} & A & B & C & D \\ \hline A & 0 & 1 & 1 & 0 \\ B & 1 & 0 & 0 & 1 \\ C & 1 & 0 & 0 & 0 \\ D & 0 & 1 & 0 & 0 \\ \end{array} \end{aligned}$


### Problem wyznaczania najkrótszej ścieżki w grafie

##### Wprowadzenie

Problem polega na znalezieniu ścieżki między dwoma wierzchołkami w grafie, która minimalizuje sumę wag krawędzi. Problem ten jest kluczowy w wielu dziedzinach takich jak:
- Systemy GPS
- Sieci Komputerowe
- Logistyka

**Rodzaje problemów najkrótszej ścieżki:**
- Najkrótsza ścieżka z jednego wierzchołka do wszystkich innych - np. z miasta A do wszystkich pozostałych.
- Najkrótsza ścieżka między zadaną parą wierzchołków - np. z miasta A do miasta B.
- Najkrótsza ścieżka między wszystkimi parami wierzchołków - optymalizacja globalna.

**Relaksacja:**
W algorytmach wyszukiwania najkrótszej ścieżki, relaksacja to proces sprawdzania, czy przejście przez dany wierzchołek prowadzi do krótszej ścieżki do innego wierzchołka. Jeśli tak, to aktualizujemy odległość do tego wierzchołka:
$$
if \ distance[u] + w(u,v) < distance[v], \ to \ distance[v] = distance[u] + w(u,v)
$$
gdzie:
- $u$ - obecnie przetwarzany wierzchołek
- $v$ - sąsiad wierzchołka $u$
- $w(u,v)$- waga krawędzi między $u$ i $v$
- $distance[v]$ - aktualna najkrótsza znana odległość do $v$
##### Główne Algorytmy

###### Algorytm Dijkstry

Algorytm służący do znajdowania najkrótszej ścieżki z jednego wierzchołka do wszystkich innych w grafie, o nieujemnych wagach krawędzi. Nie ujemność wag jest kluczowa, ponieważ algorytm opiera się na sumowaniu wag (które możemy traktować jako dystanse), co w przypadku wag ujemnych mogło by prowadzić do obliczenia nieprawidłowych tras.

Jak dane wejściowe, algorytm przyjmuje definicję grafu, oraz wierzchołek startowy, dla którego chcemy znaleźć wszystkie najkrótsze trasy. W początkowym etapie algorytmu deklarujemy tablicę dystansów, która będzie nas informowała, o najkrótszym dystansie z wierzchołka startowego, do każdego innego wierzchołka w grafie.

Zdefiniujmy przykładowy graf nieskierowany:

$$
\begin{array}{c|ccccccc}
  & 0 & 1 & 2 & 3 & 4 & 5 & 6 \\
\hline
0 & 0 & 2 & 6 & 0 & 0 & 0 & 0 \\
1 & 2 & 0 & 0 & 5 & 0 & 0 & 0 \\
2 & 6 & 0 & 0 & 8 & 0 & 0 & 0 \\
3 & 0 & 5 & 8 & 0 & 10 & 15 & 0 \\
4 & 0 & 0 & 0 & 10 & 0 & 6 & 2 \\
5 & 0 & 0 & 0 & 15 & 6 & 0 & 6 \\
6 & 0 & 0 & 0 & 0 & 2 & 6 & 0 \\
\end{array}
$$

Pierwszy wiersz i kolumna stanowią "labelki" węzłów w grafie. 

**Graficzna reprezentacja grafu:**

![[graph.jpg]]

Początkowo wszystkie dystanse (oprócz wierzchołka startowego, którego dystans wynosi $0$) są ustawione na $\infty$, ponieważ są nieznane. Lista odwiedzonych wierzchołków jest pusta. Kolejkę priorytetową wierzchołków do przetworzenia inicjalizujemy parą $(0,Startowy \ Wierzchołek)$ — gdzie pierwszy element oznacza dystans od wierzchołka startowego, a drugi to sam wierzchołek. Następnie, dopóki kolejka nie jest pusta, wykonujemy następujące kroki:
1. Pobieramy wierzchołek o **najmniejszym** dystansie z kolejki.
2. Dla każdego sąsiada tego wierzchołka obliczamy sumę dotychczasowego dystansu i wagi krawędzi prowadzącej do sąsiada.
3. Jeżeli nowy dystans jest **mniejszy** od aktualnie zapisanego dystansu do tego sąsiada, aktualizujemy tę wartość w tablicy dystansów.
4. Dodajemy sąsiada do kolejki przetwarzania.
Po zakończeniu algorytmu tablica dystansów zawiera najkrótsze ścieżki z wierzchołka startowego do wszystkich innych wierzchołków w grafie.

**Przykładowa Implementacja:**
Złożoność Czasowa: $O((V+E) \cdot \log V)$
Złożoność Pamięciowa: $O(V + E)$

```python
import heapq

def dijkstra(graph, source_node):
    distances = { node: float('inf') for node in graph.keys() }
    distances[source_node] = 0

    # (Node, Current distance to node from source)
    nodes_to_process =[(0, source_node)] 
    heapq.heapify(nodes_to_process)
    visited = set()

    while nodes_to_process:
        current_distance, node = heapq.heappop(nodes_to_process)
        
        if node in visited:
            continue

        visited.add(node)

        for adjecent_node, distance in graph[node]:
            if adjecent_node not in visited:
               new_distance = current_distance + distance
               if new_distance < distances[adjecent_node]:
                   distances[adjecent_node] = new_distance
                   heapq.heappush(nodes_to_process,(new_distance, adjecent_node))
       
    
    # Distances now includes shortest path to each node, from source node.
    return distances    

# <Node>: [(NeighborNode, Distance)]
graph = {
    "0": [("1", 2), ("2", 6)],
    "1": [("0", 2), ("3", 5)],
    "2": [("0", 6), ("3", 8)],
    "3": [("1", 5), ("2", 8), ("4", 10), ("5", 15)],
    "4": [("3", 10), ("5", 6), ("6", 2)],
    "5": [("3", 15), ("4", 6), ("6", 6)],
    "6": [("4", 2), ("5", 6)]
}    

distances = dijkstra(graph, "0")
```
###### Algorytm Bellmana-Forda

Algorytm Bellmana-Forda jest algorytmem służącym do znajdowania najkrótszej ścieżki z jednego wierzchołka do wszystkich innych w grafie, który może zawierać zarówno dodatnie, jak i ujemne wagi krawędzi. Jego kluczową cechą jest zdolność do wykrywania cykli o ujemnej wadze, co czyni go bardziej uniwersalnym niż algorytm Dijkstry, który nie radzi sobie z ujemnymi wagami.

Skorzystamy z tego samego grafu, co dla poprzedniego algorytmu. Początkowo wszystkie dystanse (oprócz wierzchołka startowego, którego dystans wynosi $0$) są ustawione na $\infty$, ponieważ są nieznane. Lista odwiedzonych wierzchołków jest pusta. Następnie algorytm wykonuje następujące kroki przez dokładnie $V - 1$ iteracji, gdzie $V$ to liczba wierzchołków w grafie:
1. Dla każdej krawędzi $(u, v)$ z wagą $w$, sprawdzamy, czy dystans do $v$ można zmniejszyć przechodząc przez $u$. Jeśli tak, aktualizujemy dystans:
2. Po wykonaniu $V - 1$ iteracji sprawdzamy, czy istnieje cykl o ujemnej wadze. Jeśli dla którejkolwiek krawędzi $(u, v)$ relaksacja jest nadal możliwa, oznacza to istnienie cyklu o ujemnej wadze, a algorytm zgłasza ten fakt.
Po zakończeniu algorytmu tablica dystansów zawiera najkrótsze ścieżki z wierzchołka startowego do wszystkich innych wierzchołków w grafie. Jeśli wykryto cykl o ujemnej wadze, algorytm zgłasza jego obecność, co pozwala uniknąć błędnych obliczeń najkrótszych ścieżek.

**Przykładowa Implementacja:**
Złożoność Czasowa: $O((V+E) \cdot \log V)$
Złożoność Pamięciowa: $O(V + E)$

```python
def bellman_ford(graph, source_node):
    distances = { node: float('inf') for node in graph.keys() }
    distances[source_node] = 0

    n = len(graph)
    for _ in range(n - 1):
        for u in graph.keys():
            for v, distance in graph[u]:
                # Relaxation
                new_distance = distances[u] + distance
                if new_distance < distances[v]:
                    distances[v] = new_distance


    # Check for negative cycle
    for u in graph.keys():
        for v, distance in graph[u]:
            new_distance = distances[u] + distance
            if new_distance < distances[v]:
                return None

    return distances


# <Node>: [(NeighborNode, Distance)]
graph = {
    "0": [("1", 2), ("2", 6)],
    "1": [("0", 2), ("3", 5)],
    "2": [("0", 6), ("3", 8)],
    "3": [("1", 5), ("2", 8), ("4", 10), ("5", 15)],
    "4": [("3", 10), ("5", 6), ("6", 2)],
    "5": [("3", 15), ("4", 6), ("6", 6), ("4", -20)], # -20 causes negative cycle here.
    "6": [("4", 2), ("5", 6)]
}

distances = bellman_ford(graph, "0")
```
###### Algorytm Floyda-Warshalla