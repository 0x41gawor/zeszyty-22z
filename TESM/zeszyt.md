# 5G Recall

## Overview

![](img/1.png)

Architektura jest jaka jest i co tu dużo mówić. Warto jedynie zauważyć, że można podłączyć się do Core za pomocą Wi-Fi, czyli używać swojego modemu w domu jako stacji bazowej. 

> Są też pomysły, żeby modemy Wi-Fi osób prywatnych były używane przez przechodniów znajdujących się w pobliżu dla zwiększenia pokrycia. Podobno PLUS kupił w tym celu UPC (dostawca Internetu domowego).

## Spectrum

**Pasmo licencjonowane** - to za którego używanie się płaci, a za używanie bez licencji płaci kary. Jak już się zapłaci to można w nim emitować z dużą mocą. Na licencjonowanym jest TV, Radio, Mobile.

**Pasmo nielicencjonowane** - to za którego używanie się nie płaci, ale można w nim emitować tylko z małą mocą. Przykład: Bluetooth, Wi-Fi, IoT

**Technology neutral spectrym licences** - licencja, która nie wymusza używana pasma tylko w konkretnej technologii. Kiedy operator kupi dane pasmo, może go używa jak chce. These licences allow existing bands (which are used for old technologies) to be easily refarmed for 5G.

5G ma zapewnić widespread coverage oraz 5G use cases (eMBB, uRLLC, mMTC). W tym celu zdefiniowano **3 key frequency ranges**:

- Sub-1 GHz
- 1-6 GHz
- above 6GHz

Pasmo licencjonowane powinno grać pierwsze skrzypce, a nielicencjonowane can play a complementary role.

### Sub-1 GHz

600-850MHz

Slower speeds (50-250Mb/s) compared to the mid and high band, but provides a superior range.

Long-distance transmissions and rural areas lacking infrastructure will benefit from Sub-1 GHz 5G access

> 800MHz będzie so nadawania poza miastem (duży zasięg trzeba) w Polsce się nie da na 700MHz bo interfercja z Rosyjskim i Białoruskim wojskiem

### 1-6 GHz

2.1-4.2GHz

Balance both speed (100-900Mb/s) and distance, making it suitable for towns, small cities, and suburban areas.

Will be the most popular across enterprises due to its flexibility and availability* for private spectrum use.

> *Czyli skrawek tego pasma może zostać nielicencjonowany.
>
> 3.4 - 3.8 GHz C-band 
> będzie aukcja 5 bloków po 80MHz
> Pokrycie miejskie
>
> 2.1 GHz Polkomtel ma na tym 5G, reszta nie ma 5G

### above 6 GHz

24-39GHz (mmWave)

Speeds  are the fastest (up to 3Gb/s. The trade-off is that the range is limited—about 500m from the small cell tower. Brak penetracji przez obiekty.

### LTE vs 5G

5G shares frequency space with LTE. It can be used to allocate bands for both LTE-and 5G-use dynamically. Network operators can use FDD and TDD to share frequencies between the two technologies without causing interference.

> EMF - pole EM jest niejonizujące powyżej 10MHz, słońce to te same f co 5G i słońce kurwa jest potężne
> Promieniowanie nie wiemy jak długofalowo stałe działa na człowieka ale z drugiej strony to ludzie żyją coraz dłużej a telco już jest od dawna. Ofc też te fy nagrzewają np. tel jak pogadamy dłużej to telefon jest cieplutki co nie
> Ludzie głupi uciekają od anteny a to od telefonu trzeba się chronić bo on promieniuje blisko. Telefon też im dalej jest od anteny to tym z większą mocą promieniuje więc więcej anten to dla zdrowia lepiej.

## Scenarios

![](img/2.png)

![](img/3.png)

![](img/4.png)

### mMTC

- wąskie pasmo
- ogromna ilość urządzeń IoT
- requirements for energy savings
- high requirements of computing resources (long-time connections)

Czyli po prostu IoT a na nim postawione smart cities.

## 5GS Architecture

![](img/5.png)

Warto zauważyć:

- Rozdzielenie Core Network vs Radio Access Network
- Rozdzieleine control i user plane zgodnie z CUPS

Że fizycznie to wygląda tak:

- DU + CU + transport + local site + transport + regional site + transport + national site, ale o co tu chodzi mu to ja nie wiem 

## RAN Innovations

**MIMO** - Multiple Inputs Multiple Outputs - metoda, dzięki której zwiększa się capacity łącza radiowego. Jak? Używa się wiele anten nadawczych i odbiorczych, aby jak najlepiej wykorzystać zjawisko **multipath propagation**.

**multipath propagation** - zjawisko, że sygnał radiowy dochodzi do anteny odbiorczej wieloma drogami (bo się odbija itp.)

Obecnie MIMO nazywa się konkretną technikę, warto zaznaczyć, że to jednak OFDM użyta do kodowania kanałów fizycznych jest odpowiedzialna za większy data capacity. MIMO to co innego niż beaforming i sptiala diversity. 5G używa OFDM tak jak 4G.

Proszę sobie [to przeczytać](https://www.avnet.com/wps/portal/abacus/solutions/markets/communications/5g-solutions/understanding-massive-mimo-technology/).

Technological Innovations in 5G New Radio:

- **Massive MIMO (with beamforming)** - wydajność pasma wzrost od 2 do 5x
- Multi-Technology include 10GHz+ - radio wspiera wiele use case'ów (stąd 3 pasma) w tym jedno o naprawdę potężnych bitrates
- **New multi-carrier radio transmission**: Filter-Bank Multi-Carrier, Universal Filtered Multi-Carrier, Generalized Frequency-Division Multiplexing, FBMC, UFMC, GFDM - nowe techniki w transmisji multi carrier (wiele fal nośnych), gdzie usprawniono synchronizacje i jest jej mniej a co za tym idzie poprawiono latency w uplink
- Non-Orthogonal Multiple Access and Sparse Coded Multiple Access (NOMA and SCMA) - te techniki wprowadzono aby avoid extensive signaling, a co za tym idzie mamy lower delay w URLLC.  NOMA complements OMA, ma większa interferencje, ale jest ona redukowana dzięki beamformingowi (power differences). NOMA jednak jeszcze nia ma w 5G, będzie w 6G.
- **Shared Spectrum Access** - dostęp do pasma współdzielony i z priorytetami przez kilka grup
  - primary - np. rząd policja jak jest powódź wtedy one dostają większe pasmo
  - secondary - licencjonowane pasmo dla operatorów
  - tertiary (trzeciorzędne) - nielicenjonowane pasmo - dla private campus networks
- **Advanced Inter-Node coordination thanks to cloud RAN**. CU jest w cloudzie więc może fajnie zarządzać DU, ktore jest przy gNodeB'ach, a co za tym idzie jeden user (CU go widzi) może być obsługiwany przez kilka gNodeB --> much higher bandwidth, gdy UE ma kiepskie zasieg z jednej.
- Simultaneous Transmission Reception in low-power transmission (small cells)
- **Device to Device communication** - it is network controlled especially for licensed bandwidth
- **Flexbile Networks** - thanks to NFV and SDN -> flexibility and reduction of time-to-deployment, to daje też nowe use-case'y biznesowe - warto się zakręcić wokół sieci komórkowych
- **Backhaul/Fronthaul and integration of backhaul/radio access** - fronthaul (UE-Antena), Backhaul (Antena-Core) //TODO
- **Flexible duplex** - jak operator ma w danym cell zwykłe warunki ruchu klienckiego to używa FDD, a jak nagle się zrobi dużo pasma dostępne (bo mało ludzi) to może się przełączyć na TDD (sloty czasowe zrekompensują (w sensie na minus) szersze pasmo).

> Flexible duplex.  FDD - wysyłam i odbieram na różnych częstotliwościach, TDD - odstępy czasowe time sloty na uplink i downlink, TDD jest lepiej kiedy mamy duży throughput Technologicznie możliwe, prawnie nie bo UKE decyduje jaka jest duplex na daną `f` mimo, że antena potrafi sobie zmieniać.
>
> > (UKE patrzy po prostu ile vendorów na danej f ma co --> antymonopol np. Nokie nie ma FDD na jakiejśtam)

## CN Innovations

Z racji wirtualizacji:

- On-demand deployment of service anchors
- Flexbile orchestration of Network Functions
- Shorter period of service deployment

Z racji nie wiem czego:

- Complex networks incorporating multiple services, standards and site types
- Coordination of multi-connectivity technologies

> VM vs kontener w 5G --> wygrywają kontenery

## Deployment scenarios

![](img/6.png)

Jak eNodeB umie gadać z 5GC, to nazywamy go **NG eNodeB** - w Polsce już prawie wszystkie stacje bazowe 4G mają te upgrade.

Dual Connectivity - to że telefon umie podłączyć się do dwóch stacji jednocześnie w NSA trzeba z tego korzystać.



Option 1 to czysta sieć 4G.

Option 2 to czysta sieć 5G, nasz cel.

Option 3 to stan obecny wdrożenia 5G.

Option 4,5,7 "we won't see them anytime soon... or at all"

## Standarisation

![](img/7.png)

Generalnie jeśli chodzi o sieci mobline to jest mocna współpraca z państwami ponieważ chcemy, aby były one kompatybilne na całym świecie. W Europie oraz europejskiego interesu w tym wszystkim standardów pilnuje ETSI.

**3GPP** - zrzesza głównie ludzi na codzień pracujących w firmach vendorów. Ci najbliżej sprzętu protokołów. Dlatego ich specyfikacje są bardzo dokładne i techniczne do bólu.

**GSMA** - zrzesza nie tylko vendorów, ale też i operatorów. Bardziej zamiast opisać jak coś dokładnie działa skupiają się na krokach jakie należy podjąć, aby zarządzać siecią mobilną.

**ITU** - brak info

**Open RAN policy coalition**

Hasło przewodnie: "poza 4G,5G moglibyśmy robić coś więcej, żeby mali vendorzy też mogli robić urządzenia 5G"

OpenRAN standaryzuje interfejsy, bo do tej pory jak się kupywalo sprzet to jednego vendora

Za OpenRAN stoi mocno USA, bo oni nie mają swojego vendora w wielkiej piątce, która tworzyła 5G na cały świat

![](img/8.png)

# TESM 3 

## 19

![](A:\Ejek\STUDIA\zeszyty-22z\TESM\img\x.png)



## 20

Release jak się kończy 

na koniec 2023 będzie R-18 czyli 5G advanced

6G dopiero od R-19, ale nauka już pracuje nad 6G

naukowo - pracujemy nad 6G

standardy - pracujemy nad 5G-Advanced



private networks jest dużo kasy w tym

## Ćwiczenia

Telefon budzi się trybie samolotym Polski fon, ale wylądował we Francji

- Antena wysyła informację (broadcast - jeśli ktoś chce do mnie wysyłać a ja go nie znam, to wysyłajcie mi tutaj (f,timeslots))
- Telefon kieruje się tam
- Antena odpowiada dedykowanym kanałem logicznym do synchronizacji
- Telefon wysyła info, że chce się połączyć z core'm swojego operatora 
- gNodeB robi UE interfejs N1 do swojego AMF'a, a v-AMF kieruje do h-AMF (SEPP'em wychodzi i idzie przez IPX) 
- h-AMF dostaje wiadomość (UE zamieszcza SUCI tam), h-AMF przeszukuje UDM dla tego UE
- przygotowuje wiadomość RES zaszyfrowaną kluczem publicznym i wysyłamy userowi
- user rozszfyruje ją kluczem prywatnym
- i jak sieć sprawdzi, że to jest coś co się spodziewał to git
- sieć też wysyła klucz do szyfrowania połączenia na czas tej rejestracji

- dostarczenie kluczy do v-network (v-AMF)
- koniec procedury rejestracji
- v-AMF powiadamia v-RAN odnośnie tego usera daje klucze na te rejestracje i jazdynia

hierarchia kluczów (idzie tylko w dół, z klucza wyższego rangą da się policzyć klucz niższy, ale nie na odwrót)

- Subscriber Key (**K**) - UICC i UDM ma. najbardziej chroniony fest, niestandardowy odczyt niszczy ten klucz

Uwierzytelnieni jest na klucz asymetrycznie

Szyfrowanie wiadomości na jest symetrycznie

AMF i RAN jest tunel TLS (IPsec)

Lawful Interception najczęściej używa Policja, żeby podsłuchiwać rozmowy.

Dopóki UE gada N1 z AMF to to jest NAS, a jak się zwróci do RAN do Access Stratum.

po tym jest ustawienie połączenia RRC między UE i gNodeB (na wypadek pagingu)

jak jest handover to na N1 (NAS) nic się nie dzieje, to wszystko na N2 jest, UE się przełączył, a RAN potem informuje tylko core gdzie

cały czas nie ma sesji w UPF, to wszystko się dzieje w Access Stratum.

Kolos1

1. Jak działa HARQ
2. Omówić standalone oraz non-standalone
3. Do czego służy radio bearer? jakie ma funkcje?

Coś takiego ale na materiał jaki mieliśmy w te kolosy.
