W systemach operacyjnych procesy często współdzielą zasoby, takie jak pliki, pamięć czy urządzenia. Aby zapewnić prawidłowe działanie tych procesów, konieczna jest synchronizacja, czyli koordynacja ich działania w taki sposób, aby uniknąć konfliktów. Synchronizacja procesów zapobiega sytuacjom, w których dwa lub więcej procesów jednocześnie próbują zmodyfikować te same zasoby, co może prowadzić do niespójności danych. Dwa kluczowe aspekty synchronizacji to użycie **semaforów** oraz rozwiązywanie problemu **wzajemnej blokady**.

### **Semafory**
Semafory to mechanizmy synchronizacyjne wprowadzone przez E.W. Dijkstrę. Pozwalają kontrolować dostęp do zasobów współdzielonych przez procesy. Są szczególnie użyteczne w zarządzaniu dostępem do sekcji krytycznych – fragmentów kodu, które nie mogą być wykonywane jednocześnie przez więcej niż jeden proces.

#### **Rodzaje semaforów**
1. **Semafory binarne - [mutex](https://stackoverflow.com/questions/34524/what-is-a-mutex)**:
    - Przyjmują tylko dwie wartości: 0 (zajęty) i 1 (wolny).
    - Stosowane do zapewnienia wzajemnego wykluczania w dostępie do zasobów.
2. **Semafory liczące**:
    - Mogą przyjmować wartości całkowite większe od 1.
    - Umożliwiają kontrolowanie liczby procesów, które mogą jednocześnie uzyskać dostęp do zasobu (np. dostęp do bazy danych z ograniczoną liczbą połączeń).

#### **Operacje na semaforach**
1. **`wait()`** (czasem nazywana `P` – od języka holenderskiego "proberen", czyli "spróbować"):
    - Zmniejsza wartość semafora o 1.
    - Jeśli wartość semafora jest mniejsza od 0, proces zostaje zablokowany, aż zasób stanie się dostępny.
2. **`signal()`** (czasem nazywana `V` – od "verhogen", czyli "zwiększyć"):
    - Zwiększa wartość semafora o 1.
    - Jeśli procesy były zablokowane, jeden z nich zostaje odblokowany.

```cpp
#include <iostream>
#include <thread>
#include <semaphore>

std::binary_semaphore semafor(1); // Inicjalizacja semafora binarnego (1 oznacza wolny zasób)

void sekcja_krytyczna(int id) {
    semafor.acquire(); // wait()
    std::cout << "Proces " << id << " w sekcji krytycznej.\n";
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "Proces " << id << " opuszcza sekcję krytyczną.\n";
    semafor.release(); // signal()
}

int main() {
    std::thread t1(sekcja_krytyczna, 1);
    std::thread t2(sekcja_krytyczna, 2);

    t1.join();
    t2.join();
    return 0;
}
```

Kiedy proces jest odblokowywany w wyniku wywołania funkcji **`signal()`** na semaforze, wybór procesu do odblokowania zależy od implementacji semafora w danym systemie operacyjnym. W większości przypadków stosowane są następujące zasady:
- FIFO (First-In-First-Out)
- Wybór z priorytetami
- Wybór losowy

### **Problem wzajemnej blokady (deadlock)**

Wzajemna blokada (ang. _deadlock_) to sytuacja, w której dwa lub więcej procesów blokują się nawzajem, oczekując na zasoby, które są już przez nie zajęte. W efekcie procesy nie mogą kontynuować swojej pracy, co prowadzi do zatrzymania ich wykonania.

#### **Warunki powstawania wzajemnej blokady**
Według Coffmana wzajemna blokada występuje, gdy spełnione są wszystkie cztery poniższe warunki:
1. **Wzajemne wykluczanie (Mutual Exclusion)**:
    - Co najmniej jeden zasób jest dostępny wyłącznie dla jednego procesu w danym czasie.
2. **Zatrzymanie i oczekiwanie (Hold and Wait)**:
    - Procesy trzymają już przydzielone zasoby i jednocześnie oczekują na kolejne.
3. **Brak wywłaszczenia (No Preemption)**:
    - Raz przydzielony zasób nie może zostać odebrany procesowi – proces musi go zwolnić samodzielnie.
4. **Cykliczne oczekiwanie (Circular Wait)**:
    - Istnieje cykl procesów, w którym każdy proces czeka na zasób, który jest zajęty przez kolejny proces w cyklu.

#### **Przykład wzajemnej blokady**
1. Proces P1 zajmuje zasób R1 i żąda R2.
2. Proces P2 zajmuje zasób R2 i żąda R1.
3. Ani P1, ani P2 nie mogą kontynuować działania, ponieważ każdy czeka na zasób zajęty przez drugiego.

### **Zapobieganie i rozwiązywanie problemu wzajemnej blokady**
1. **Eliminacja jednego z warunków Coffmana**:
    - **Brak wzajemnego wykluczania**:
        - Jeśli zasoby mogą być współdzielone przez procesy bez konfliktów, wzajemna blokada nie wystąpi.
    - **Eliminacja zatrzymania i oczekiwania**:
        - Procesy muszą żądać wszystkich potrzebnych zasobów na początku swojego działania. Jeśli nie są one dostępne, proces czeka, zanim zacznie działać.
    - **Wywłaszczenie zasobów**:
        - Procesy mogą zostać zmuszone do zwolnienia zasobów, jeśli inne procesy ich potrzebują.
    - **Eliminacja cyklicznego oczekiwania**:
        - Zasoby są przydzielane w określonej kolejności, uniemożliwiając powstanie cyklu.
2. **Algorytm Bankiera Dijkstry**:
    - Sprawdza, czy przydzielenie zasobów nie doprowadzi do sytuacji, w której procesy nie mogą zakończyć swojej pracy. Jeśli istnieje ryzyko wzajemnej blokady, przydział jest wstrzymany.

#### **Metody wykrywania i rozwiązywania**
1. **Wykrywanie wzajemnej blokady**:
    - System cyklicznie monitoruje wykorzystanie zasobów i tworzy graf zależności między procesami. Jeśli w grafie pojawi się cykl, wystąpiła wzajemna blokada.
2. **Rozwiązywanie wzajemnej blokady**:
    - **Zakończenie procesów**:
        - Wybór jednego lub więcej procesów w celu ich zakończenia i zwolnienia zajętych zasobów.
    - **Wywłaszczenie zasobów**:
        - Odebranie zasobów zablokowanym procesom i przydzielenie ich innym.

### **Podsumowanie**
Synchronizacja procesów i unikanie problemu wzajemnej blokady to kluczowe aspekty systemów operacyjnych, zapewniające stabilność i efektywność działania. Semafory są podstawowym narzędziem do kontrolowania dostępu do zasobów współdzielonych, podczas gdy wzajemna blokada wymaga bardziej zaawansowanych technik, takich jak algorytmy zapobiegania, wykrywania i rozwiązywania. Zrozumienie tych mechanizmów jest niezbędne dla projektowania wydajnych i niezawodnych systemów operacyjnych.