Język asemblera to niskopoziomowy język programowania, który umożliwia programowanie w sposób bliski bezpośredniemu działaniu procesora. Głównymi cechami języków asemblerowych jest:

- Symboliczne odwzorowanie instrukcji maszynowych - Każda instrukcja odpowiada jednej instrukcji maszynowej procesora. Instrukcje te są reprezentowane przy pomocy mnemoników (Instrukcji np. ADD, SUB itp. Zastępują one bezpośrednie kody binarne instrukcji ułatwiając proces programowania.).
    
- Adresowanie pamięci: Umożliwia bezpośrednie operacje na adresach pamięci i rejestrach procesora. Stosuje tryby adresowania np. Natychmiastowe, pośredni, względne.
    
- Kontrola Hardware'u: Język asemblera pozwala na kontrolę rejestrów, przerwań, i urządzeń peryferyjnych.

---
### Przykładowy kod w asemblerze:

MOV AX, 5 ; Załaduj liczbę 5 do rejestru AX  
MOV BX, 3 ; Załaduj liczbę 3 do rejestru BX  
ADD AX, BX ; Dodaj zawartość rejestru BX do rejestru AX

---
### Proces Asemblacji:  
  
Asemblacja to proces tłumaczenia kodu napisanego w ASM na kod maszynowy, który może być bezpośrednio wykonywany przez procesor. Poszczególne etapy asemblacji:

1. Analiza Leksykalna i Składniowa - Kod źródłowy jest sprawdzany pod kątem poprawności składniowej i leksykalnej. Mnemoniki, etykiety i symbole są analizowane i rozpoznawane.
    
2. Tworzenie Tablic Symboli - Asembler identyfikuje etykiety (np.punkty skoków) i ich adresy w kodzie maszynowym. Następnie tworzy tablice symboli, która przechowuje adresy zmiennych, etykiet oraz innych elementów.
    
3. Generacja Kodu Maszynowego - Mnemoniki są tłumaczone na odpowiadające im opkody (ang. OPCODE), czyli ciągi binarne reprezentujące instrukcje maszynowe. Adresy są obliczane i wstawiane w odpowiednie miejsca.
    
4. Powstaje plik binarny, lub wykonywalny, który zawiera kod maszynowy.

---

### Proces Generacji Kod Wynikowego:

Kod wynikowy to ciąg binarny, który procesor może bezpośrednio wykonać. Generacja kodu wynikowego polega na zapisaniu opkodów i adresów w formie zrozumiałej dla procesora.  
Struktura kodu binarnego:

1. Nagłówek - Informacja o architekturze procesora, trybie pracy, punktach wejścia programu.
2. Sekcja Kodu - Instrukcje maszynowe przetłumaczone z asemblera.
3. Sekcja Danych - Zdefiniowane w programie dane (np. Zmienne, tablice)
4. Sekcja Symboli - Informacje o etykietach i adresach. Przydatne w procesie debugowania.
    
### Przykład opkodu dla instrukcji z architektury x86:  
  
B8 05 00

B8 - opkod dla instrukcji MOV do rejestru AX

05 00 - wartość zapisana w postaci [malego endianu](https://pl.wikipedia.org/wiki/Kolejno%C5%9B%C4%87_bajt%C3%B3w)

---

### Wady i Zalety języków asemblerowych:

Zalety:
- Wysoka wydajność - Programy napisane w asemblerze są szybkie i zoptymalizowane pod kątem sprzętu.
- Pełna kontrola nad sprzętem - Możliwość sterowania rejestrami, pamięcią i urządzeniami.
- Bezpośredni dostęp do zasobów procesora.

Wady:
- Złożoność - Programy w porównaniu do języków wysokiego poziomu są trudne do napisania i utrzymania.
- Brak Przenośności - Kod asemblera jest specyficzny dla danej architektury procesora.
- Czasochłonność - Proces tworzenia i debugowania programów jest dłuższy niż w językach wysokiego poziomu.

---  
### Przykładowy proces asemblacji

```asm
MOV AX, 5       ; Załaduj wartość 5 do AX

ADD AX, 3       ; Dodaj wartość 3 do AX

INT 21h         ; Wywołaj przerwanie 21h
```

W procesie asemblacji Asembler rozpoznaje instrukcje MOV, ADD i INT. Utworzona zostaje tablica symboli, która zawiera adresy zmiennych i etykiet. Zostaje wygenerowany kod wynikowy:

```
B8 05 00 ; MOV AX, 5

05 03 00 ; ADD AX, 3

CD 21 ; INT 21h
```