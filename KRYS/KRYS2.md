# KRYS 2 - szyfry strumieniowe

bit po bicie, nie jest to podzielone na paczki 8 bitowe

a blokowy to po 8 bitów spaczkowany

strumieniowe - tańsze, łatwiej je obliczyć, aczkolwiek blokowe dzisiaj też są w miare tanie

strumieniowe przeważają tam gdzie mamy limitowane miejsce, telefony np. 

w internecie blokowe win



xi = wiadomość szyfrowana i=0,...

yi = wiadomość zaszyfrowana

si = klucz (strumień klucza) - powinien być losowy bez regularności

yi = xi XOR si

XOR - modulo 2

![image-20221011182308208](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011182308208.png)

Całe sedno leży w tym, skąd wziąć si.

## One time pad

szyfr strumieniowy, taki że:

- strumień klucza jest generowany przez generator liczb losowych
- strumień klucza znany jest tylko uprawnionym stronom.  (Alice i Bob)
- każdy bit si jest użyty tylko raz ==> si ma taką długość jak wiadomość szyfrowana

Nie można go złamać. Nawet jeśli odczytam połowę wiadomości, to to nic nie powie nam o drugiej połowie. Nie da się znaleźć żadnej poszlaki, bo każdy bit klucza jest losowany, więc nic oprócz zgadywania nie mamy.



Wady:

1. Cięzko mieć taki generator
2. Jak już umiemy przesłać klucz bezpiecznie, to po co nam byłby szyfr?
3. 1Mb wiadomości wymaga dosłania 1Mb klucza

Generator licz losowych - wynik jest zjawiskiem losowym, czyli p-stwo zgadnięcia wyniku idzie do zera wraz z rozmiarem wyjścia (np. rzut monetą).

![image-20221011183233614](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011183233614.png)

**Kryptosystem jest bezwarunkowo bezpieczny** (teorio-informacyjno bezpieczny) jeśli nie może być złamany przy założeniu dowolnie dużej mocy obliczniowej. 

> Możemy mieć dowolnie dużą liczbę komputerów i to i tak będzie zbyt mało żeby złamać szyfr to wtedy jest bezpieczny.

OTP jest bezwarunkowo bezpieczny.

bo

możemy ustalić przestrzeń klucza i dać komputerom każdą kombinajce klucza i niech każdy obliczy czy to co wyjdzie ma sens.

Ale tutaj przestrzeń klucza jest nieskończona, zawsze można wziąć dłuższy, więc nie da się wziąć tyle komputerów ile jest możliwych kluczy i potem na jednym dojdzie do złamania

Mało który szyfr jest bezwarunkowo bezpieczny, a jak już jest to ma takie fatalne wady jak OTP.

**Kyptosysmte jest obliczeniowo bezpieczny** jeśli najlepszy znany nam algorytm go łamiący wymaga co najmniej T operacji.

Możemy powiedzieć że szyfr jest bezpieczny na poziomie T operacji np.500

Wada tej defki to "najlepszy nam znany" - nie wiem tak naprawdę, ktoś mógł złamać i się nie przyznać.

***

Upraktycznijmy nasz OTP

![image-20221011184326851](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011184326851.png)

Problematyczny jest ten generator prawdziwcyh liczb (aczkolwiek podobno USA-Rosja podcza Cold War używali tego między sobą).

Dlatego żeby to ulepszyć to zróbmy tańszy i łatwiejszy generator.

**Generator liczb pseudolosowych** - fcja generująca ciąg zero-jedynkowy na podstawie wejścia (seed). 

np: 

```
s0 = seed // seed to nie jest 1 bit, to ciąg bitów (blok)
si+1 = f(si) // ale si to już tylko jeden bit
lub
si+1 = f(si,si-1, si-2, ...., si-k)
```

Przykład:

Funkcja Random w ANSI C.

```
s0 = 12345
si+1 = 1103515245si+12345 mod 2^31
```

działa to na takiej zasadzie że możne dwie duże liczby a później biorę małą resztę z dzielenie to to przypomina losowe, a w dodatku te liczby są tak dobrane, żeby to nie było regularne.

Random z ANSI C nie jest stosowana w kryptografii, bo po kilku wiadomościach Oskar może łatwo zgadnąć seed.

A skąd inąd jest to bardzo dobra funkcja w innych zastosowaniach: próbkowanie, Monte Carlo

**CSPRNG** - Crypto Secure Pseudo Random Number Generator - generator taki, że nie można obliczyć `si+1` z p-stwem > 50 % na podstawie `si, si-1, ... , si-n`. Parametr defki, im większe jest `n` tym większego bezpieczeństwa wymagamy.

powiedzmy że mamy:

```
s0=seed si+1 = Asi +  mod m si,A,B, należą do {0,....m-1}
```

na czym polega generator?

A i B definiuje funkcje, która si+1 daje ciąg zadanej długości

A,B mają po 100 bitów

Zgadnięcie 2^100 i 2^100 to obliczniowo się nie da,

Ale przypuśćmy, że Oskar zna 300 bitów tekstu jawnego x1,....x300 - ofc. zna też y1, ..... y300

to wtedy potrafi wyliczyć S1 = s1,....s100, S2=s101,....s200, S3 = s201, s300.

Jak? No robi XOR na x'ach i y'ach.

No i teraz sobie układa równanie.

S2 = A*S1+B mod m

S3 = A*S2+B mod m

Który da się rozwiązać

A=(S2-S3)/S1-S2) mod m

B = S2 - (S1(S2-S3))/(S1-S2) mod m

jeśli NWD(S1-S2,m) != 1

**Wniosek?**

Taki generator liczb pseudolosowych nie jest bezpieczny. Znaczy ok, jak dobrze dobierzemy A i B i m to strumień klucza będzie dużo większy od klucza i dzięki temu mamy dużo krótszy klucz do przekazania co jest dobre :D

I w tym celu często się używa

Shift Register Based Stream Cipher, a ogólniej Linear Feedback Shift Register Stream Cypher ---> LFSR

![image-20221011190512026](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011190512026.png)

Mamy stan początkowy s2,s1,s0 = 1 0 0 i za każdym cykiem zegara idziemy według strzałek

![image-20221011190819263](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011190819263.png)

Co jest tu fajnie?

Ze ten układzik dostając 3 bity wygenerował 7 róznych kombinacji ułożenia 3 bitów bez żadnej powtórki. I to jest fajne bo robi dobrą pseudolosowość.

Potem analozujemy drugi rozbudowańszy ujładzik.

![image-20221011191236142](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011191236142.png)

No i cyk mamy takie twierdzenie

![image-20221011191257783](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011191257783.png)

Klucz o długość tylko `m` potrafi zbudowac tak ogromny strumień klucza i to jest super.

Przykład 4 pudełeczka generuje ciąg 2^4-1 = 15 Czyli 15 bez zapętleń.

**Atak na LFSR**

klucz (`pm-1,......p0`)

Zakładamy, że Oskar zna:

- `x0,.....xm-1`
- `m`
- `y0,......ym-1`

Co robi? Wylicza `si = xi+yi` 

![image-20221011191909288](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011191909288.png)

I ten układ jest oznaczony i Oskar da rade go rozwiąząć (równania są niezależne).

![image-20221011191958285](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011191958285.png)

Jaki z tego morał?

Bezpiecznie możemy przesłać tylko wiadomość tej długości co jest klucz.

No ale to still jest fajne bo jak sobie połączymy coś tam to zwiększymy bezpieczeństwo i jest taki do fajny algorytm TRIVIUM.

**TRIVIUM**

2^98 operacji wymaga to, a 2^80 uważa się za bezpieczne

![image-20221011192439036](/home/ejek/snap/typora/68/.config/Typora/typora-user-images/image-20221011192439036.png)

> Uzyte bramki to XOR i AND

To nie jest liniowe, bo jest AND czyli mnożenie i to burzy cały ten, mamy gigantycny układ równań ale one nie są liniowe i tego nie da się rozwiązać tak łatwo jak przed chwilą. Więc te ANDy gwarantują bezpieczeństwo.

Po drugie nie ma tych kabli tak wcale dużo więc tanie to jest.

Ogólnie to kryptografia jest balansem między bezpieczeństwem a szybkością. Tak jak zamykamy drzwi jednym kluczem a nie na 3 zamki,

To od jakich wartości na każdym bicie zaczniemy to jest `klucz`.

Używanie trivium jest skomplikowane bo mamy 3 fazy:

- Inicjalizacja -
  -  na pierwszych 80 bitach A wpisujemy wektor startowy (nie musi być tajny ale musi być losowy) 	Number Used Once, Non-Sense 
  - na pierwszych 80 bitach B wpisujemy klucz
- robimy dużo iteracji i dopiero po 1000którymś bicie bierzemy OUTPUT.

O trivium są dwie fajne sprawy:

- Możemy podać wektor inicjalizujący publicznie bo on i tak zostanie zaszyfrowany z kluczem i potem nie sposób się połapać jaki miał udział w bicie.

- Bardzo dobrze chowa jakąkolwiek regularność, bo w szyfrowaniu najważniejsze jest to, żeby po zaszyfrowaniu wyglądało to jak najbardziej losowe
- najważniejsze jest to żeby ten NONS (wektor startowy) się nie powtarzał

## Podsumowanie

strumieniowe - blokowe

OTP i ta teoria z nim związana

generatory liczb losowych (jedne są ok, a trivium jest sztos)