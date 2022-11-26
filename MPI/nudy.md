
# MPI

**co chciałbym zebyście znali**

- M/M/1
  - podstawowy system który ulatwia analize sieci
- system ze stratami M/M/n/n
  - jeśli nie ma wolnych urządzeń obsługujących to pakiet/żądanie/klient zostaje stracony
- M/G/1 rozkład dowolny byle był dla każdego zadania taki sam
- M/G/1 z priorytetami

***

**System M/M/1**

Jaka jest własność że daje najmniejszy czas oczekiwania w systemie? Najpierw obsługuje pakiety krótki a te długie niech czekają, ta metoda daje najlepsze wyniki.

***

**System M/M/1 (2)**

Czyli np. ile klientów jest teraz w systemie. Czyli np. nie ma 0.1 klienta jak jest 1 klient, to potem moze być ich tylko 2 (nie 1.6 czy cos)

Albo że może przyjść naraz tyko jedno zadanie.

W systemie z czasem dyskretnym mamy ściśle określone momenty w których coś się może zdazyć, i tylko w nich może coś się zdarzyć

3) zależy tylko od stane anie od przeszłośći - to nazywamy ze jest **bezpamięciowy**

***

**Model sieci komputerowej**

To jest sieć kaskada przejść przez system M/M/1

Wyliczam wszędzie oddzielnie i potem czas oczekiwania to jest suma

co ja muszę założyć jeśli stosuje coś takiego? Proces napływu jest zgodny z poissonem, no więc wyjście też

Robimy założenie i teraz jakie sa konsekwencje tego założenia? Np. to ze w realu to nie jest poisson.

***

**Zastosowanie systemu M/M/1 do wyliczania ...**

Każdą kaskadę można analizować niezależnie.


Ryszard Sys napisał książkę

## System M/M/1 (4)

### +1

Najprostsza sieć do anala to sieć Jacksona

praktyka odbiega od teorii ale dobre to i tak

Każdy węzeł mogę analizować niezależnie.

## Problem wyznaczenia przepływności łączy (1)

G - to funkcja celu

## System ze stratami M/M/n/n (1)

n klientów co są w systemie jednocześnie mogą być jak przyjdzie kolejny to jest tracony

### System M/G/1

res - residual

