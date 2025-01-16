Funkcjonalne bloki [1](http://www.ue.eti.pg.gda.pl/~waldi/EDM/Materialy/Technika_cyfrowa.pdf) cyfrowe to podstawowe elementy składające się na układy cyfrowe, realizujące określone funkcje logiczne, matematyczne lub sterujące. Stanowią one fundament projektowania nowoczesnych systemów cyfrowych, takich jak mikroprocesory, systemy wbudowane, czy układy sterujące.

### Bramki Logiczne
Podstawowe elementy układów cyfrowych realizujące proste operacje logiczne. Ich działanie oparte jest na algebrze Boole'a.

**AND (iloczyn logiczny)** - wynik to 1, gdy wszystkie wejścia są równe 1.
**OR (suma logiczna)** - wynik to 1, gdy co najmniej jedno wejście jest równe 1.
**NOT (negacja)** - odwraca stan logiczny wejścia.
**NAND, NOR, XOR, XNOR** - kombinacje lub wariacje podstawowych funkcji logicznych.

![[Pasted image 20250108195748.png]]

Wykorzystywane są one do realizacji złożonych funkcji logicznych oraz realizacji układów kombinacyjnych. Dodatkowo za pomocą bramek OR, AND i NOT jesteśmy w stanie zrealizować **układy zupełne**, które są w stanie zrealizować dowolną funkcję logiczną. NAND i NOR nazywa się **funkcjonalnie pełnymi** i można za ich pomocą zrealizować dowolną funkcję logiczną. Różnica między układem zupełnym, a pełnym polega na tym, że układy zupełne realizują dowolną funkcję za pomocą ***co najmniej dwóch bramek***, a układy pełne przy pomocy ***tylko jednego typu bramki***.

---
### Układy Kombinacyjne
Rodzaj układów cyfrowych charakteryzujący się tym, że stan wyjść zależy tylko i wyłącznie od stanu wejść. Stan wyjść opisują funkcje boole'owskie, których argumentami są stany wejść. W przeciwieństwie do układów sekwencyjnych, gdzie stan wyjść nie zależy tylko od stanu wejść, ale również od poprzedniego stanu układu. Z tego powodu w układach kombinacyjnych nie występuje sprzężenie zwrotne. W takich układach występuje niekorzystne zjawisko nazywane hazardem, które wynika z niezerowego czasu propagacji (rozchodzenia się) sygnałów. W układach synchronicznych zjawisko hazardu praktycznie nie występuje, ze względu na takie elementy jak obecność pamięci, czy synchroniczności i synchronizacji zegarowej.

##### Komutatory
Układy kombinacyjne, które dokonują wyboru, lub rozdzielenia sygnałów w zależności od wartości sygnałów sterujących.
##### Komutatory - Multiplekser
Układ wybierający jeden z wielu sygnałów wejściowych i przekazuje go na wyjście, zależnie od sygnałów sterujących (adresujących):
- **Wejścia:** $N$ wejść danych (np. 2, 4, 8), 1 lub więcej wejść sterujących.
- **Wyjście:** 1 linia wyjściowa.
- **Zasada działania:** Multiplekser przekazuje sygnał wejściowy na wyjście na podstawie kombinacji sygnałów sterujących. Jeśli mamy $2^n$ wejść, potrzebujemy $n$ bitów sterujących, aby wybrać odpowiedni sygnał wejściowy.
- **Przykład:** 4-na-1 multiplekser ma 4 wejścia danych i 2 bity sterujące ($2^2=4$), dzięki temu wybieramy jeden z 4 sygnałów wejściowych.

![[Pasted image 20250108195234.png]]

##### Komutatory - Demultiplekser
Układ odwrotny do multipleksera. Rozdziela jeden sygnał wejściowy na wiele sygnałów wyjściowych, zależnie od sygnałów sterujących:
- **Wejścia:** 1 wejście danych, 1 lub więcej wejść sterujących.
- **Wyjścia:** $N$ wyjść (np. 2, 4, 8).
- **Zasada działania:** Demultiplekser przyjmuje jeden sygnał na wejściu i kieruje go na jedno z wielu wyjść, zależnie od kombinacji układów sterujących.
- **Przykład:**  1-na-4 demultiplekser ma 1 wejście danych i 2 bity sterujące, a jego wyjścia są zależne od 2 bitów sterujących.

![[Pasted image 20250108195336.png]]

##### Konwertery Kodów
Układy kombinacyjne służące do przekształcania informacji reprezentowanej w jednym kodzie do innego formatu.
### Konwertery Kodów - Koder
Układ, który zmienia kod "1 z n" na dowolny inny kod dwójkowy (różny od 1 z n) o długości K, czyli służy on do przedstawiania informacji tylko jednego aktywnego wejścia na postać binarną. Ponieważ istnieje fizyczna możliwość aktywacji więcej niż jednego wejścia, musi istnieć możliwość uznania tylko jednego z nich np. poprzez ustalenie priorytetów wejść. Przykładowym zastosowaniem może być wprowadzenie informacji do systemów cyfrowych z klawiatury numerycznej.
- **Wejścia:** $2^n$ wejść danych.
- **Wyjścia:** $N$ bitów kodu.
- **Zasada działania:** Koder przypisuje unikalny kod binarny do każdego z wejść, a następnie przesyła ten kod na wyjście.
- **Przykład:** Koder 4-do-2 (4 wejścia, 2 bity wyjściowe) przypisuje każdemu z 4 wejść binarny kod 2-bitowy (np. wejście 1 → 00, wejście 2 → 01 itd.).

![[Pasted image 20250108195651.png]]

##### Konwertery Kodów - Dekoder
Układ, który zmienia naturalny kod binarny o długości $n$, lub każdego innego kodu, na kod "1 z n" (o długości K). Jego działanie jest odwrotne do Kodera, tzn. zamienia kod binarny na jego reprezentacje w postaci tylko jednego wybranego wyjścia. W zależności od ilości wyjść nazywa się go dekoderem 1 z N.
- **Wejścia:** N bitów kodu.
- **Wyjścia:** 2^n wyjść.
- **Zasada działania:** Dekoder "rozpakowuje" kod binarny i ustawia odpowiednie wyjście w stan aktywny (zwykle na 1), podczas gdy pozostałe pozostają w stanie nieaktywnym (zwykle 0).
- **Przykład:** Dekoder 2-do-4 przyjmuje 2 bity kodu i wybiera jedno z 4 wyjść (np. kod 00 → wyjście 0, kod 01 → wyjście 1 itd.).

![[Pasted image 20250108195723.png]]

##### Konwertery Kodów - Transkoder
Układ, który przekształca kod z jednej postaci na inną (oba kody muszą być różne od "1 z n"), ale na ogół zachowuje tą samą liczbę bitów. Czyli posiada $n$ wejść oraz $k$ wyjść. Typowym przykładem takiego układu jest układ zmieniający naturalny kod binarny na kod wyświetlacza siedmiosegmentowego (mylony często z dekoderem). Różnica miedzy transkoderem, a dekoderem polega na tym, że transkoder zmienia jedynie formę reprezentacji na inną formę reprezentacji przy tej samej liczbie bitów
- **Wejścia:** N bitów wejściowych.
- **Wyjścia:** M bitów wyjściowych, gdzie N może być różne od M.
- **Zasada działania:** Transkoder zmienia sposób reprezentowania wartości bez zmiany ilości informacji.
- **Przykład:** Transkoder 4-do-3 zmienia 4-bitowy kod na 3-bitowy, zmieniając kodowanie bez utraty informacji.

![[Pasted image 20250108200620.png]]

### Bloki Artmetyczne
Układy kombinacyjne, które wykonują operacje matematyczne lub porównawcze na liczbach binarnych.
##### Sumator (Adder)
Układ służący do dodawania dwóch (lub więcej) liczb binarnych. Sumatory można podzielić na:
- Szeregowe (Serial Adder): podczas każdej operacji dodają one dwa bity składników oraz przeniesienia.
- Równoległe (Parallel Adder): wielopozycyjne, dodają do siebie jednocześnie bity ze wszystkich pozycji, a przeniesienie realizowane jest w zależności od sposobu łączenia sumatorów jednobitowych. Sumatory równoległe obejmują dwie grupy: Z przeniesieniem szeregowym i równoległym. Każdy sumator charakteryzuje się typem ukończenia:
	- Sumator Pełny - Dodaje dwie cyfry binarne i uwzględnia przeniesienie z poprzedniej operacji dodawania.
	- Sumator Półpełny - Dodaje dwie pojedyncze cyfry binarne. Składa się z bramki XOR (sumy) i bramki AND (przeniesienie).

	Każdy sumator pełny składa się z dwóch sumatorów półpełnych.

Przykład Sumatora 1-bitowego:

0 + 0 = 0  
0 + 1 = 1  
1 + 0 = 1  
1 + 1 = 0 i przeniesienie do następnej kolumny.

Uwzględniając przeniesienie z poprzedniej pozycji możemy rozszerzyć podane reguły dodawania. Oznaczmy indeksem 1 przeniesienie z poprzedniej pozycji (w pierwszej kolumnie przeniesienie to po prostu wynosi 0), które musimy dodać do wyniku dodawania cyfr na bieżącej pozycji, a indeksem 2 przeniesienie do następnej pozycji. Otrzymamy następujące reguły dodawania pojedynczych bitów:

$$
\begin{align}
0 + 0 + 0_{1} = 0 \ i \ 0_{2}  \\
0 + 1 + 0_{1} = 1 \ i \ 0_{2}  \\
1 + 0 + 0_{1} = 1 \ i \ 0_{2}  \\
1 + 1 + 0_{1} = 0 \ i \ 1_{2}  \\
0 + 0 + 1_{1} = 1 \ i \ 0_{2}  \\
0 + 1 + 1_{1} = 0 \ i \ 1_{2}  \\
1 + 0 + 1_{1} = 0 \ i \ 1_{2}  \\
1 + 1 + 1_{1} = 1 \ i \ 1_{2} \\
\end{align}
$$
![[Pasted image 20250109190036.png]]

Funkcje logiczne dla sygnałów wyjściowych Y i C2 otrzymamy na podstawie reguł dodawania z przeniesieniem. W tym celu układamy tablice Karnaugha. Funkcje sprowadzamy do postaci NAND i NOT, aby można było zastosować standardowe bramki logiczne.

![[Pasted image 20250109190149.png]]

![[Pasted image 20250109190156.png]]

![[Pasted image 20250109190226.png]]

![[Pasted image 20250109190230.png]]

###### Sumator Pełny (Uwzględnia przeniesienia, jako sygnał wejściowy)
![[Pasted image 20250111110546.png]]

##### Komparator
Układ kombinacyjny służący do porównywania dwóch liczb binarnych (komparator cyfrowy), albo dwóch poziomów napięć (komparator analogowy). Głównym zadaniem komparatora cyfrowego jest analiza dwóch wejściowych sygnałów cyfrowych (reprezentujących liczby) i wydanie odpowiedniego sygnału wyjściowego, który wskazuje wynik porównania.

Komparator przyjmuje dwa zestawy sygnałów binarnych oznaczonych, jako A i B. Każdy zestaw  to reprezentacja liczb w postaci cyfrowej (np. A = 101, B = 1100). Następnie komparator porównuje bity obu liczb w odpowiednich miejscach (od najwyższego do najniższego bitu). Na przykład, w przypadku 4-bitowego porównania, komparator analizuje kolejno bity A3, A2, A1, A0 z bitami B3, B2, B1, B0. Po dokonaniu analizy komparator generuje odpowiednie sygnały wyjściowe, które mogą wskazywać:
- A > B
- A < B
- A = B
  
![[Pasted image 20250109191618.png]]
![[Pasted image 20250111123850.png]]
###### Jak komparator porównuje bity?
1. **Porównanie bitów zaczynając od najbardziej znaczącego (MSB)**: Komparator zaczyna porównywać bity obu liczb od najbardziej znaczącego bitu (najwyższy bit, czyli najbardziej na lewo). To jest kluczowy punkt, ponieważ najbardziej znaczący bit w systemie binarnym ma największy wpływ na wartość liczby.
    - Jeśli bit w liczbie **A** jest większy niż odpowiadający mu bit w liczbie **B**, to liczba **A** jest większa i komparator natychmiast wydaje sygnał wskazujący, że **A > B**.
    - Jeśli bit w liczbie **B** jest większy niż bit w liczbie **A**, to liczba **B** jest większa i komparator wydaje sygnał wskazujący, że **A < B**.
2. **Porównanie kolejnych bitów**: Jeśli najbardziej znaczące bity obu liczb są równe (A = B), komparator przechodzi do porównania kolejnych bitów, od drugiego najbardziej znaczącego bitu (A2 z B2), aż do najmniej znaczącego bitu. Cały proces polega na porównywaniu bit po bicie, aż do momentu, gdy któryś bit wskazuje, że jedna liczba jest większa lub mniejsza od drugiej.
    - Jeśli w którymś momencie komparator znajdzie, że **A_i > B_i**, komparator może natychmiast wydać wynik, że **A > B** i zakończyć dalsze porównania.
    - Jeśli w którymś momencie komparator znajdzie, że **A_i < B_i**, komparator natychmiast wyda wynik, że **A < B** i zakończy dalsze porównania.
3. **Porównanie całkowite**: Jeśli wszystkie bity w obu liczbach są równe (A = B), to komparator uznaje liczby za równe i wydaje sygnał **A = B**.


##### ALU - Arithmetic and Logic Unit (Jednostka Arytmetyczno-Logiczna)
Kluczowy element procesora. Jej główną funkcją jest wykonywanie operacji arytmetycznych, takich jak dodawanie, odejmowanie, mnożenie, przesunięcie bitowe, oraz wykonywanie operacji logicznych takich jak AND, OR, XOR, NOT na danych wejściowych. ALU przyjmuje dane wejściowe w postaci binarnej i na ich podstawie wykonuje określoną operację, a wynik tej operacji jest przekazywany na wyjście. Jest to układ kombinacyjny, ponieważ stany wyjść są zależnie tylko od stanów wejść, a historyczne stany jednostki nie wpływają na wynik.
###### Budowa ALU
Schemat budowy 2 bitowej jednostki arytmetyczno logicznej:
![[Pasted image 20250111115154.png]]

W tym przypadku jednostka arytmetyczno logiczna składa się z bramek umożliwiających operacje logiczne: XOR, AND, OR. Następnie mamy sumatory pełne, które umożliwiają dodawanie z uwzględnieniem przeniesienia, oraz informują o przeniesieniu na wyjściu. Układ posiada również dwa multipleksery, które umożliwiają sterowanie wyjściem układu, tj. który wynik operacji ALU chcemy odczytać. Warto zauważyć, że ALU wykonuje te operacje równolegle, ze względu na izolacje poszczególnych układów.

**Generalnie ALU składa się z:**
- **Rejestrów wejściowych**, przez które odbiera dane wejściowe, które są przechowywane w rejestrach. Wartości te mogą pochodzić z pamięci lub innych części procesora.
- **Multiplekser**, który w przypadku bardziej złożonych operacji logicznych czy arytmetycznych może być używany, aby wybierać odpowiednie dane wejściowe do obróbki i wyjściowe w zależności od wymaganej operacji.
- **Jednostki arytmetyczne:** Do realizacji operacji arytmetycznych, takich jak dodawanie i odejmowanie, w ALU znajdują się takie elementy jak:
	- **Sumator (Adder):** Odpowiedzialny za dodawanie liczb binarnych.
	- **Komparator:** Służy do porównywania dwóch liczb (np. sprawdzanie równości lub większości).
- **Jednostki logiczne:** Odpowiadają za realizację operacji logicznych, takich jak AND, OR, XOR, NOT. Te operacje są realizowane przy użyciu bramek logicznych.
- **Sterownik:** Część ALU, która kontroluje, jaka operacja ma zostać wykonana, na podstawie sygnałów sterujących (np. kodów operacji). Sterownik wybiera odpowiednią jednostkę arytmetyczną lub logiczną, aby wykonać wybraną operację.
- **Rejestry wyjściowe:** Po wykonaniu operacji, wynik jest zapisywany w rejestrze wyjściowym, który może być następnie przekazany do innych części systemu (np. pamięci, innych rejestrów lub jednostki sterującej).


---
### Układy Sekwencyjne
Rodzaj układów cyfrowych, w których stan wyjść zależy od stanu wejść układu oraz poprzedniego stanu, zwanego stanem wewnętrznym, pamiętanego w zespole rejestrów (**pamięci**). Jeśli stan wewnętrzny układu nie ulega zmianie pod wpływem podania na wejście różnych sygnałów, to taki stan nazywa się **stanem stabilnym**. Wyróżniamy dwa rodzaje układów sekwencyjnych: **synchroniczne** i **asynchroniczne**.

![[Pasted image 20250111125030.png]]

Układ sekwencyjny może zostać opisany, jako:
$$
Y = f(X, A)
$$
gdzie wyjście zależy od stanu wewnętrznego i wejść, lub:
$$
Y = f(A)
$$
gdzie wyjście zależy wyłącznie od stanu wewnętrznego.

- $A$ - Stan wewnętrzny.
- $X \ i \ Y$ - wejścia i wyjścia.

Pierwsza z funkcji dotyczy automatu Mealy'ego, druga automatu Moore'a. Oba te automaty są sobie równoważne. Zachowanie układu sekwencyjnego może być opisywane:
- Słownie.
- Jako przebieg czasowy, pokazując zależności pomiędzy $X$, $A$, a $Y$.
- W postaci grafu przejść.
- Jako tablica przejść i wyjść.

##### Asynchroniczne Układy Sekwencyjne
Układy cyfrowe, w których zmiana stanu i generacja wyjść zachodzą **bez użycia globalnego sygnału zegarowego**. Przejścia między stanami następują natychmiast po zmianie sygnałów wejściowych, co odróżnia je od synchronicznych układów sekwencyjnych, które działają w oparciu o taktowanie zegarowe. Podstawową cechą asynchronicznych układów sekwencyjnych jest to, że przejścia między stanami są wyzwalane bezpośrednio przez zmiany wejść, co pozwala na szybszą reakcję na zmieniające się warunki. Taka konstrukcja sprawia jednak, że układy te są bardziej wrażliwe na zakłócenia i błędy projektowe. W szczególności mogą występować tzw. hazardy, czyli krótkotrwałe, niepożądane zmiany sygnałów wyjściowych wynikające z różnych opóźnień propagacji sygnałów wewnętrznych. Dodatkowym problemem są wyścigi sygnałów, czyli sytuacje, w których równoczesna zmiana kilku sygnałów wejściowych prowadzi do nieprzewidywalnych przejść stanów. Wyścigi te mogą być krytyczne, gdy prowadzą do błędnego działania układu, lub niekrytyczne, gdy nie wpływają na poprawność pracy.

Asynchroniczny układ sekwencyjny można opisać podobnie jak automat skończony, ale bez użycia zegara:
- **Zbiór stanów S** – reprezentuje możliwe konfiguracje układu.
- **Alfabet wejściowy Σ** – zestaw możliwych sygnałów wejściowych.
- **Alfabet wyjściowy Λ** – zestaw możliwych sygnałów wyjściowych.
- **Funkcja przejścia δ:S×Σ→S** – określa przejścia między stanami na podstawie bieżącego stanu i wejścia.
- **Funkcja wyjścia ω:S→Λ** – określa wyjście zależnie od aktualnego stanu.

**Problemy projektowe asynchronicznych układów**
1. **Hazardy:**
    - Krótkie, niepożądane zmiany wyjścia wynikające z różnic w opóźnieniach propagacji sygnałów.
    - Mogą powodować błędne działanie układu.
2. **Wyścigi (races):**
    - W sytuacji, gdy dwa lub więcej sygnałów zmienia się jednocześnie, mogą wystąpić nieprzewidywalne przejścia stanów.
    - Wyróżnia się wyścigi **krytyczne** (mogące prowadzić do błędów) i **niekrytyczne** (niepowodujące błędów).
3. **Synchronizacja:**
    - Trudności w zapewnieniu poprawnego działania w przypadku asynchronicznych zmian wielu wejść.

**Zalety asynchronicznych układów sekwencyjnych**
- **Szybkość działania:** Reagują natychmiast na zmiany wejść, co pozwala na szybsze działanie.
- **Mniejsze zużycie energii:** Brak zegara oznacza, że układ pracuje tylko wtedy, gdy jest to konieczne.
- **Prostota sprzętowa:** Brak skomplikowanego układu zegarowego zmniejsza fizyczną złożoność.
- **Mniejsza emisja elektromagnetyczna:** Brak taktowania zmniejsza zakłócenia.

**Wady asynchronicznych układów sekwencyjnych**
- **Trudności projektowe:** Trudniejsze do zaprojektowania, testowania i analizy.
- **Wrażliwość na hazardy:** Ryzyko niepożądanych przejść stanów.
- **Problemy z synchronizacją:** Utrudniona współpraca z innymi, synchronicznymi systemami.

**Zastosowania asynchronicznych układów sekwencyjnych**
- **Układy o niskim poborze energii** – np. urządzenia IoT, systemy wbudowane.
- **Specjalistyczne procesory** – układy działające w środowiskach o zmiennym obciążeniu.
- **Systemy o wysokiej niezawodności** – np. systemy kosmiczne, gdzie zegar mógłby być źródłem awarii.
- **Układy sterujące** – np. układy resetujące lub czujniki reagujące na zmiany.

##### Synchroniczne Układy Sekwencyjne
Kluczowy rodzaj układów cyfrowych, w których zmiany stanów oraz generowanie sygnałów wyjściowych odbywają się w sposób zsynchronizowany z globalnym sygnałem zegarowym. Oznacza to, że wszystkie elementy układu reagują na zmiany wejść i przejścia stanów tylko w ściśle określonych momentach, które wyznacza impuls zegara. Dzięki temu działanie układu jest przewidywalne i uporządkowane, co znacząco upraszcza jego projektowanie, testowanie oraz analizę. W układach synchronicznych podstawową rolę odgrywa **sygnał zegarowy** (ang. _clock signal_), który jest generowany przez oscylator. Ten sygnał zegarowy ma najczęściej postać przebiegu prostokątnego i składa się z powtarzających się impulsów. Zmiany stanów układu zachodzą zwykle na określonym zboczu tego sygnału – **narastającym** (ang. _rising edge_) lub **opadającym** (ang. _falling edge_). Dzięki temu elementy pamięci, takie jak **przerzutniki**, aktualizują swoje stany w sposób zsynchronizowany, co eliminuje ryzyko niekontrolowanych zmian.

**Budowa układów synchronicznych**
- **Przerzutniki:** Elementy pamięci przechowujące stan.
- **Układy kombinacyjne:** Odpowiadają za logikę przejść i generowanie wyjść.
- **Generator zegarowy:** Dostarcza sygnał taktujący.
- **Sieć dystrybucji zegara:** Zapewnia równomierne dostarczenie sygnału zegarowego do wszystkich komponentów.

**Rodzaje układów synchronicznych**
1. **Synchroniczne układy kombinacyjne:**  
    Wyjście zależy wyłącznie od bieżących sygnałów wejściowych.
2. **Synchroniczne układy sekwencyjne:**  
    Wyjście zależy od bieżących sygnałów wejściowych oraz od poprzednich stanów zapisanych w przerzutnikach.
3. **Automaty skończone:**  
    Układy modelowane jako **automat Mealy'ego** (wyjście zależy od stanu i wejścia) lub **automat Moore'a** (wyjście zależy tylko od stanu).

**Zalety układów synchronicznych**
- **Przewidywalność działania:** Dzięki zegarowi działanie układu jest deterministyczne.
- **Stabilność:** Brak problemów z hazardami i wyścigami.
- **Łatwość testowania:** Synchronizacja ułatwia diagnozowanie i wykrywanie błędów.
- **Skalowalność:** Łatwość integracji w dużych systemach (np. mikroprocesory, FPGA).

**Wady układów synchronicznych**
- **Problemy z dystrybucją zegara:** Trudności z równomiernym dostarczeniem sygnału zegarowego w dużych układach (**clock skew**).
- **Wysokie zużycie energii:** Wszystkie elementy układu są taktowane, co zwiększa pobór mocy.
- **Ograniczenia w szybkości działania:** Maksymalna częstotliwość pracy jest ograniczona przez najwolniejszy element układu.

**Techniki optymalizacji układów synchronicznych**
- **Bufory zegarowe:** Minimalizują różnice w dostarczaniu zegara do różnych części układu.
- **Clock gating:** Wyłączanie zegara dla nieaktywnych bloków w celu oszczędzania energii.
- **Dynamiczne skalowanie częstotliwości (DFS):** Dostosowywanie częstotliwości zegara do aktualnego obciążenia układu.

**Zastosowania układów synchronicznych**
- **Procesory i mikroprocesory** – centralne jednostki obliczeniowe.
- **Pamięci RAM** – szybkie pamięci operacyjne.
- **Układy FPGA** – programowalne układy logiczne.
- **Mikrokontrolery** – sterowanie urządzeniami elektronicznymi.
- **Systemy komunikacyjne** – kontrola przepływu danych w sieciach cyfrowych.
##### Automaty
Automaty Mealy'ego i Moore'a to dwa podstawowe modele automatów skończonych, wykorzystywane do modelowania systemów reagujących na ciąg wejściowy poprzez generowanie ciągu wyjściowego. Oba modele różnią się sposobem generowania wyjść, choć ich struktura jest podobna.
##### Automat Mealy'ego
Automat Mealy'ego to sześcio-składnikowy automat skończony, definiowany jako uporządkowana szóstka:

$$
M=(S,Σ,Λ,δ,ω,s_{0}​)
$$

gdzie:
- S – skończony zbiór stanów,
- Σ (Sigma) – skończony alfabet wejściowy,
- Λ (Lambda) – skończony alfabet wyjściowy,
- δ:S×Σ→S – funkcja przejścia,
- ω:S×Σ→Λ – funkcja wyjścia (zależna od stanu i wejścia),
- $s_{0}​∈S$ – stan początkowy.

Funkcja, definiująca automat:
$$
F(S, Σ)
$$

Widzimy zatem, że w tym automacie stan wyjścia zależy nie tylko od stanu wewnętrznego, ale również od stanu sygnałów wejściowych. Automat ten szybciej reaguje na zmiany, ponieważ wyjście może zmienić się natychmiast po zmianie wejścia. Dodatkowo zazwyczaj potrzebuje mniej stanów niż automat Moore'a dla tej samej funkcji.

Jeśli automat znajduje się w stanie $s$ i otrzyma symbol wejściowy $x$, przechodzi do stanu $δ(s,x)$ i generuje wyjście $ω(s,x)$.
##### Automat Moore'a
Automat Moore'a to sześcio-składnikowy automat skończony, definiowany jako uporządkowana szóstka:
$$M=(S,Σ,Λ,δ,ω,s_{0}​)$$
gdzie:
- S – skończony zbiór stanów,
- Σ (Sigma) – skończony alfabet wejściowy,
- Λ (Lambda) – skończony alfabet wyjściowy,
- δ:S×Σ→S – funkcja przejścia,
- ω:S×Σ→Λ – funkcja wyjścia (zależna od stanu i wejścia),
- $s_{0}​∈S$ – stan początkowy.

Funkcja definiująca automat:
$$
F(S)
$$
W tym automacie wyjście zależy tylko i wyłącznie od stanu wewnętrznego. Zapewnia stabilność ponieważ zmiana wyjścia następuje dopiero po przejściu do następnego stanu. Zazwyczaj wymaga on więcej stanów niż automat Mealy'ego, ale jest prostszy w projektowaniu i analizie.

[Synteza Automatów](http://antoni.sterna.staff.iiar.pwr.wroc.pl/luc/LUC_synteza_automatow.pdf)![[synteza-automat-mealy-rozpoznajacy-ciag.pdf]]
##### Dlaczego automat Moore'a jest prostszy w projektowaniu i analizie od automatu Mealy'ego?
Ponieważ dla automatu Moore'a, stan wyjścia zależy tylko i wyłącznie od stanu wewnętrznego automatu. Nie trzeba dzięki temu analizować kombinacji stanu wew. i wejścia do określenia wyjścia. Dodatkowo wyjście zmienia się tylko przy przejściu do innego stanu, co eliminuje ryzyko chwilowych, niepożądanych zmian wyjścia. Odbywa się to natomiast kosztem ilości stanów, ponieważ przy stanie wyjść, nie uwzględniamy wejść.

---
### Przerzutniki
Układ sekwencyjny, którego sygnał na wyjściu może zależeć od stanu na jego wejściu lub od jego stanu wewnętrznego. Istnieją trzy rodzaje przerzutników: bistabilne, monostabilne (tzw. uniwibratory) oraz astabilne (tzw. multiwibratory). W układach cyfrowych najczęściej stosowane są przerzutniki bistabilne mogące być stosowane jako układy pamiętające. Grupa czterech lub ośmiu połączonych ze sobą przerzutników bistabilnych może tworzyć tzw. rejestr, zdolny do pamiętania jednego bajta informacji.

Przerzutniki zbudowane są z bramek logicznych lub specjalnych układów scalonych. Podstawowym mechanizmem działania jest sprzężenie zwrotne, które pozwala na utrzymanie określonego stanu. Poniżej przedstawiono prosty schemat przerzutnika D:

![[Pasted image 20250111155314.png]]

Przerzutniki pełnią kluczową rolę w wielu zastosowaniach układów cyfrowych. Ich podstawowe funkcje to:
- **Przechowywanie informacji:** Służą jako podstawowe jednostki pamięci w układach logicznych.
- **Budowa rejestrów:** Grupując przerzutniki, tworzy się rejestry służące do przechowywania większej ilości danych.
- **Liczniki:** Przerzutniki są wykorzystywane do tworzenia liczników binarnych, które zliczają impulsy zegarowe.
- **Generatory sygnałów:** W połączeniu z bramkami logicznymi tworzą układy generujące sygnały taktujące i sterujące.
- **Automaty stanów:** Przerzutniki przechowują aktualny stan automatu skończonego, umożliwiając realizację logiki sterowania.
- **Pamięci RAM i ROM:** Są podstawą działania dynamicznych i statycznych pamięci komputerowych.

#### **Kluczowe parametry przerzutników**
- **Czas propagacji (Propagation Delay):** Opóźnienie między sygnałem wejściowym a zmianą stanu wyjścia.
- **Setup Time:** Minimalny czas, przez jaki sygnał wejściowy musi być stabilny przed zboczem zegara.
- **Hold Time:** Minimalny czas, przez jaki sygnał wejściowy musi pozostać stabilny po zboczu zegara.
- **Częstotliwość maksymalna:** Najwyższa częstotliwość, z jaką przerzutnik może pracować poprawnie.

#### **Rodzaje przerzutników i ich budowa**
1. [**Przerzutnik SR (Set-Reset)](https://www.geeksforgeeks.org/sr-flip-flop/):**
    - Najprostszy typ przerzutnika.
    - Ma dwa wejścia: **S (Set)** – ustawienie i **R (Reset)** – zerowanie.
    - Budowa: zwykle z dwóch bramek NAND lub NOR sprzężonych zwrotnie.
    - Problem: niepoprawny stan przy jednoczesnym podaniu sygnału na oba wejścia.
2. [**Przerzutnik D (Data/Delay)](https://www.geeksforgeeks.org/d-flip-flop/):**
    - Ulepszona wersja przerzutnika SR, która eliminuje niepoprawne stany.
    - Ma jedno wejście danych **D** i wejście zegarowe **CLK**.
    - Przy zboczu sygnału zegarowego stan wejścia **D** jest zapisywany na wyjście.
    - Budowa: modyfikacja przerzutnika SR z dodatkową bramką NOT.
3. [**Przerzutnik JK](https://www.geeksforgeeks.org/what-is-jk-flip-flop/?ref=ml_lbp):**
    - Rozbudowana wersja przerzutnika SR, która eliminuje niedozwolony stan.
    - Ma dwa wejścia sterujące: **J** (ustawienie) i **K** (zerowanie).
    - Przy jednoczesnym podaniu sygnału na **J** i **K** następuje zmiana stanu na przeciwny (toglowanie).
    - Budowa: wykorzystuje sprzężenie zwrotne z bramek logicznych.
4. **[Przerzutnik T (Toggle)](https://www.geeksforgeeks.org/t-flip-flop/?ref=ml_lbp):**
    - Specjalna odmiana przerzutnika JK z połączonymi wejściami **J** i **K**.
    - Przy każdym impulsie zegarowym zmienia swój stan na przeciwny.
    - Wykorzystywany głównie w licznikach binarnych.

#### **Podział przerzutników ze względu na zegar**
1. **Przerzutniki asynchroniczne:**
    - Zmieniają stan natychmiast po zmianie sygnału wejściowego.
    - Nie wymagają sygnału zegarowego.
2. **Przerzutniki synchroniczne:**
    - Zmieniają stan tylko na określonym zboczu sygnału zegarowego.
    - Gwarantują przewidywalność i uporządkowane działanie.