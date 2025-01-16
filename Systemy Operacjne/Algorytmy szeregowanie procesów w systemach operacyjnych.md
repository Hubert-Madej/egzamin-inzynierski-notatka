Szeregowanie procesów jest jednym z kluczowych zadań systemu operacyjnego. Polega na zarządzaniu kolejnością, w której procesy otrzymują dostęp do procesora lub innych zasobów systemowych. Efektywne szeregowanie pozwala maksymalnie wykorzystać dostępne zasoby, zapewniając jednocześnie sprawiedliwy podział czasu procesora między procesy oraz minimalizując czas oczekiwania, wykonania i inne parametry wydajności systemu.

### **Cele szeregowania**
Algorytmy szeregowania procesów w systemach operacyjnych mają na celu osiągnięcie kilku kluczowych celów:

1. **Sprawiedliwość** – każdy proces powinien otrzymać dostęp do procesora.
2. **Efektywne wykorzystanie procesora** – maksymalne wykorzystanie czasu procesora.
3. **Minimalizacja opóźnień** – skrócenie czasu oczekiwania procesów na wykonanie.
4. **Zapewnienie interaktywności** – szybkie reagowanie na interakcje użytkownika w systemach interaktywnych.
5. **Priorytetyzacja** – obsługa ważniejszych procesów w pierwszej kolejności.

### **Typy szeregowania**
Szeregowanie procesów można podzielić na trzy główne typy:

1. **Szeregowanie długoterminowe (long-term scheduling)**:
    - Decyduje, które procesy zostaną załadowane do pamięci głównej.
    - Kontroluje stopień wielozadaniowości systemu.
2. **Szeregowanie średnioterminowe (medium-term scheduling)**:
    - Zarządza procesami w pamięci, czasowo usuwając je (swap-out) lub przywracając (swap-in).
3. **Szeregowanie krótkoterminowe (short-term scheduling)**:
    - Decyduje, który proces otrzyma procesor w danym momencie.
    - Działa bardzo szybko, często w czasie rzędu milisekund.

### **Algorytmy szeregowania**
#### **1. First-Come, First-Served (FCFS)**
- **Opis**: Procesy są obsługiwane w kolejności, w jakiej przychodzą.
- **Zalety**: Łatwy do zaimplementowania.
- **Wady**:
    - Może prowadzić do efektu _konwoju_ – długie procesy blokują krótkie.
    - Brak sprawiedliwości w przypadku procesów interaktywnych.

**Przykład**: Procesy: P1 (czas wykonania: 5), P2 (czas wykonania: 3), P3 (czas wykonania: 2).  
Kolejność obsługi: P1 → P2 → P3.

#### **2. Shortest Job Next (SJN)**
- **Opis**: Najpierw obsługiwane są procesy o najkrótszym czasie wykonania.
- **Zalety**:
    - Minimalizuje średni czas oczekiwania.
- **Wady**:
    - Wymaga znajomości czasu wykonania procesów (trudne do przewidzenia).
    - Może prowadzić do problemu głodzenia (procesy długie są pomijane).

**Przykład**: Procesy: P1 (czas wykonania: 5), P2 (czas wykonania: 3), P3 (czas wykonania: 2).  
Kolejność obsługi: P3 → P2 → P1.

#### **3. Round Robin (RR)**
- **Opis**: Każdy proces otrzymuje równą ilość czasu procesora (_kwant czasu_). Po jego upływie proces jest przesuwany na koniec kolejki, jeśli nie został ukończony.
- **Zalety**:
    - Zapewnia sprawiedliwość.
    - Dobre dla systemów interaktywnych.
- **Wady**:
    - Zbyt krótki kwant czasu powoduje nadmierny narzut kontekstowy.
    - Zbyt długi kwant czasu pogarsza responsywność systemu.

**Przykład**: Procesy: P1 (czas wykonania: 5), P2 (czas wykonania: 3), P3 (czas wykonania: 2).  
Kwant czasu: 2.  
Kolejność obsługi: P1 (2), P2 (2), P3 (2), P1 (2), P2 (1).

#### **4. Priority Scheduling**
- **Opis**: Procesy są obsługiwane na podstawie ich priorytetów.
- **Zalety**:
    - Umożliwia obsługę ważniejszych procesów w pierwszej kolejności.
- **Wady**:
    - Może prowadzić do problemu głodzenia procesów o niskim priorytecie.
    - Wymaga mechanizmów dynamicznej zmiany priorytetów, aby zapobiec głodzeniu.

**Przykład**: Procesy: P1 (priorytet: 2), P2 (priorytet: 1), P3 (priorytet: 3).  
Kolejność obsługi: P2 → P1 → P3.

#### **5. Multilevel Queue Scheduling**
- **Opis**: Procesy są podzielone na różne kolejki w zależności od ich priorytetu lub typu (np. procesy systemowe, interaktywne, wsadowe). Każda kolejka może używać innego algorytmu szeregowania.
- **Zalety**:
    - Dobrze radzi sobie z różnorodnymi typami procesów.
- **Wady**:
    - Statyczne przypisanie kolejek może prowadzić do problemów z głodzeniem.

**Przykład**:
- Kolejka 1 (procesy interaktywne): Round Robin.
- Kolejka 2 (procesy wsadowe): FCFS.

#### **6. Multilevel Feedback Queue**

- **Opis**: Procesy mogą przemieszczać się między kolejkami w zależności od swojego zachowania i potrzeb (np. procesy intensywnie korzystające z procesora mogą być przesuwane do niższych kolejek).
- **Zalety**:
    - Dynamiczne dostosowanie do potrzeb procesów.
    - Łączy zalety wielu algorytmów.
- **Wady**:
    - Skomplikowana implementacja.

**Przykład**:

- Procesy początkowo trafiają do kolejki o najwyższym priorytecie (krótki kwant czasu).
- Jeśli nie ukończą się w swoim czasie, są przesuwane do niższej kolejki.


### **Wskaźniki wydajności algorytmów szeregowania**

1. **Czas oczekiwania** – średni czas, jaki proces czeka na rozpoczęcie wykonywania.
2. **Czas wykonania** – całkowity czas od momentu zgłoszenia procesu do jego zakończenia.
3. **Przepustowość (throughput)** – liczba procesów wykonanych w jednostce czasu.
4. **Czas odpowiedzi** – czas od zgłoszenia procesu do pierwszej odpowiedzi.