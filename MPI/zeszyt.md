# Co będzie na kolosie

- [ ] Jaki to system **M/D/n/K**?
- [ ] Co to jest **sieć Jakcsona**?
- [ ] Udowodnij, że rozkład wykładniczy jest **rozkładem bezpamięciowym**
- [ ] Wyprowadź zależność na średni czas oczekiwania pakietów obsługiwanych z niższym priorytetem w systemie **M/G/1** z dwoma priorytetami
- [ ] Podaj **metryki** opisujące jakość przekazu pakietów przez sieć
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

## 2.1 IP Packet Transfer Delay

