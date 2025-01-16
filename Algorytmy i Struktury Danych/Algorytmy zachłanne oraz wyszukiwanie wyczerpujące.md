### Heurystyka
Metoda rozwiązywania problemów, która polega na stosowaniu praktycznych i intuicyjnych reguł (uproszczonych zasad), pozwalających znaleźć wystarczająco dobre rozwiązanie w rozsądnym czasie, zamiast dążyć do rozwiązania idealnego, które mogłoby wymagać ogromnych zasobów obliczeniowych.

**Cechy Heurystyki:**
- Nie gwarantuje optymalności - heurystyka może nie znaleźć najlepszego rozwiązania, ale często dostarcza rozwiązanie "wystarczająco dobre".
- Szybkość Działania - heurystyki działają znacznie szybciej niż algorytmy dokładne co jest kluczowe w złożonych problemach.
- Prostota i Intuicyjność - opierają się na prostych zasadach lub doświadczeniu, co sprawia, że są łatwe do wdrożenia.
- Przybliżenie do rozwiązania - często dostarczają rozwiązanie bliskie optymalnemu, co w praktyce bywa wystarczające.

**Dlaczego stosujemy Heurystyki?** Między innymi dla problemów NP-trudnych (np. komiwojażera, problem plecakowy), gdzie algorytmy dokładne mają zbyt dużą złożoność obliczeniową. Ponadto mogą zdarzyć się sytuacje, w których często ważniejszy jest szybki wynik niż idealne rozwiązanie. Czasami też możemy mieć niepełną informację wejściową, heurystyki mogą pomóc podejmować decyzje.

**Rodzaje Heurystyk:**
- Proste - bazują na intuicji i prostych regułach.
- Algorytmy Zachłanne - Wybierają najlepszą lokalnie opcję.
- Meta-heurystyki - Bardziej zaawansowane techniki, które łączą różne strategie poszukiwań

**Przykłady Heurystyki:**
- Problem plecakowy - Wybieraj przedmioty o najwyższym stosunku wartości do wagi, aż plecak się nie zapełni.
- Problem komiwojażera - Odwiedzaj najbliższe nieodwiedzone miasto. Szybka ścieżka, ale może nie być najkrótsza.

### Algorytmy Zachłanne
Strategia rozwiązywania problemów, która polega na podejmowaniu lokalnie optymalnych decyzji na każdym kroku, mając nadzieję, że doprowadzi to do globalnie optymalnego rozwiązania. W wielu przypadkach algorytmy zachłanne nie prowadzą do uzyskania optymalnych rozwiązań, ale zachłanna heurystyka może w rozsądnym czasie dostarczyć lokalnie optymalne rozwiązania, które są zbliżone do globalnie optymalnego rozwiązania.

Istnieją pewne własności problemów, które pozwalają nam stwierdzić czy warto w danym przypadku zastosować rozwiązanie zachłanne:
1. **Greedy Choice Property (Własność Zachłannego Wyboru):**
   W każdym kroku można dokonać wyboru, który wydaje się najlepszy lokalnie, a następnie rozwiązać pozostały pod-problem, bez konieczności cofania się i zmiany wcześniejszych decyzji. Jeśli problem spełnia tą własność, to lokalnie najlepszy wybór prowadzi do rozwiązania globalnie optymalnego. Dzięki temu algorytm zachłanny nie musi analizować całej przestrzeni rozwiązań, ani przewidywać konsekwencji swoich wyborów.
   
   **Przykład:**
	   - Minimalne Drzewo Rozpinające (MST): W algorytmie Kruskala, zawsze wybieramy krawędź o najmniejszej wadze, która nie tworzy cyklu. Ten wybór prowadzi do globalnie optymalnego drzewa.
	   - Algorytm Dijkstry: Zawsze wybieramy wierzchołek o najmniejszym koszcie, który nie został jeszcze odwiedzony.

2. **Optimal Substructure (Optymalna Podstruktura):**
   Problem posiada optymalną podstrukturę, jeśli optymalne rozwiązanie całego problemu zawiera rozwiązania jego pod-problemów. Jeśli rozwiązania pod-problemów są również optymalne, to algorytm zachłanny rozwiązując kolejne podproblemy, doprowadzi do globalnie najlepszego rozwiązania.
   
   **Przykład:**
	   - Algorytm Dijkstry: Najkrótsza ścieżka z A do B, musi zawierać najkrótszą ścieżkę z A do C, jeśli C leży na tej trasie.
	   - Problem wydawania reszty ([Dla wybranych nominałów](http://algorytmy.ency.pl/artykul/problem_wydawania_reszty)): Rozwiązanie dla kwoty $n$ składa się z optymalnego rozwiązania dla $n-k$, gdzie $k$ to nominał na wybranej monety.

Na podstawie powyższych cech algorytmów zachłannych, możemy zauważyć, dlaczego stosując algorytm zachłanny do problemu komiwojażera, lub plecakowego nie musimy uzyskać optymalnego rozwiązania.
### Wyszukiwanie Wyczerpujące
Metoda rozwiązywania problemów, która polega na sprawdzeniu wszystkich możliwych rozwiązań w celu znalezienia optymalnego. Jest to prosta, ale czasochłonna technika, która gwarantuje znalezienie najlepszego rozwiązania, jeśli takie istnieje. Dla problemów permutacji $n$ elementów złożoność wynosi $n!$, natomiast dla problemów podzbiorów $2^n$.

**Charakterystyka:**
- **Kompleksowość** - w tym podejściu przeszukiwane są wszystkie rozwiązania, bez pomijania jakiejkolwiek opcji.
- **Gwarancja Rozwiązania** - jeśli rozwiązanie istnieje, metoda je znajdzie.
- **Brak Optymalizacji** - nie stosuje heurystyk, ani sprytnych strategii skracających czas poszukiwań. 
- **Wysoka złożoność obliczeniowa** - może być bardzo czasochłonne i wymagać dużo pamięci, szczególnie dla dużych przestrzeni stanów.

**Przykłady Zastosowań:**
- Rozwiązywanie łamigłówek - np. znajdowanie rozwiązań kostki Rubika, przez sprawdzenie wszystkich możliwych sekwencji ruchów.
- Łamanie haseł - sprawdzanie wszystkich możliwych kombinacji znaków.
- Przeszukiwanie labiryntów.
- Szukanie podzbiorów - np. znajdowanie podzbiorów sumujących się do określonych wartości.

**Alternatywy dla wyszukiwania wyczerpującego:**
- **Algorytmy heurystyczne** (np. algorytmy zachłanne, algorytmy genetyczne)
- **Algorytmy optymalizacyjne** (np. programowanie dynamiczne, metoda podziału i ograniczeń)
- **Przeszukiwanie z przycinaniem** (np. _backtracking_, _branch and bound_)