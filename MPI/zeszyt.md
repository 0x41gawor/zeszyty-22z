# Co będzie na kolosie

- [x] Jaki to system **M/D/n/K**?
- [ ] Co to jest **sieć Jakcsona**?
- [ ] Udowodnij, że rozkład wykładniczy jest **rozkładem bezpamięciowym**
- [ ] Wyprowadź zależność na średni czas oczekiwania pakietów obsługiwanych z niższym priorytetem w systemie **M/G/1** z dwoma priorytetami
- [x] Podaj **metryki** opisujące jakość przekazu pakietów przez sieć
- [ ] Wyjaśnij czym charakteryzuje się rozkład **pod wykładniczy i nad wykładniczy**
- [ ] Udowodnij, że strumień wyjściowy w systemie **M/M/1** jest opisany rozkładem Poissona
- [ ] Wyprowadź zależność na średni czas oczekiwania w systemie **M/G/1**

# Blok A

## Co będzie

- **Modelowanie ruchu w sieci Internet**, w tym w sieci *best* *effort* (model ARIMA, GARCH itd.), modelowanie ruchu generowanego przez różne typy aplikacji (wideo, mowa, dane) oraz znaczenie źródła ON/OFF. 

- **Użyteczne modele kolejkowe dla modelowania elementów Internetu**. Modelowanie elementów infrastruktury sieciowej i użyteczne algorytmy. Modelowanie elementów infrastruktury obliczeniowej i użyteczne algorytmy

- **Projektowanie klas usług „od końca do końca” w sieci gwarantującej jakość przekazu** **QoS/QoE** obejmujące metody matematyczne dla algorytmów przyjmowania/odrzucania wywołań, algorytmy szeregowania pakietów w węzłach, monitorowania ruchu, wielokryterialnego ruting między domenowy, …)

## 0. Plan

1. Wprowadzenie do QoS

2. Metryki QoS na poziomie pakietów

3. System obsługi

4. Rozkład Poissona

5. Rozkłady wykładniczy, pod wykładniczy i nad wykładniczy 

6. Inne ważne zależności

7. System z oczekiwaniem M/M/1 
   1. Proces Markowa
   2. Sieci Jacksona

8. System ze stratami M/M/n/n 
   1. Wzór Erlanga

9. System M/G/1

10. System M/G/1 z priorytetami 

## 1. Wprowadzenie do QoS

![](img/2.png)

To co generuje sieć to ocenia/standaryzuje *"Y.1541 : Network performance objectives for IP-based services"*. Z tym, że poziom sieci widzi apka.

To co generuje apka to ocenia/standaryzuje *"ITU G.1010 End-user multimedia QoS categories"*. Z tym że poziom aplikacji "widzi" user.

To co widzi user to ocenia jego rozum, jego subiektywna ocena.

![](img/3.png)

Strumień pakietów jak przejdzie przez sieć to:

- po pierwsze każdy z pakietów przyjdzie z jakimś opóźnieniem - **delay**
- po drugie dla każdego z pakietów wartość tego opóźnienia będzie inna - **delay jitter**
- po trzecie niektóre pakiety mogą się zgubić - **packet loss**
- po czwarte sieć jest w stanie przesłać tylko daną ilość pakietów w danym czasie - **throughput**

## 2. Metryki QoS na poziomie pakietów

### 2.1 IP Packet Transfer Delay (IPTD)

Zalecenie ITU-T Y.1540

**Dla danego pakietu** - jest to czas upływający pomiędzy chwilą wysłania pierwszego bitu a momentem odebrania ostatniego bitu pakietu w mierzonej sieci

Zazwyczaj wyrażane jest jako **parametry statystyczne próby*** 

- minimalne opóźnienie (min IPTD)
- maksymalne opóźnienie (max IPTD)
- średnie opóźnienie (mean IPTD)

*próba - wielokrotnie powtórzony eksperyment "dla danego pakietu"

![](img/4.png)

> Uwagi:
>
> - Min i Max IPTD wynikają z przepływności łączy, wielkości buforów i długości pakietów
>
> - Mean IPTD zależą od przepływności łączy, wielkości buforów, ruchu w sieci i długości pakietów

### 2.2 IP Packet Delay Variation (IPDV)

Zalecenie ITU-T Y.1540

**Dla danego pakietu** jest zdefiniowane jako różnica IPTD tego pakietu i pewnego pakietu, którego IPTD jest traktowane jako punkt odniesienia. Może być zdefiniowane w odniesieniu do IPTD pierwszego pakietu w strumieniu, najmniejszego IPTD w próbie lub średniego IPTD w próbie

**Dla danego zbioru pakietów** to różnica pomiędzy kwantylem rzędu (1-a) rozkładu opóźnienia przekazu pakietów IPTD  `minIPTD` w danym przedziale czasu, np. a=10-3

![](img/5.png)

### 2.3 IP Packet Loss Rate (IPLR)

Zalecenie ITU-T Y.1540

**Dla danego zbioru pakietów** to stosunek liczby pakietów straconych do liczby pakietów wysłanych w danym okresie pomiarowym

Za stracone uznaje się pakiety pomiarowe które nie dotarły do odbiornika przed upływem czasu Tmax (zalecane 3s).

> **Uwaga -** dla niektórych aplikacji, zbyt duże opóźnienie pakietów uważa się za ich stratę

### 2.4 Throughput

Przepłwność

Liczba przesłanych pakietów (od danych długościach) w danej jednostce czasu, liczona na poziomie aplikacji

> czyli liczone są pakiety, które został odebrane przez apke odbiorcy

> Ważne dla przekazu dużych ilości informacji z wykorzystaniem np. protokołu TCP, gdzie istotnym parametrem jest np. gwarancja minimalnej szybkości przekazu

### 2.5 Przykładowe wymagania apek

<img src="img/6.png" style="zoom:75%;" />

## 3 System obsługi

### 3.1 Intro

![](img/7.png)

Klientami mogą być pakiety lub zadania do wykonania przez serwer obsługi

Metody badawcze:

- teoria kolejek
- metody symulacyjne

### 3.2 Klasyfikacja systemów obsługi

Systemy obsługi klasyfikujemy ze względu na opisujące je charakterystki:

- **Napływ klientów do systemu**
  - `a` w notacji Kendall'a
- **Zachowanie klienta w kolejce** 
  - czy będzie cierpliwie czekał, czy będzie rezygnował 
- **Czas obsługi klientów przez serwer**
  - `b` w notacji Kendall'a
- **Kolejność obsługi klientów**
  - czy FIFO, czy dzielenie strumieni na priorytety
- **Ilość serwerów obsługi** 
  - `c` w notacji Kendall'a
- **Pojemność kolejki**
  - `d` w notacji Kendall'a
  - czy kolejka jest nieskonczona, czy skończona 
- **Liczba klientów korzystających z systemu obsługi**
  - //TODO nie czaje jeszcze

### 3.3 Notacja Kendall'a

A/B/n/K/S/X

określają kolejno:

A) Napływ klientów do systemu

B) Czas obsługi klientów przez serwer

n) Ilość serwerów obsługi 

K) Pojemność kolejki (pominięty oznacza kolejkę nieskończoną)

S) Liczba klientów korzystających z systemu obsługi (population size)

X) Queueing discipline 

Jak można je wypełnić?

`A i B`:

- `M` - Markovian -  rozkład czasów między zdarzeniami w Procesie Poissona - rozkład wykładniczy

- `D` - Determinitic - rozkład Stały.

- `G` - General - General. Arbitrary distribution of time intervals (may include correlation).

`n`:

- liczba całkowita

`K`:

- liczba całkowita
- pominąć - wartość nieskończona

`S`:

- liczba całkowita
- pominąć - wartość nieskończona

`X`

- FIFO - First In First Out
- LIFO - Last in First Out
- SIRO - Service in Random Order

Przykłady:

![](img/8.png)

## 4 Proces Poissona

Type of random mathematical object that consists of points randomly located on a mathematical space.

The process has convenient mathematical properties, which has led to its being used as a mathematical model] for seemingly random processes in numerous disciplines: w tym telco.

<img src="img/9.png" style="zoom:150%;" />

A visual depiction of a Poisson point process starting from 0, in which increments occur continuously and independently at rate `λ`.

Czyli kolejne *punkty* pojawiają się losowo, ale średnio co `λ`. Więc jak weźmiemy wygenerujemy 100000 punktów procesem Poissona, to średnia odstępów między nimi wyjdzie `λ`. Mimo, to każdy kolejny odstęp generowany jest niezależnie, tzn. gdy `λ=2` i poprzedni odstęp był `1` to nie ma specjalnego mechanizmu, żeby teraz odstęp był `3`.

Podsumuwujac: a process in which events occur continuously and independently at a constant average rate

## 5 Rozkład wykładniczy

Rozkład prawdopodobieństwa czasów pomiędzy zdarzeniami/punktami w procesie Poissona.

<img src="img/10.png" style="zoom:75%;" />

> Funkcja gęstości p-stwa - aka że całka z tej funkcji, obliczona w odpowiednich granicach, jest równa prawdopodobieństwu wystąpienia danego zdarzenia losowego
>
> Dystrybuanta - funkcja taka, że dla danego parametru `x`, określa p-stwo, ze zmienna losowa dla której jest określona ta dystrybuanta będzie mniejsza od `x`. ===> `F(x) = P(X < x)`

### 5.1 Bezpamięciowość

![](img/11.png)

> Czyli jak idziesz na przystanek gdzie autobusy przybywają zgodnie z rozkładem Poissona o λ = 3 minuty, i czekasz już 2 minuty, to kiedy się spodziewać autobusu? Za minutę? No właśnie nie - rozkład nie ma pamięci, więc nie ma nigdzie zapisane, że już mineły 2 minuty i za minutę powinien dać autobus. Cały czas czas oczekiwania na autobus wynosi 3 minuty. Więc jak już czekasz 2 minuty, to autobusu spodziewaj się za 3 minuty.
>
> Pomogła mi siostra Ania :smile:

#### Dowód

![](img/12.jpg)
