Algebra Układów Cyfrowych jest matematycznym fundamentem projektowania i analizy układów logicznych. Jest to dziedzina algebry, w której operacje i wyrażenia dotyczą zmiennych logicznych, przyjmujących wartości logiczne 0 (fałsz) lub 1 (prawda). Podstawowymi operacjami w algebrze boole'a są:

##### Negacja zmienia wartość zmiennej:

$$
\textbf{NOT (\( \neg \))}
$$

$$
\neg 0 = 1, \quad \neg 1 = 0
$$

##### Iloczyn logiczny (wynik to 1 tylko, gdy oba argumenty są 1).
$$
\textbf{AND (\( \land \))}
$$
$$
0 \land 0 = 0, \quad 1 \land 1 = 1
$$

##### Suma logiczna (wynik to 1, gdy przynajmniej jeden argument to 1).
$$
\textbf{OR (\( \lor \))}
$$
$$
0 \lor 0 = 0, \quad 1 \lor 1 = 1
$$

Algebra Bool'ea została opracowana przez George'a Boole'a w XIX wieku. Pierwotnym celem było stworzenie formalnego sposobu wyrażania procesów logicznych i operacji na zdaniach prawdziwych lub fałszywych. Celem algebry boole'a jest matematyczny opis logiki. Daje to możliwość modelowania problemów logicznych i rozwiązywania ich w sposób systematyczny i formalny. W połowie XX wieku algebra Boole'a stała się fundamentem analizy i projektowania układów cyfrowych gdy Calude Shannon wykazał, że można ją bezpośrednio zastosować do opisu przełączników elektrycznych.

Algebra Boole'a jest jednym z najważniejszych elementów dzisiejszej techniki cyfrowej. Dzięki niej, każdy układ można opisać, jako zbiór operacji logicznych. Dzięki niej projektanci mogą modelować, upraszczać i optymalizować systemy cyfrowe. Uproszczanie funkcji logicznych (np. za pomocą tablic Karnaugha) prowadzi do minimalizacji bramek logicznych, a tym samym do redukcji kosztów i zużycia energii.

Algebra Boole'a jest stosowana w technice cyfrowej, ze względu na bazowanie na prostych regułach, która łatwo można odwzorować w sprzęcie elektronicznym. Dodatkowo wcześniej wymienione operacje posiadają swój odpowiednik w postaci bramek logicznych. Ponadto, układ można zrealizować przy pomocy różnych technologii (elektronika, fotonika, nanotechnologia), natomiast algebra bool'ea nadal będzie obowiązywać.

---
### Prawa Algebry Boole'a

Algebra Boole’a, jako podstawowe narzędzie w teorii układów cyfrowych, opiera się na zestawie praw, które umożliwiają przekształcanie i upraszczanie funkcji logicznych. Prawa te znajdują zastosowanie w projektowaniu i minimalizacji układów logicznych, optymalizując liczbę bramek logicznych oraz redukując złożoność systemów.

##### Prawa łączności
Grupowanie operandów nie wpływa na wynik operacji:
$$
A \lor (B \lor C) = (A \lor B) \lor C
$$
$$
A \land (B \land C) = (A \land B) \land C
$$
##### Prawa przemienności
Kolejność operandów nie wpływa na wynik operacji.
$$
A \lor B = B \lor A, \quad A \land B = B \land A
$$

##### Prawa rozdzielności
Iloczyn względem sumy:
$$
A⋅(B+C)=(A⋅B)+(A⋅C)
$$
Suma względem iloczynu.
$$
A+(B⋅C)=(A+B)⋅(A+C)
$$
##### Prawo idempotentności
Powtórzenie tej samej zmiennej w operacji daje tę samą zmienną.
$$
A+A=A
$$
$$
A⋅A=AA
$$
##### Prawo redukcji (Konsensusu)
Redukcja redundancji w funkcjach logicznych.
$$
A⋅B+A⋅¬B=A
$$
$$
(A+B)(A+¬B)=A
$$
##### Prawo absorpcji
Uproszczenie wyrażeń logicznych.
$$
A+A⋅B=A
$$
$$
A⋅(A+B)=A
$$

##### Prawo De Morgana
Negacja sumy.
$$
¬(A+B)=¬A⋅¬B
$$
Negacja iloczynu.
$$
¬(A⋅B)=¬A+¬B
$$

##### Prawo podwójnej negacji
Dwukrotne zaprzeczenie zmiennej przywraca jej pierwotną wartość.
$$
¬(¬A)=A
$$

##### Rozszerzone prawa redukcji
Kombinacja zmiennych i ich negacji.
$$
A+¬A⋅B=A+B
$$
$$
A⋅(¬A+B)=A⋅B
$$

---
### Minimalizacja Funkcji Logicznych

Minimalizacja funkcji logicznych to proces upraszczania wyrażeń logicznych tak, aby były one możliwie najprostsze. Celem minimalizacji jest zmniejszenie liczby operacji logicznych oraz komponentów sprzętowych (np. bramek logicznych) potrzebnych do realizacji danej funkcji.

Minimalizacja funkcji logicznych jest ważnym elementem techniki cyfrowej. Umożliwia ona zredukowanie liczby bramek logicznych, co przekłada się na niższe koszty produkcji i mniejsze zużycie energii. Dodatkowo redukujemy opóźnienia propagacyjne (Krótsze ścieżki oznaczają działanie układu). Redukcja zwiększa również czytelność, prostsze wyrażenia są łatwiejsze do zrozumienia, analizy i testowania.

### Metody Minimalizacji Funkcji Logicznych
#### **Siatki Karnaugha**
Siatki Karnaugha (tabela Karnaugha) to graficzne narzędzie służące do minimalizacji funkcji logicznych. Pozwalają na łatwe uproszczenie funkcji poprzez wizualne grupowanie sąsiadujących mintermów (kombinacji wejść, dla których funkcja przyjmuje wartość 1). Stosuje się ją do upraszczania funkcji logicznych o małej ilości zmiennych (do 6). Dla większej ilości zmiennych stosuje się komputerowy algorytm Quine'a-McCluskeya.

##### Konstrukcja Siatki Karnaugha
Siatka Karnaugha jest zbudowana jako tablica dwuwymiarowa, gdzie liczba komórek odpowiada liczbie możliwych kombinacji zmiennych wejściowych:
- 2 zmienne: 4 komórki ($2^2$).
- 3 zmienne: 8 komórek ($2^3$).
- 4 zmienne: 16 komórek ($2^4$).
Indeksowanie komórek odbywa się zgodnie z [kodem Gray'a](https://pl.wikipedia.org/wiki/Kod_Graya), aby zapewnić sąsiedztwo jednego bitu różnicy. 

##### Zasady Minimalizacji
W celu minimalizacji funkcji logicznych należy wypełnić mapę Karnaugha wartościami (1 lub 0) odpowiadającymi wartościom funkcji dla wartości argumentów opisujących dane pole w tablicy. Następnie grupuje się pola o wybranej wartości (1 aby uzyskać funkcję minimalną w postaci sumy, 0 dla postaci iloczynu). Grupy muszą mieć kształt prostokąta o długościach boków będących potęgami dwójki (przy czym może on przechodzić przez krawędź tablicy, a dla liczby zmiennych powyżej 4 nie musi być spójny, a jedynie łączyć pola sąsiednie logicznie). W celu uzyskania postaci minimalnej, grupy powinny być możliwie największe. Jedno pole może należeć do wielu grup. W każdej uzyskanej grupie część wartości zmiennych będzie wspólna dla wszystkich pól i to z nich powstaje wyrażenie odpowiadające danej grupie. Jeżeli pogrupowane zostały jedynki, wyrażenie dla pojedynczej grupy będzie miało postać iloczynu zmiennych, które, jeżeli w danej grupie przyjmują wartość 1, będą występowały w postaci prostej, jeżeli 0 – w postaci zanegowanej (zmienne przyjmujące w danej grupie różne wartości są pomijane); funkcja końcowa będzie sumą tych iloczynów. Jeżeli utworzono grupy zer, wyrażenie dla danej grupy będzie sumą zmiennych w postaci zanegowanej, jeżeli w danej grupie mają wartość 1, prostej, jeśli 0; wynik będzie iloczynem takich sum. Tak więc im grupa jest większa, od tym mniejszej liczby zmiennych zależy.

![[Pasted image 20250108070743.png]]

![[Pasted image 20250108070800.png]]

##### Przykład
![[Pasted image 20250108071418.png]]
![[Pasted image 20250108071428.png]]
![[Pasted image 20250108071447.png]]

##### Przykład 2
![[Pasted image 20250108071532.png]]
![[Pasted image 20250108071548.png]]![[Pasted image 20250108071608.png]]
![[Pasted image 20250108071619.png]]

##### [Przykłady Zadań](https://www.mcholewa.us.edu.pl/Downloads/root/siatki-karnaugh.pdf)

---
### Metoda Quine’a-McCluskeya
Drugi popularny sposób minimalizacji funkcji logicznych, daje identyczne wyniki do metody Karnaugh, ale w przeciwieństwie do niej dużo łatwiej daje się zaimplementować na komputerze.

##### Algorytm
Załóżmy, że mamy daną funkcję:

$$
f(A,B,C,D) = \Sigma \ m(4,8,10,11,12,15) + d(9,14)
$$

Powyższy zapis oznacza, że mamy daną funkcję 4 zmiennych, która będzie dawała wartość 1, dla argumentów 4, 8, 10, 12, oraz 15. Będzie ona niezdefiniowana dla 9 i 14, a dla pozostały wartości będzie dawać 0.

Powyższą funkcję, można zapisać w postaci:
$$
\begin{align}
f(A,B,C,D) = (\neg A \ B \ \neg C \ \neg D) + (A \ \neg B \ \neg C \ \neg D) + (A \ \neg B \ C \ \neg D) \\ + (A \ \neg B \ C \ D) + (A \ B \ \neg C \ \neg D)(ABCD)
\end{align}
$$

Tworzymy ją na podstawie wartości w nawiasie, przykładowo:

$$ 4 = 0100 \implies (\neg A \ B \ \neg C \ \neg D) $$
Ponieważ jest tu funkcja sumy, i dla podanych wartości funkcja przyjmuje wartości 1, to jeśli na danym bicie mamy jedynkę, to wstawiamy zwykłą wartość zmiennej (tak jak w przypadku B), jeśli wartość wynosi 0, to negujemy zmienną (A, C, D).

Teraz każdą wartość z $m$ należy zamienić na postać binarną:
$4 = 0100$
$8 = 1000$
$10 = 1010$
$12 = 1100$
$15 = 1111$

Tak samo dla stanów nieokreślonych:
$9=1001$
$14 = 1110$

Teraz należy pogrupować wartości zgodnie z ilością jedynek, które znajdują się w ich binarnej reprezentacji:

$$
\begin{array}{|c|c|c|}
\hline
\textbf{Ilość jedynek} & \textbf{Iloczyn zupełny} & \textbf{Reprezentacja binarna} \\ \hline
1 & m4  & 0100 \\ \hline
1 & m8  & 1000 \\ \hline
1 & m9  & 1001 \\ \hline
2 & m10 & 1010 \\ \hline
2 & m12 & 1100 \\ \hline
3 & m11 & 1011 \\ \hline
3 & m14 & 1110 \\ \hline
4 & m15 & 1111 \\ \hline
\end{array}
$$

Kolejnym krokiem jest uproszczenie grup. Jest to proces, który finalnie powinien nas doprowadzić do tych samych grup, co w przypadku metody Karnaugh. Jest to jednak dużo wydajniejszy i prostszy sposób poszukiwania optymalnego grupowania, w porównaniu do do metody Karnaugh jeśli chodzi o implementację komputerową.

Proces uproszczania polega na badaniu grupy $n$ i $n+1$. Polega to na porównaniu wartości i znalezieniu tych, które różnią się tylko na jednej pozycji. Pozycję, na której dwie wartości się różnią oznaczamy $-$ (minus). Powstałe grupy również względem ilości jedynek. Otrzymujemy implikanty rozmiaru 2. Jeśli, któryś iloczyn nie może być połączony z żadnym innym oznaczamy go $*$ (gwiazdka) - jest to nasz implikant prosty, czyli taki, którego nie da się już bardziej uprościć. Proces ten powtarzamy, łącząc implikanty rozmiaru 2 w 4 itd.

![[Pasted image 20250108181748.png]]

W naszym przypadku, aby uzyskać wszystkie możliwe implikanty proste, wystarczyło dojść do rozmiaru 4, natomiast można dojść do 8, 16 itd.

Teraz tworzymy tabelę, która pozwoli nam uzyskać finalny wynik. Wiersze tej tabeli to znalezione implikanty proste (te, które oznaczaliśmy gwiazdką), a kolumny to liczby ze zbioru $m$. 
***Nie bierzemy już pod uwagę stanów nieokreślonych.*** W tabeli zaznaczamy „X” tam, gdzie dany implikant pokrywa dany minterm (czyli zawiera tę kombinację w swojej definicji). Teraz poszukujemy implikantów istotnych (czyli najważniejszych) - jeśli w kolumnie jest tylko jeden "X", oznacza to, że tylko jeden implikant może pokryć ten minterm (wartość $m$ z kolumny). Mówiąc prościej jeden X w kolumnie, dany stan wejść może zostać uzyskany tylko przez jedną kombinacje wejść. Pozostałe mintermy pokrywamy za pomocą metody Petricka, lub wybierając tak, aby użyć minimalnej liczby implikantów.

![[Pasted image 20250108182605.png]]

Zatem na pewno w naszym wyniku otrzymamy:
$$
(B \ \neg C \ \neg D) + (A \ C)
$$
Ponieważ są to implikanty istotne, które pokrywają mintermy, które nie mogą być pokryte przez inne. Problemem jest to, że te implikanty nie pokrywają wszystkich mintermów (8 nie jest pokryte ani przez pierwszy, ani ostatni wiersz).

Żeby znaleźć finalny kompletny wynik stosujemy metodę Petricka. Dla każdego mintermu tworzymy wyrażenia logiczne opisujące, które implikanty go pokrywają (symbolizowane, jako $P_{n}$)

Minterm 4 pokryty jest przez wiersz 1 ($P_{1}$)
$$
\begin{align}
4 \to P_{1}
\end{align}
$$
Minterm 8 pokryty jest przez wiersz 2 i 3 ($P_{2}, P_{3}$)
$$
\begin{align}
8 \to P_{2} + P_{3}
\end{align}
$$
Minterm 10 pokryty jest przez wiersz 2, 3, 4 ($P_{2}, P_{3}, P_{4}$)
$$
\begin{align}
10 \to P_{2} + P_{3} + P_{4}
\end{align}
$$
Minterm 11 pokryty jest przez wiersz 2 i 4 ($P_{2}, P_{4}$)
$$
\begin{align}
11 \to P_{2} + P_{4}
\end{align}
$$
Minterm 12 pokryty jest przez wiersz 1 i 3 ($P_{1}, P_{3}$)
$$
\begin{align}
12 \to P_{1} + P_{3}
\end{align}
$$
Minterm 15 pokryty jest przez wiersz 4 ($P_{4}$)
$$
\begin{align}
15 \to P_{4}
\end{align}
$$

Tworzymy teraz iloczyn logiczny powyższych warunków:
$$
F = (P_{1}) \ \cdot \ (P_{2} + P_{3}) \ \cdot \ (P_{2} + P_{3} + P_{4}) \ \cdot \ (P_{2} + P_{4}) \ \cdot \ (P_{1} + P_{3}) \ \cdot \ (P_{4})
$$

Wiemy, że implikanty $P_{1}$ i $P_{4}$ są istotne i muszą być zawarte w rozwiązaniu. Pokrywają nam one wartości 4 i 15, zatem spośród pozostałych implikantów musimy wybrać te (jeden lub więcej), które pokryją pozostałe, czyli 8, 10, 11, 12.

$P_{2} = m(8,10,11)$
Pokrywa 8. 10, 11 jest już pokryte przez P4.

$P_{3} = m(8, 10, 12, 14)$
Pokrywa 8. 10, 12 i 14 jest już pokryte przez P1.

W tym przypadku, ponieważ zarówno $P_{2}$ i $P_{3}$ pokrywają pozostałe mintermy w ten sam sposób, nie ma znaczenia, które wybierzemy. Na tym etapie poza implikantami istotnymi wybieramy te, który pokrywają nam jak najwięcej minterów nie pokrytych przez implikanty istotne.

Zatem finalny wynik to:

$$
f_{A,B,C,D} = (B \ \neg C \ \neg D) + (A \ C) + (A \ \neg B)
$$
lub:
$$
f_{A,B,C,D} = (B \ \neg C \ \neg D) + (A \ C) + (A \ \neg D)
$$