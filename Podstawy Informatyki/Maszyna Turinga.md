Maszyna Turinga to abstrakcyjny, matematyczny model obliczeniowy, który składa się z:

- Nieskończonej w obie strony taśmy, która podzielona jest na komórki, które mogą zawierać symbole z ustalonego alfabetu. Np. 0, 1, lub □ (symbol pusty). Alfabet może być dowolny, jednak ograniczony do skończonej liczby symboli.

- Głowicy, która porusza się po taśmie w lewo lub prawo. Głowica ta odczytuje symbol z aktualnej komórki taśmy. Głowica może również zapisywać symbole na taśmie.

- Stanu wewnętrznego, który określa aktualny stan maszyny, który może być oznaczany literami: q0​,q1​,qf.

- Funkcji przejścia, która określa co maszyna robi w odpowiedzi na aktualny stan i symbol, który został odczytany z taśmy. Funkcja ta decyduje o nowym stanie maszyny, symbolu do zapisania na taśmie, oraz kierunku ruchu głowicy (L - lewo, R - prawo, lub S - brak ruchu).

Maszyny Turinga rozpoczyna swoje działanie w stanie początkowym q0. Następnie głowica odczytuje symbol z bieżącej komórki taśmy. Na podstawie funkcji przejścia maszyna:

- Zapisuje nowy symbol w bieżącej komórce.
- Przechodzi do nowego stanu.
- Przesuwa głowicę w lewo, lub prawo.

Proces ten powtarza się, dopóki maszyna nie przejdzie do stanu akceptującego (stan końcowy qf), lub nie zatrzyma się z innego powodu.

---

Programowanie Maszyny Turinga polega na zdefiniowaniu tabeli przejść lub reguł, które określają zachowanie maszyny dla każdego stanu i symbolu. Logika Maszyny Turinga musi zakładać skończoność programu (tj. Nie może istnieć sytuacja, w której maszyna będzie przesuwać głowicę w nieskończoność).

Przykładowo, możemy stworzyć program, umożliwiający inkrementacje liczby binarnej. Założeniem programu jest to, że na taśmie zapisana jest liczba w postaci binarnej np. 1011. Maszyna Turinga dodaje do niej 1, zwracając wynik w postaci 1100. Działanie maszyny jest następujące:

- Maszyna przesuwa głowicę, aż znajdzie pustą komórkę, która oznacza koniec liczby binarnej.
- Następnie, przesuwa się w lewo, aby rozpocząć dodawanie od najmniej znaczącego bitu:
- Jeśli bit ma wartość 0, zamień na 1 i zakończ działanie programu.
- Jeśli bit ma wartość 1, zmień wartość na 0 i przejdź do kolejnego bitu.
- Jeśli głowica napotka pustą komórkę z lewej strony (np. Po przeniesieniu), zapisuje 1, jako dodanie najstarszego bitu.

Alfabet: 0, 1, □.

|   |   |   |   |   |
|---|---|---|---|---|
|Stan|Wartość Komórki|Nowa Wartość Komórki|Ruch Głowicy|Nowy Stan|
|q0|0|0|R|q0|
|q0|1|1|R|q0|
|q0|□|□|L|q1|
|q1|0|1|S|qf|
|q1|1|0|L|q1|
|q1|□|1|S|qf|

Możemy wyróżnić 3 stany pracy maszyny:

- q0, w którym głowica przesuwa się w prawo do momentu znalezienia końca liczby.
- q1, w którym maszyna dokonuje inkrementacji
- qf, stan końcowy

Pomimo swojej prostoty, Maszyna Turinga umożliwia implementację dowolnego algorytmu komputerowego.