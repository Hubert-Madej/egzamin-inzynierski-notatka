M/M/1 - model kolejkowy opisujący system z jednym stanowiskiem obsługi, wykładniczym rozkładem czasu między zgłoszeniami i czasu obsługi, nieograniczoną kolejką oraz regulaminem obsługi FIFO.

M - rozkład wykładniczy czasów między zgłoszeniami.
M - rozkład wykładniczy czasów obsługi.
1 - jedno stanowisko obsługi.

---
### Charakterystyka systemu M/M/1:

1. Źródło zgłoszeń - jako źródło zgłoszeń przyjmujemy nieskończoną liczbę klientów mogących przyjść do systemu. Zgłoszenia przybywają zgodnie z procesem Poissona z intensywnością λ (liczba zgłoszeń na jednostkę czasu).
2. Czas Obsługi - Jeden serwer obsługuje zgłoszenia z intensywnością μ (liczba obsługiwanych zgłoszeń na jednostkę czasu). Czas obsługi jednego klienta jest losowy, opisany rozkładem wykładniczym.
3. Regulamin Kolejki - Klienci ustawiają się w kolejce jeśli serwer jest zajęty, ich obsługa odbywa się w kolejności FIFO.
4. Pojemność Systemu - Kolejka jest nieograniczona, każdy klient, który przyjdzie zostanie dodany do kolejki.

---

Wskaźniki wydajności:
1. Współczynnik obciążenia serwera:  
    ρ = λμ​  
    Warunek stabilności systemu: ρ < 1 (średnia intensywność zgłoszeń musi być mniejsza od intensywności obsługi).  
      
2. Prawdopodobieństwo, że w systemie nie ma zgłoszeń:    
   p0 = 1 - ρ
   
3. Prawdopodobieństwo, że w systemie jest K zgłoszeń (pK):  
    pk=(1 - ρ) pk, gdzie k = 0, 1, 2...  

4. Średnia liczba zgłoszeń w systemie (L):  
      
    L = ρ / (1- ρ)  
      
5. Średnia liczba zgłoszeń w kolejce (Lq):  
      
    Lq=(ρ^2) / (1-ρ)  
      
6. Średni czas przebywania zgłoszenia w systemie (Ts):  
      
    Ts =1 / (μ -λ)
      
7. Średni czas oczekiwania zgłoszenia w kolejce (Tq):  
      
    Tq = ρ / (μ -λ)
  ---
  
#### Zalety i ograniczenia modelu M/M/1:

Zalety:
1. Prosty w analizie i implementacji.
2. Łatwe obliczenia wskaźników wydajności.
3. Znajduje zastosowanie w wielu rzeczywistych systemach.

Ograniczenia:
1. Rozkład wykładniczy może być nienaturalny w niektórych zastosowaniach.
2. Nieograniczona kolejka jest nierealistycznym założeniem w praktyce.
3. Brak priorytetów w obsłudze zgłoszeń.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfe5OVRIgYpFqx5PP3np4FqwUOH0TfNfdPHq1UUvPMkDJfSM_MzKnsbbfvWxLRChiJrAW4Ts5qLrOW4kBTL8RKcbeHf8HCwaZzfXEcEX9Jr8dwUCqUmUlM5ayQlainllumQZPp_?key=LhzamKR2PARjwTU86rGUktuQ)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdze6ntYpQkGvXb3tOajG1DCi1oLXh900NJCd6-8WEoGl1FY4CZ_BcltGOtgnxJylodkdxsd7SoPjYlPtfYf0kGe8fauhsfWsNrV_FfWX8goI_Cy2CGs7OSkAwphZdehzphMBn_gg?key=LhzamKR2PARjwTU86rGUktuQ)