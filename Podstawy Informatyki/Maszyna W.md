Budowa Maszyny W [[1]](https://minut.polsl.pl/articles/C-19-004.pdf) [[2]](https://minut.polsl.pl/articles/C-20-007.pdf)

Maszyna W to uproszczony model komputera oparty na architekturze von Neumanna, zaprojektowany w latach 70. XX wieku na Politechnice Śląskiej. Jest to narzędzie dydaktyczne pozwalające zrozumieć podstawowe zasady działania komputerów.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcoftYobi3TCR2RccGOxtxr65wII9RV9vHT2iH7Wd_-F29-OCJ8k34RaJa7DfySfAkE6FOKuwbrMYA8MmKiUZfdNQlJiG6XKUu0Aq1PIFoLR7pUH48lWiBePl8lCh-MyRVxHBroYA?key=LhzamKR2PARjwTU86rGUktuQ)

# Kluczowe elementy:
1. Pamięć operacyjna (PaO):
	- Przechowuje program (instrukcje) oraz dane.
	- Składa się z komórek pamięci identyfikowanych za pomocą adresów.    
	- Operacje na pamięci wymagają podania adresu komórki.

2. Jednostka arytmetyczno-logiczna (JAL):
	- Wykonuje podstawowe operacje arytmetyczne (np. dodawanie, odejmowanie) oraz logiczne (np. AND, OR).
	- Posiada:
		- Akumulator (Ak): przechowuje wyniki operacji.
		- Bit znaku (Z): informuje o wyniku operacji (np. czy liczba jest ujemna).

3. Układ sterujący:
	- Składa się z:
		- Rejestru instrukcji (I): przechowuje bieżący rozkaz.
		- Licznika rozkazów (L): przechowuje adres kolejnego rozkazu.
		- Odpowiada za sterowanie przepływem danych oraz aktywowanie odpowiednich sygnałów sterujących.

4. Magistrale:
	- Magistrala danych: przesyła dane między komponentami.
	- Magistrala adresowa: przesyła adresy komórek pamięci.

---

Sygnały sterujące:
	- Impulsowe: krótkie sygnały aktywowane na końcu taktu zegarowego, np. **wea**, **weak**.
	- Poziomowe: aktywne przez cały takt zegarowy, np. **wys**, **czyt**.

---

# Sposób działania

Maszyna W działa w cyklu "pobierz, dekoduj, wykonaj":

1. Pobierz:
	- Instrukcja jest pobierana z pamięci operacyjnej (adres wskazany przez licznik rozkazów L) i zapisywana w rejestrze instrukcji I.

2. Dekoduj:
	- Kod rozkazu (z rejestru I) jest interpretowany.
	- Określana jest operacja do wykonania i argumenty (np. adres komórki pamięci).

3. Wykonaj:
	- Wykonywana jest właściwa operacja (np. dodawanie, zapis do pamięci, skok warunkowy).
	- Wynik operacji może być zapisany w akumulatorze lub pamięci.

---

# Programowanie Maszyny W

Programowanie Maszyny W polega na definiowaniu rozkazów i ich realizacji w postaci sekwencji sygnałów sterujących.

### Przykład rozkazu: Dodawanie

Rozkaz: (Ak)+((Ad))→Ak  
  
Opis:
1. Pobranie rozkazu:
- Rozkaz jest pobierany z pamięci i zapisywany w rejestrze I.
- Licznik rozkazów L jest inkrementowany.

2. Przygotowanie operandu:
- Adres komórki z operatorem (z rejestru Ad) jest wpisywany do rejestru adresowego A.
- Wartość z tej komórki jest odczytywana i przesyłana do JAL.

3. Wykonanie operacji:
- Zawartość akumulatora Ak jest dodawana do wartości z JAL.
- Wynik operacji jest zapisany w Ak.

Fazy rozkazu:
1. Pobranie rozkazu: czyt, wys, wei, il
2. Przygotowanie operandu: wyad, wea
3. Wykonanie dodawania: czyt, wys, weja, dod, weak, wyl, wea

### Przykłady instrukcji

1. Dodanie wartości z pamięci do akumulatora:
	- Symbolicznie: (Ak)+((Ad))→Ak
	- Fazy:
		1. Pobranie instrukcji.
		2. Przygotowanie wartości z pamięci.
		3. Dodanie wartości do akumulatora.

2. Zapis akumulatora do pamięci:
- Symbolicznie: (Ak)→((Ad))
- Fazy:
	1. Pobranie instrukcji.
	2. Wpisanie wartości z akumulatora do rejestru słowa pamięci SSS.
	3. Zapis wartości z SSS do komórki pamięci.

3. Skok warunkowy:
- Symbolicznie: Jeśli Z=1, to (Ad)→L
- Fazy:
	1. Pobranie instrukcji.
	2. Sprawdzenie warunku (wartości bitu Z).
	3. Ustawienie nowego adresu w liczniku rozkazów.

  
Kluczowe właściwości Maszyny W
- Architektura von Neumanna: program i dane znajdują się w jednej pamięci.
- Prostota: Maszyna W jest uproszczonym modelem komputera, idealnym do celów dydaktycznych.
- Reprezentacja liczb: Maszyna korzysta z systemu binarnego (np. kod uzupełnieniowy do 2n2^n2n).
- Elastyczność: Możliwość projektowania nowych rozkazów i ich realizacji.