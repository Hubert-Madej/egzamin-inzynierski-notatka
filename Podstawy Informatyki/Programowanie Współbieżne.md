Zasobami systemu nazywam wszystkie ograniczone elementy, które są niezbędne do realizacji procesów w systemie komputerowy.

---
### Rodzaje zasobów:
1. Sprzętowe:
	1. Procesory.
	2. RAM (Pamięć Operacyjna)
	3. Urządzenia wejścia / wyjścia (np. Drukarki, klawiatury, dyski twarde).
2. Programowe:
	1. Pliki.
	2. Dane.
	3. Semafory i inne struktury synchronizacyjne.
    
### Cechy Zasobów:
1. Dzielone - Mogą być jednocześnie używane przez wiele procesów (np. Pliki w trybie tylko do odczytu).
2. Wyłącznego dostępu - w danym momencie dany zasób może być używany tylko przez jeden proces (np. drukarka).
3. Odnawialne - Mogą być ponownie przydzielane po zakończeniu operacji (np. procesor).
4. Nieodnawialne - Raz przydzielane zasoby są wyczerpane (np. Licencja na oprogramowanie).
---

Wzajemna blokada (Zakleszczenie) to sytuacja w systemie, w której dwa lub więcej procesów czeka na zasoby, które są jednocześnie zajmowane przez inne procesy, co prowadzi do trwałego zablokowania ich działania.

Warunki powstania wzajemnej blokady (ang. DeadLock) (Warunki Coffmana):

1. Wzajemne Wykluczenie (Mutual Exclusion) - Co najmniej jeden zasób musi być używany w trybie wyłączności.
    
2. Trzymanie i Czekanie (ang. Hold and Wait) - Procesy posiadają już przydzielone zasoby i jednocześnie oczekują na kolejne.
    
3. Brak wywłaszczenia (ang. No Preemption) - Zasoby nie mogą zostać odebrane procesowi - muszą być zwolnione przez proces, który je posiada.
    
4. Cykliczne oczekiwanie (ang. Circular Wait) - Istnieje cykl procesów, w którym każdy proces oczekuje na zasób trzymany przez następny proces w cyklu.

---

### Przykład DeadLock’a:
1. P1 posiada zasób R1 i oczekuje na zasób R2.
2. P2 posiada zasób R2 i oczekuje na zasób R1.
3. Powstaje cykliczne oczekiwanie które blokuje dwa procesy.

---

### Metody Ochrony przed Wzajemną Blokadą:

1. Zapobieganie:
	1. Wzajemne wykluczenie: Używaj dzielonych zasobów jeśli to możliwe (np. Pliki tylko do odczytu).
	2. Przetrzymywanie i oczekiwanie: Procesy muszą zamawiać, wszystkie zasoby na początku swojego działania. Przed żądaniem kolejnego zasobu, proces musi zwolnić aktualnie zajmowane zasoby.
	3. Brak Wywłaszczenia: W przypadku braku dostępnego zasobu, system może odebrać przydzielone zasoby i oddać je innemu procesowi.
	4. Cykliczne Oczekiwanie: Wprowadzenie porządku globalnego dla zasobów (np. Numerowanie zasobów) i wymuszenie żądań w kolejności.

2. Unikanie:
	1. Stan Bezpieczny:  System jest w stanie bezpiecznym, jeśli może zakończyć wszystkie procesy przy odpowiednim przydziale zasobów.
	2. Algorytm bankiera: Procesy deklarują liczbę zasobów, które mogą być im potrzebne. Zasoby są przydzielane tylko wtedy, gdy system pozostaje w stanie bezpiecznym.
	3. Wykrywanie i wychodzenie:
		1. Wykrywanie Zakleszczeń: Używanie grafów przydziału do identyfikacji cykli.   Wierzchołki to procesy i zasoby, krawędzie to natomiast żądania i przydziały. Jeśli graf zawiera cykl, może występować zakleszczenie.
		2. Wychodzenie z Zakleszczeń: Przerywanie działania procesów w cyklu (np. Zabicie jednego z procesów), lub wywłaszczenie zasobów i przydzielenie ich innemu procesowi.