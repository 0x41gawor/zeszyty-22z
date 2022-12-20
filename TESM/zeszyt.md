# 5G Recall

## Overview

![](img/1.png)

Architektura jest jaka jest i co tu dużo mówić. Warto jedynie zauważyć, że można podłączyć się do Core za pomocą Wi-Fi, czyli używać swojego modemu w domu jako stacji bazowej. 

> Są też pomysły, żeby modemy Wi-Fi osób prywatnych były używane przez przechodniów znajdujących się w pobliżu dla zwiększenia pokrycia. Podobno PLUS kupił w tym celu UPC (dostawca Internetu domowego).

## Spectrum

**Pasmo licencjonowane** - to za którego używanie się płaci, a za używanie bez licencji płaci kary. Jak już się zapłaci to można w nim emitować z dużą mocą. Na licencjonowanym jest TV, Radio, Mobile.

**Pasmo nielicencjonowane** - to za którego używanie się nie płaci, ale można w nim emitować tylko z małą mocą. Przykład: Bluetooth, Wi-Fi, IoT.

**Technology neutral spectrum licences** - licencja, która nie wymusza używana pasma tylko w konkretnej technologii. Kiedy operator kupi dane pasmo, może go używa jak chce. These licences allow existing bands (which are used for old technologies) to be easily refarmed for 5G.

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

local site: UPF

regional site: AMF SMF

national site: reszta

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

![](img/9.png)

Na air interface nie musi być szyfrowania w User Plane, i nikt w polsce w LTE nie szyfruje i to jest największa dziura bezpieczeństwa w sieciach moblinych.

# Kolos

Był kolos

# Air Interface

## Intro

Dzisiaj popatrzymy na Air Interface.

Jest to komunikacja między UE a gNodeB.

Należy tu rozróżnić komunikację dwóch typów UE może gadać z gNodeB albo w ramach:

- NAS - Non-Access Stratum. Żeby gadać z core network (gNodeB zapewnia wtedy transparentny interfejs N1). UE <--> AMF
- AS - Access Stratum - Żeby gadać z RAN'em (interfejs N2). UE <--> gNodeB

## Protocol Stack

Jak wygląda protocol stack w 5G?

<img src="img/13.png" style="zoom:150%;" />

My dzisiaj zajmujemy się Access Stratum między UE a gNodeB:

<img src="img/14.png" style="zoom:150%;" />

Skoro widać te wartswy oraz na nich działające protokoły to zdefiniujmy sobie kilka rzeczy.

**Peer to peer communication** - apka na UE działająca w warstwie `n` "gada" z apką w gNodeB działającą w warstwie `n`. Z innymi warstwami nie gadają. To w jakim języku one gadają to określa *protokół danej warstwy*

**Channel, Service Access Point** - apka warstwy `n`, żeby wysłać coś do apki warstwy `n` po drugiej stronie musi swoją wiadomość wsadzić do apki warstwy niższej. Robi to za pomocą *service access point*, wystawiony przez tę warstwę wkładając swoją wiadomość w odpowiedni *channel*, który między tymi warstwami istnieje. 

**Protocol Data Unit** - Jak apka warstwy `n` coś wytworzy do wysłania, to nazywamy to *Procotocl Data Unit*. 

**Service Data Unit** - Jak apka warstwy `n` wyśle swoje PDU przez channel wyśle do apki warstwy `n-1` to wartwa `n-1` dostanie PDU warstwy wyższej i zrobi swoje (ale to już się nazywa SDU), bo ona wykonała usługę jakąś na tym PDU.

### Peer to Peer communication: protocol layer

![](img/10.png)

### Control Plane

#### RRC

**Radio Resource Control** - protocol used in 5G on the Air Interface between UE and gNodeB. Specified in TS 38.331. RRC messages are trasnported via PDCP-messages. The major functions include:

- **connection Establishment and connection Release** (ale jaki connection? RRC connection?)
- **broadcast of system information**
  - np. info synchronizacyjne (ustalanie jak wysylac i co wysylac w jakich slotach czasowych)
  - czy jest standalone czy non-standalone (czy dwa interfejsy radiowe czy nie (dual connectivity)), czy bedziemy używac carrier aggregation
  - czy bedzie szyfrowanie i jakie
- **paging notification**
  - wysyłanie na broadcastowy kanał, "ktoś chce sesje z tą komórką" i UE się odzywa "to ja"
- **radio bearer establishment, reconfiguration and release** (dedykowany bearer dla UE na coś tam)
  -  (service radio bearer SDR i Data radio bearer) (ale to core daje info o QoS Flow w SDAP jakie ma być)
- **RRC connection mobility procedures**
  - zleca robienia pomiarów UE (do handoveru i do lokalizowania UE), zeby wiedziec jaką moc trzeba nadawać (jak UE blizej stacji to mozna zmniejszyc moc)
  - handover and interRAT handover 
  - wie gdzie forwardować NAS

> RRC to serwis point, który kontroluje wszystko co sie dzieje w antenie, jest to punkt kontaktowy z corem, core wysyła na niego komendy jak co robić.
>
> By means of the signalling functions the RRC configures the user and control planes according to the network status and allows for Radio Resource Management strategies to be implemented

The operation of the RRC is guided by a state machine which defines certain specific states that a UE may be present in.  The different states in this state machine have different amounts of radio resources associated with them and these are the resources that the UE may use when it is present in a given specific state.

Stany RRC w jakich może być UE z danym gNodeB:

- `RRC_Idle`- nie ma ustalone jeszcze połączenia RRC (apki RRC nie znają się nawzajem)
  - wszystkie decyzje są po stronie UE
  - RRC idle w antenie ma tylko przekazać coś do core i wtedy core moze zrobić stan RRC_Connected
  - antena w idle robi paging
- `RRC_Connected`
  - jest sesja danych, RRC kontroluje wszystko co sie dzieje z UE, wszystkie decyzje są po jego stronie
- `RRC_Inactive`
  - jeszce nie ma sesji danych, 

### User Plane

#### SDAP

**Service Data Adaptation Protocol** - introduced in 5G. Maps **Qos Flow IDs** to **Radio Bearers**. The SDAP layer is configured by the RRC.

Jak UE rozpocznie *PDU session*, to SMF wymyśli dla niej *Qos Flow ID*, które w 5G jest najmniejszą jednostką, która w core decyduje o jakości przekazu danych. 

> W LTE core zlecał RAN'owi bezpośredno jaki ma zrobić bearer (tym się zajmował protokół PDCP, który w 5G jest nieco copy&paste z 4G). Jedyna więc funkcja SDAP, to mapowanie QoS Flow, które umie core, na Radio Bearer, które umie PDCP. 

Do warstwy SDAP każdy pakiet przychodzi z QoS Flow ID i wszystkie które przyjdą z takim samym beda potraktowane tak samo.

SDAP podejmuje na podstawie QoS Flow ID decyzję:

-  jakiego typu tworzyć Bearer'y:
  - Guaranteed BitRate (GBR)
  - Non-Guaranteed BitRate (Non-GBR)
  - GBR with latency

- Jak ma być transfer w Uplink:
  - negotiated QoS, czy
  - reflective QoS (po 50%)
- Który typ Radio Bearer zrobić:
  - Signalling Radio Bearer:
    - SRB0 - Common RRC Signalling: (`rrc connection request`, `rrc connection setup`, `rrc connection re-establishment request`). Since this radio bearer is used for all the user that's why it is not security and integrity protected.
    - SRB1 - UE dedicated RRC signalling (`rrc connection setup complete`, `rrc connection re-establishment complete`, `rrc connection re-configuration complete`). Once the AS security is activated, all the signalling messages over this bearer will be security and integrity protected.
    - SRB2 - UE dedicated NAS messages such as ` dedicated bearer creation message`
  - Data Radio Bearer:
    - DRB - is established for the transmission of data plane packets. Multiple DRBs can be established for an UE due to different types of services used by UE such as internet browsing, voip call etc. 

Na jedną *PDU session* tworzone jest jedno *SDAP entity*. Czym można je skonfigurować?

- QoS Flow Identifier (QFI)
- Allocation and Retention Priority (ARP)
- Reflective QoS attribute
- Guaranteed Flow Rate + max Flow Rate, Max packet loss
  - to podobne do Token Bucket , i te parametry defniuja ten wiadro
- Notification control from RAN
  - niech medium informuje ze jest np. dużo błędów albo zbyt dużo pakietów w wiadrze i żeby zwolnić tempo, więc tam wyżej SDAP musi wyrzucić jakąś sesję i wtedy SDAP mówi do SMF "niestety, trzeba tę sesję wyrzucić".

> PDCP istnieje w LTE, SDAP nie. Więc funkcjonalność PDCP  jest copy&paste z poprzedniego standardu, więc tam jest bardzo duzo. SDAP robi malutko.

> W 4G nie było, a w 5G jest nacisk na QoS. 4G mniej więcej cały ruch był ten samo - multimedia. Różnica był tylko między voice i multimedia (voice+video), ale to tak naprawdę załatwisz jedną kolejką. Jest niby 9 klas, ale jest 3 używane na głos i 1 na mutlimedia.
>
> Ale w 5G jest sieć która ma tworzyć dużo nowych modeli biznesowych i URLLC, MBB, MMTC, i wgl to już klasi jest mega dużo fest że hej. i Właśnie dlatego się pojawia SDAP

### Plane-independent

#### PDCP

**Packet Data Convergence Protocol** - protocol located on top of the air interface. Provides transport services for RRC (CP) and SDAP (UP) upper layers. Specified in TS 38.323. Functionalities:

- transfer of control/user plane data
  - SDAP wybiera jakość jaka ma być, jest odpowiedzialny za wysoko-poziomowy (najwyżej) transport
- TCP/IP header compression
  - antena ma max 100 userów, więc nie ma sensu wysyłać całego nagłówka TCP/IP. Kompresujemy tylko nagłówki TCP/IP, HTTP (lub inny protokół apki) to dla nas dane więc "nie znamy tego" jako PDCP.
- Sequence numbering;
  - przydant np. w handover
- ciphering;
- integrity protection.
  -  jeśli Oscar zmieni choćby 1 bit w tych danych -> będziemy wiedzieli.
- reply protection
  - do szyfrowania pakietów używany jest nie tylko `kenc` ale też i `seqNum` 
  -  dajemy jeszcze sequence number, i dzieki temu kazdy pakiet jest szyfrowany innym kluczem, zeby nikt inny (kto nie wie jaki jest seq. num. ) nie bedzie wstanianie wysyłać mi ten pakiet, nawet jesli wie ten KLUCZ (**K**)

- PDCP PDU discards xd Jordi łeb ze to napisał 

- PDCP PDU routing in dual connectivity: split/non split (1,2 or 4 RLC entities per PDCP TODO????

  - Dual Connectivity - połączenie UE do dwóch anten na raz.

    Jeśli mamy Dual Connectity ON to robimy splitDRB

    Jeśli potrzebujemy Uplink i Downlink sesje, która to potrzebuje, to będzie mieli 4 RLC per każdy PDCP.

- PCDP PDU for lower latency (SRB0)

- Selection of AM, UM ,TM 

  - Ack Mode - jak w TCP
  - UnAck Mode - jak w UDP
  - Transparent Mode - jak //TODO
  - Czyli czy każemy, żeby RLC potwierdzało każdy RLC message czy nie.

![](img/11.png)

> Zwróć uwagę na nazwę protokołu. 'Convergence - the act of converging and especially moving toward union or uniformity'. Zauważ, że jest to najwyższa warstwa w Plane-Idependent, więc PDCP po prostu daje dla UP i CP usługę wysyłania danych w formie pakietów.

#### RLC

> PDCP decyduje jaki jest sposób przekazu a RLC wykonuje ten sposób
>
> RCL przygotowuje dane do MAC'a

**Radio Link Control**

Functionalities:

- Transfer of upper layer PDUs in one of 3 modes:
  - AM - Ack Mode (ARQ)
  - UM UnAck
  - TM - Transparent
- Reaseembly window for segmentation
  - MAC wysyła dane w chunkach (bo to ostatnia warstwa przed zamianą na sygnał ele), więc to co trzeba mu dać to takie chunki. RLC właśnie musi zrobić te chunki. Chunki mają określony rozmiar np 64. Co jeśli dostaniemy od PDCP dwa pakiety po 20? Trochę głupio je wysyłać w oddzielnych MAC PDU (chunki), bo tracimy ok 70% przestrzeni, więc RLC składa oba te PDCP PDU w jeden pakiet i przekazuje do MAC. To się nazywa **konkatencja** - analogicznie podział PDCP PDU na mniejsze, bo jeden się nie mieści to **segmentacja**. W LTE było i to i to, ale 5G z racji nacisku na latency odrzuca konkatenacje (bo jak dostanie się małe PDCP PDU, to trzeba czekać na następne małe).
- Operacje na RLC header takie jak:
  - Zapisanie bitu `D` lub `C` - Data czy Control, dlaczego to zapisujemy? Bo w segmentacji tracimy info o DRB itp
  - Polling - 1 bit, który mówi czy ma potwierdzać czy ten pakiet przyszedł czy nie (ARQ)
  - Segment offset - ile bitów danych jest z tego segmentu
  - Segment info - czy była segmentacja
  - Segment number - wiadomka

Opis z wikipedii mi się mega podoba https://en.wikipedia.org/wiki/Radio_Link_Control

#### MAC

**Medium Access Control** - ogólnie to to jest protokół kontrolujący the hardware responsible for interaction with the wired, optical or wireless trasmission medium. 

>  MAC decyduje ile bit/s ja wysyłam w powietrzu, ofc przez nagłówek MAC jest to inna wartość niż w RLC.

>  Najważniejsza fucja MAC to kontrolować ile mogę bitów wyssyłać, tak żeby nie zakłócać szczelin czasowych.
>
> MAC ostatnia warstwa przed fizyczną. Zaraz dojdzie do zmiany na sygnał elektryczny :D

Functionalties:

- **Mapowanie kanałów logicznych na transportowe**

  - multiplexing of MAC SDUs from one or different logical channels onto transport blocks (TB) to be delivered to the physical layer on transport channels; 

- **Inbdand monitoring**, 

  - MAC w UE co jakiś czas wysyła info odnośnie moc sygnału, synchronizacja itp.

- **Uplink channel prioritatization** 

  - MAC w UE wysyła jak ważny jest ten pakiet, zeby antena jak nie moze obsluzyc wszystkiego w uplink, to zeby miala priorytety jakieś do decyzji

- **Uplink time alignment** 

  - między antena i UE może byc kilka km, więc droga propagacji już może wpływać na synchronizacje, (światło leci z `c`). Więc antena patrzy jaka jest moc sygnału RSRP i oczacowuje jak daleko UE jest od anteny i UE wtedy wysyła trochę wcześniej niż ma timeslot dany. 

- **HARQ**: MAC ma też swój mechanizm ARQ no bo najwięcej pakietów sie traci w kolejkach do MAC'a, a nie w powietrzu :o 

  - > Bo to tak jest, że własnie kolejka do MAC'a traci najwięcej pakietów, bo dopiero wtedy się okazuje czy medium (powietrze) jest w stanie przesyłać co mu się narzuci 

  - multitasking jest ważny w MAC, bo nie możemy tracić czasu

  - soft combining - jeśli pakiety przyjdzie z błędem ARQ chowa ten pakiet, i potem jak przyjdzie retransmisja ale znowu popsuty pakiet, to możliwe, że na podstawie dwóch możemy zrobić dobry pakiet

  - HARQ jest wszędzie gdzie jest MAC, nie tylko 5G

- Są dwa przypadki zeby uruchomić UL Random Access Procedure

  - handover: wtedy RRC inicjuje RAP mówiąc to do MAC i one otworzą higher layers
  - jeśli do MAC przyjdzie nowy strumień danych, czyli to znaczy, że jest nowa sesja, wtedy sam MAC inicjalizuje procedure RAP
  - Obczaj sobie Contention-Free RA oraz Contention-Based. Based jest używane kiedy Free się nie udaje kilka razy.  
  - Są dwa sposoby na RAP:

    - czytać z System Info że możesz wysyłać w timeslot taki, z taką preamble. I SIB wysyła że wysyłaj w `t+tau`, gdzie `tau` jest od `0 do 100 mikro sekund` i wtedy my losujemy że np. tau=27us



>#### AS UP 11
>
>**RLC**
>
>ile instancji mamy PDCP na instancji RLC jeśli mamy dual connectivity to pakiet PDCP moze iść na dwie RLC (bo moge uzywac dwie f, zeby wysylac to) i to się nazywa split
>
>a split ACknowledge mode to są jeszcze dwie instancje DRB, jedna DL jedna UL żeby dostawać acknowledge pakietów czyli instancji RLC jest 3 (on mówi 4).
>
>"zamyślenie aaa bueno jeszcze jak ten pakiet cccoś tam..."
>
>#### AS UP 9/10
>
>![](img/12.png)
>
>ARP definiuje ile max sesji transport channel (moze ile slotów?)
>
>BER w fiber 10^-11
>
>A w air interface 10^-6-10^-8
>
>Ale BER to nie tylko powietrze ale też ze nie procesujemy wystarczająco szybko tego wiadra, więc mamy dwa błędy medium oraz process

## Warstwa fizyczna

### Ocb z tymi kanałami?

GSM

![](img/16.png)

**Kanał fizyczny TDMA (Time Slot (TS))** - tworzony przez cykliczny ciąg (modulo 7) okienek przypisanych temu kanałowi, przeplecionych z innymi okienkami czasowymi. Czyli na przykład mamy Time Slot tworzony z okienek o numerze 4,

![](img/18.png)

**Kanał logiczny** - przepływ informacji określonego typu w ramach Time Slotu

- realizowany z użyciem określonego podzbioru okienek kanały fizycznego

- określony przez zarezerwowanie określonych okienek (lub sekwencji okienek grupowanych po kilka) w ramach danego Time Slotu

- sekwencja (pozycje) okienek tworzących kanał logiczny musi być znana perz terminal i BTS; może być predefiniowana lub ustalona dynamicznie wg reguł

  - > bo opisano ileś standardów pakowania kanałów logicznych w fizyczne i stacja może powiedzieć do terminala "ej, stosujemy układ nr 7" i terminal wie jakie kanały logiczne jak idą po sobie na jakich kanałach fizycznych

- > np. my mówimy, że grupa czterech kolejnych okienek o numerze 2 powtarzająca się co 20 to jest nasz kanał logiczny, on będzie miał jakąś przepływność tam, co prawda będzie taki szarpany ale to nic

![](img/19.png)

^To coś na rysunku to Burszti nazywa **czekoladka**

Tak było w GSM widać, że w 5G wprowadzili kojeną wartswę abstrakcji czyli kanały transportowe, ale idee łapiemy.

### Podział kanałów w 5G

Są trzy typy kanałów w 5G:

- **logiczne** 
  - Oferowane przez MAC dla RLC
  - Mówią "what is carried"
  - RLC to co ma do wysłania to wkłada w kanały logiczne oferowane przez MAC (MAC wystawia pojemniki a RLC wkłada tam treść, odpowiedniego typu do odpowiedniego pojemnika)
- **transportowe**
  - Oferowane przez PHY dla MAC
  - Mówią "how it is carried"
- **fizyczne**
  - Tutaj jak już PHY dostanie kanały trasnportowe od MAC to mapuje je na fizyczne
  - Mówią "how pack it into timeslots"
  - Potem jak jest transmisja to PHY obserwuje timesloty i patrzy jakie mają one przypisane kanały fizyczne i sprawdza czy ma jakieś bursty do wysłania na danym kanale fizycznym

Ten proces jest ogólny dla UE jak i dla gNodeB.

To co UE wysła do gNodeB to się nazywa Uplink.

To co gNodeB wysyła do UE to się nazywa downlink.

Zauważmy, że to często różniące się rzeczy. Mają część wspólną jak to że zarówno UE jak i gNodeB wysyłają między sobą dane. Ale np. gNodeB rozgłasza informacje systemowe, a UE tego nie robi, gNodeB też robi paging a UE nie, a UE np. budzi się i prosi gNodeB o rejestracja, a gNodeB nie. Dlatego właśnie chłopaki wymyślili te kanały logiczne, transporowe i zrobili podział na Uplink oraz Downlink.

![](img/15.png)

### Kanały logiczne

Pierwszy podział to na User Plane (<u>Traffic channel</u>) i Control Plane (<u>Control channel</u>). 

Drugi podział to na common i gNodeB-specific.

Dobra, jazda:

- gNodeB-specific
  - **BCCH - Broadcast Control Channel** - to tu gNodeB rozgłasza informacje systemowe
  - **PCCH - Paging Control Channel** - to tu gNodeB robi paging

- common
  - **CCCH - Common Control Channel** - kanał control plane ale wspólny dla wszystkich UE, to tu UE np. zgłasza się do gNodeB, ze chce się zarejestrować (robi RRC connection)
  - **DCCH - Dedicated Control Channel** - jak UE i gNodeB wejdą w jakiś bardziej zaawansowany scenariusz sygnalizacyjny to "idą na stronę", czyli na dedykowany kanał sygnalizacyjny tylko dla nich
  - **DTCH - Dedicated Traffic Channel** - kanał do User Plane

### Kanały transportowe

Logiczne stanowiły taki logiczny podział, do czego dany pakiet będzie potrzebny ale tak górnolotnie. Tutaj nadal jest podział do czego dany pakiet będzie potrzebny ale tak warstwę niżej. Zauważ, np. że tu już znika pojęcie control i user plane, ta warstaw nie rozumie tego podziału. 

Tutaj pakujemy pakiety, które mają wspólne cechy "transportowo".

Niektóre da się zawezić inne rzeczy nie da się. Takie coś jak broadcast info systemowe czy paging to musi mieć zapewniony byt, więc nie wclicza się do współdzielonej puli. A reszta rzeczy jak sygnalizacja i data traffic między UE a gNodeB to już jest współdzielone, dlatego widzimy 3 kanały logiczne mapowane na jeden. 

Dobra, jazda:

- gNodeB-specific
  - **BCH - Broadcast Channel** - zmapowany logiczny::BCCH
  - **PCH - Paging Channel** - zmapowany logiczny::PCCH
- UE-specific
  - **Random Access Channel** - Random Access oznacza "Dostęp w dowolnym momencie". UE używa tego kanału jak się "obudzi" i nie wie jeszcze nic o strukturze czekoladki jaką wysyła gNodeB. Więc próbuje tutaj coś wysyłać i może akurat uniknie kolizji z innymi UE.
- Common
  - **DL-SCH i UL-SCH - Downlink i Uplink Shared Common Channel** - zmapowane kanały logiczne::CCCH, DCCH, DTCH, ale z podziałem na uplink i downlink (bo warstwa niżej - jesteśmy już bliżej organizacji tego w air interface)

### Kanały fizyczne

Tu już wkładamy bursty w timesloty - uzupełniamy czekoladke.

Tutaj widzimy dwa kanały, które nie mają żadnego mapowania z góry, czyli nie otrzymują danych do przeniesienia z wyższych warstw, one powstały w tej warstwie - są to kanały, które kontrolują medium.

Mamy też kanały P(U/D)SCH, które niosą info z góry typu common. Oraz po jednym kanale UE i gNodeB-specific, które mapują wyższe kanały -specific.

Dobra, jazdunia:

- Medium control
  - **PDCCH - Physical Downlink Control Channel** 
  - **PUCCH - Physical Uplink Control Channel**
  - Robią sheduling timeslotów (wymiana info jak ma wyglądać on), robią pomiary Transmit Power Control itp.
- Common (mapują wyższe kanały)
  - **PDSCH - Physical Downlink Shared Channel**
  - **PUSCH - Physical Uplink Shared Channel**
- UE-specific
  - **PRACH - Physical Random Access Channel**
- gNodeB-specific
  - **PBCH - Physical Broadcast Channel**

Zaraz je omówimy dokładniej bo Jordi jakoś je lubi i dał na wykładzie dokładniejszy opis.

> Jest pewna kwestia o której nie wspomniałem nic. Dlaczego BCCH i PCH w downlink mają odnogi w kanały shared? Bo części tego rozgłoszeniowego lub pagingowego info idzie tamtymi kanałami. Np. Broadcast ma dwa bloki Master Information Block (dla wszystkich) i jakiś tam inny blok (dla bardziej zainteresowanych UE - chyba tych co są podłączeni do komórki i mają robić pomiary, a MBI jest dla wszystkich UE na świecie).

#### P(D/U)SCH

Trzeba wiedzieć, że to jest jakiś sofcik i on po prostu na tych bitach co dostanie od warstw wyżej, to coś jeszcze robi i opis funkcjonalny poniżej to jest właśnie co on robi:

- Contains User Data and UE-specific higher layers control data (system info and paging)
  - No to na ten fizyczny mapowane są kanały Shared z transportowej warstwy
  - Czyli: Control i User Plane oraz odnogi paging i broadcast(system info)
- For each P(D/U)SCH resource block:
  - UE w 5G może mieć aż do 4 anten (nadawczo-odbiorczych). Stąd bierze się pojęcie **Single-User MIMO**. Czyli skoro mam jakieś słowo 8 bitowe do wysłania, i mam 4 anteny to mogę:
    - wysłać ciurkiem jedną anteną, tak jak jest standarodowo, ale mam wtedy zerowy gain z tych 4 anten
    - wysłać ciurkiem czterema antenami, co wprowadza nieco redundancji, ale tak się robi gdy **SINR (Signal INterference Ratio)** jest przeszkadzający
    - wysłać po 2 bity każdą z anten, co zmiejsza 4-krotnie czas transmisji* i tak się robi gdy SINR na to pozwala
    
      - > *a w 5G przecież jest mocny nacisk na latency
- It adds:
  - **CRC** - 
    - Cyclic Redundancy Check, czyli jeden z error-detecting code
  - **Scrambling**
    - Jak trafi się, że do wysłania jest bajt, który ma same zera lub jedynki to jest to trochę problematyczne, bo
      - a) Łatwo o desynchornizacje nadajnika i odbiornika - jak zmienia się symbol to odbiornik wie, a teraz minął czas trwania symbolu i może sobie skorygować
      - b) jeśli wysyłamy non-stop jedynki to nadajnik ma voltage na UP długo, co w UE zżera batke, antena git bo ma prąd
    - Dlatego zamiast wysyłać takie potencjalnie niebezpieczne ciąg to wysyłam kod scrumblingowy i umawiamy się na jego mapowanie
  - **HARQ**
    - Hybrid automatic repeat request
    - Protokoł do bezbłędnej transmisji w czasie trudnych warunków propagacyjnych
    - Ponad standardowe ARQ dodaje FEC (forward error correction)
  - **DMRS** (Demodulation Reference Signal)**
    - Impuls który wysyłamy w pewnym momencie żeby estymować jaka jest odpowiedź kanału, żeby sprawdzić interferencję i szumy (channel estimation) 
    - Ogólnie DMRS to kreseczki w prawym górnym rogu
  - **Layer mapping**
    - Wiadomka
  - **Transparent precoding**
    - Precoding is a generalization of [beamforming](https://en.wikipedia.org/wiki/Beamforming) to support multi-stream (or multi-layer) transmission in [multi-antenna](https://en.wikipedia.org/wiki/MIMO) wireless communications
  - In additional symbols:
    - Ten kanał czasami wciska takie swoje symbole i jednym z nich jest **Phase Tracking Reference Symbols (PTRS)	**
    - Czasem jak nam się lekko sin i cos przesunie to mamy interferencje w fazie. To jest jedno z trudniejszych zagadnień w telco, no bo przecież cała tranismiaj opiera się na dokładnych i zsynchronizowanych zegarach. Dlatego wysyłamy ten PTRS. 
  - Jakich modulacj używa ten kanał?
    - QPSK, 16QAM, 64QAM, 256QAM
    - Wybiera je na podstawie tych "reference signals"
    - CQI (Channel Quality Indicator) zakres: 0-15 i jest mapowanie np CQI=7 => 16QAM
      -  CQI to wysyła UE do gnb po pomiarach
      - gnb często wybiera lepszą modulację niż CQI wskazuje a potem patrzy jakie straty i dopasowuje ewentualnie

> **UKE jedno z obowiązek to mierzyć jakość usług. Można wnioski składać że jest lipa i UKE musi sprawdzać. Do tej pory robił to piprzed właśnie DMRS. Ogólnie DMRS to kreseczki w prawym górnym rogu jak jest -130dBm to jest wniosek do operatora żeby zmienił (lepsza Aneta albo kolejna) 
> Jedyne co UKE kontroluje to tylko moc sygnału zakres -120 - -130dBm jest git. Ale tylko antena wie jak jest SNR. Aneta wysłała -70 a UE odbiera -120 i tylko antena to wie. Więc wiemy tylko jaki jest coverage ale nic nie wiemy jaka jest jakość usług. 
> Ale od dziś UKE ocenia na podstawie SINR (nie dokładnie SINR ale coś związane zaraz zobaczymy) a jest to RSRP sygnał referencyjny i to tylko w kanale PDCCH 

#### P(D/U)CCH

To jest kanał, który nie przenosi żadnych ramek od warstw wyżej. On kontroluje transmije tej warstwy między nadajnikiem a odbiornikiem.

- Contains control information used in PDSCH and PUSCH
  - Czyli po prostu nadajnik wysyła informacje kontrolne do odbiornika i instruuje go jak ma odbierać/interpretować to co nadajnik mu wysyła na kanałach PDSCH/PUSCH
    - np. nadajnik używa kodów scramblingowych, więc tu wyśle jak je mapować
- DL assignments: PDSCH resource allocation, modulation and HARQ info.
- UL assignments: modulation, power control info. and HARQ info.
- Jako modulacji ten kanał używa QPSK 
  - bo niezależy nam aż tak na szybkości (to nie są dane) takie info kontrolne jest wysyłane dużo rzadziej (np. umówimy się na konkrente mapowanie scrumblingowe i potem używam go aż przez następne 100000 ramek), a QPSK jest wolna ale za to mało błędów
- It adds DMRS for beamforming
  - https://www.linkedin.com/pulse/5g-nr-pdsch-dmrs-figured-out-andrew-kolomatski/?trk=articles_directory żeby wiedzieć ocb to trzeba przeczytać ten artykuł, czy Jordi tego wymaga od nas?

#### PBCH

Tego kanału fizycznego uzywa tylko gNodeB

- PBCH is part of the SSB
- It provides information about the Master information block content used for cell selection
  - Czyli żeby UE sie zsynchronizował z gNodeB (tzn. "wbił w czekoladkę")
- Używana modulacja to QPSK
  - "ja lubie wolmo ale dokładnie, bo nikt mi nie każe szybko, bo nie jestem danymi usera" - PBCH tak mówi zapytany o wybraną modulacje

#### PRACH

Tego kanału fizycznego uzywa tylko UE.

PRACH jest tylko do znalezienia mój beam na tym gnb

> UE może tu mówić słuchaj straciłem beama, informuj mnie jakiś jest mój nowy beam -- nie wiem, do którego myślnika to pasuje

# Za tydzień kolos do slajd 19 punkty 1.2 i ten z sinc(x)

# Fast review

Jak byś miał się czegoś nauczyć o każdej warstwie to tego?

## RRC

Tylko w contol plane

Punkt kontrolny RAN dla core'a.

- paging
- broadcast of system info
- establishment of radio bearers, reconfiguration etc.
- RRC connection and release
- mobility procedures 
  - zlecanie pomiarów i handover

## SDAP

tylko User plane

Mapowanie QoS Flow Id (rozumiane przez core) na Radio bearers (rozumiane przez radio)

Wybór i konfiguracja radio bearera

## PDCP

Usługa jednolitego pakietowego przekazu danych dla SDAP (UP) i RRC (CP).

Tutaj się najwięcej dzieje:

- TCP/IP header compression
- Szyftowanie
- Reply protection
- Integrity protection
- Sequence numbering
- Wybór trybu (AM, UM, TM)

## RLC

Usłga transferu PDU wyższych przez MAC. 

- Segmentacja wyższych PDU.

- Zapewnienie trybu (AM, UM, TM)

## MAC

- mapowanie kanałów logicznych na transportowe
- HARQ
- Iband monitoring

## PDSCH / PUSCH

Przesyła dane control i user plane.

Dodaje scrambling, CRC, HARQ, Reference signals, modulacje QPSK, 16QAM, 64QAM, 256QAM

## PDCCH / PDUCCH 

Nie przesyła żadnych ramek wartwy wyższej. 

Kontroluje transmisje kanału P(D/U)SCH, które leci "obok".

## PBCH

Broadcast

QPSK

## PRACH

Gdzie jest mój beam

# Kolos2 się wydarzył

Jakie były pytania?

- Opisz kanał PBCH
- Wymień functionalties MAC

Trzeba pytać Kuba Kitka Polska o 3-cie i weryfikacje

## OFDM

- **Multi-path propagation** - odbicia przeszkadzają bo w nadajniku robi się **intersymbol interference**. Dlatego robi się tzw. **cyclic prefix**. Czyli symbol nie trwa `T`, a `T+T'`, nieco dłużej, tak aby zdążył zaistnieć na tyle, że nadajnik go uzna za symbol do odebrania. Wartość `T'` w obszarach gdzie jest dużo odbijania się (np. miasto) powinna być większa, a tam gdzie nie trzeba (pole, łąka) mniejsza. Niestety w LTE to tylko jedna wartość, a w 5G dwie.

- **Channel frequency selectivity**

  - ```
    y = h*x + n
    y - to co będzie odebrane
    x - to co wysłane
    n - noise (ale szum biały)
    h - odpowiedź medium (warunki propagacyjne)
    ```

  - **szum biały** - to szum jaki wprowadza sama aneta, nadajnik i odbiornik (a w nim detektory), nie zależy on od otoczenia, od medium, a od samych urządzeń. Po prostu UE i gnb ich detektory charakteryzują się jakimś szumem na antenie. 

  - Ten szum biały mogę sobie estymować i na tej podstawie zrobić equalization

  - ![](img/20.png)

- **Signal modulation, DFT, sinc(x)**

  - Każda nośna ma jakiś wzór:
    Asin(2pinf0t) + A2cos(2pinf0t) i nadajnik wysyła sumę punkt po punkcie. I tak co symbol czyli okres sinusa T. 
  - Potem z czasu idzie to na f czyli transformata Fouriera ez
  - Tylko jedna nośna będzie na max amplitudę w punkcie środkowym, reszta wszystkie są zero tam. Dlatego nie ma interferencji między nośnymi - bo są ortogonalne.

- **Doppler shift creates channel incoherency -> coherence time* limits the inter-arrival samples of channel estimation**
  - *ang. incoherent* - (physics) (of waves) having no definite or stable phase relationship.
  - *ang. coherent* - (noun) the quality of being logical and consistent. (przymotnik) konsekwentny 
  - Efekt Dopplera
  - *https://en.wikipedia.org/wiki/Coherence_time - For an electromagnetic wave, the **coherence time** is the time over which a propagating wave may be considered coherent, meaning that its phase is, on average, predictable. In long-distance transmission systems, the coherence time may be reduced by propagation factors such as dispersion, scattering, and diffraction. Czyli czas jaki możemy uznać, że lecąca fala jest spójna w fazie, że lecąca fala nie zmieniła nic swojej fazy, że faza jest taka jak w nadajniku
- **Peak to Average Power Ratio (PAPR) --> scrambling**
  - Znowu chodzi o voltage, stosujemy scrambling (szamotanina - czyli zamiast stały sygnał to wysyłamy poszamotany)
- **sensitive to phase noise and to frequency and time deviation -> synchronization (reference signals and synchronization channels)**
  - *ang. deviation* - the action of departing from an established course or accepted standard ; odchylenie
  - Czyli podczas transmisji między Tx a Rx są odchylenia w czasie i freq dlatego więc stosujemy synchronizacje poprzez reference signals i dedykowane sygnały synchronizacyjne

Tu Jordi też zaznaczył iż OFDM nie jest nic analogowe, wszystko idzie DFT, a jak wiemy DFT to suma szeregu o nieskończonej liczbie elementów, a przecież nie da się wytworzyć nieskończoności w skończonym czasie, więc ta transformata nigdy nie jest na 100% idealna.

## Physical layer

> Nokia głównie zarabia z patentów - wymyślą coś, potem żeby inne firmy mogły tego używać, to muszą im płacić. Dlatego Nokii Open-RAN aż tak bardzo nie wadzi. Ericsson z kolei już mu Open-RAN przeszkadza, więc udaje, że tam jest ale nic się nie udziela i nie zagania tego do przodu.

- **TDD vs FDD**

  - Time Division vs Frequency Division Duplexing
  - TDD is a method where both the transmitter and receiver use the same frequency band but transmit and receive traffic at different times.
  - FDD is a full-duplex method that uses two different frequencies for transmit and receive operations.
  - Comparison
    - FDD się używa się na małe f 
      - Wszystkie kraje EU zdecydowały, że na 3.4-3.8 będzie TDD
      - Na 700MHz i poniżej FDD
    - TDD jest prostsze a FDD jest trudne bo anteny muszą słuchać i nadawać w tym samym czasie
    - TDD ma opóźnienie większe.
    - TDD jest łatwiej zmieniać proporcje UPlink i downlink np z up600dl800 na up700dl700
      

- **Flexible-OFDM:      flexible symbol duration (sub-carrier spacing) and CyclicPrefix duration per each subband** 

  - W 4G szerokość sub-carrier jest taki sam (15kHz), a w 5G jest aż 5 możliwości

  - Skąd taki wybór? Bo 5G jest service-centric nie tylko eMBB jak 4G. I np. takie URLLC potrzebuje szerokiego pasma, dzięki któremu będą małe latency. Przy większym kanale, też efekt Dopplera, aż tak nie doskwiera.

  - Dlatego w 5G jest 5 subcarrier spacing (**SCS**): 15, 30, 60, 120, 240 kHz

    - 120 i 240 jest tylko dla pasma 26GHz (URLLC)

  - Bandwidth Part: UE specific allocation (UL/DL). Bandwidth Parts are adaptable to UE
    features and UE communication state

    - UE i gNodeBdogadują się na jakim SCS będą gadać (jakie bandwidth parts supportują)
      - Po co to? Bo np. urządzenia IoT wspierają najczęściej tylko 15
    - Podczas sesji można zmieniać bandwidth parts

  - <img src="img/21.png" style="zoom:50%;" />

  - Krzysiu Sadura dostał zadanie od Jordiego, żeby policzyć jaki jest Bitrate, gdy mamy dostępne pasmo 100MHz dla jednego UE.

    - 100MHz to reasonable szerokość, UKE rozda np. operatorom po 80MHz, 80MHz też będzie na NPN'y

    - Krzysiu jako, że jest skromny wybrał, że sub-carrier spacing to będzie 30kHz.

    - ![](img/22.png)

    - Pytanie teraz ile symboli zmieści się w jednej milisekundzie?

    - Trzeba zajrzeć do tabelki dla Subcarrier spacing 30, czas trwania symbolu to 33.3μs, ale trzeba do tego doliczyć, że między symbolami jest trawający 2.3μs CyclicPrefix, tak więc łącznie mamy 35.6μs. 1ms=1000μs, robimy dzielenie i nam wychodzi 28.

    - ![](img/23.png)

    - Dobra, no to teraz pytanie ile jest bitów na jednym symbolu? To już zależy od modulacji, my zakładamy maxowy przypadek i że są super warunki propagacji, więc bierzemy 256QAM ==> 8 bitów na jeden symbol. Z tym, że musimy pomnożyć to przez *wspólczynnik kodowania*, no bo nie wszystko to są dane do wysłania przez warstwe fizyczną, ale też CRC itp.  Jordi ma taką tabelkę:

      - <img src="img/24.jpg" style="zoom:50%;" />
      - I z niej widzimy, że na 1024 bity przypada 948 bitow danych, reszta to CRC, FEC itp.'

    - Okej no to policzmy jaki jest bitrate na jednej nośnej (sub-carrier) podczas jednej milisekundu przy modulacji 256QAM

      - ```
        Br = 28[symboli/milisekundę] * 8[bitów/symbol] * 948/1024[bitów danych/bitów łącznie] = 207.375[bitów/milisekundę]
        ```
    
    - To jest dla jednego sub-carrier, a my liczymy max przypadek, że UE jest sam w komórce.
    
      - Ile zmieści się 30kHz sub-carrier w 100MHz kanale? Odp: 3,333.3333
    
    - I to było dla jednej milisekundy, więc znormujmy to do sekundy
    
    - Wychodzi 691,250,000 czyli `691.25 Mbit/s`
    
    - Ale to na poziomie warstwy PHY, a czyste dane w tym (np. zapytanie HTTP) to 84%
    
    - Czyli wychodzi `580.65 Mbit/s`
    
    - Stosując MIMO4x4 ten wynik możemy polepszyć do`2.322 Gbit/s`

**Resource block** tak nazywa się 12 przenośnych dla anteny nie ma nic innego niż resource block i to jest jej jednostka. Bandwidth ma np. 10 RB 

Tak wygląda ramka dla Subcarrier Spacing 60 i 240 kHz

![](img/24.png)

Najmniejsze co jest to jest symbol, symbol w zależności od modulacji koduje ileś bitów (np. 64QAM koduje 6bitów).

W SCS (Sub-Carrier Spacing)=60kHz, symbola trwa 16.7µs, a w SCS=240KHz, symbol trwa 4.17µs, symbole wkładane są w sloty. Sloty w subframe'y, a subframe w radio frame. Radio frame trwa aż 10ms i jest największą strukturą. Jordi nie tłumaczył skąd te podziały itp. więc luz.

### Beamforming

MIMO (Multiple Input Multiple Output) walczy z multipath-propagation, czyli po to ma wiele odbiorników, żeby odebrać wiele poodbijanych sygnałów i poskładać je do kupy, same z outputem.

Massive MIMO, to marketingowa nazwa na to, że tych anten jest naprawdę dużo (Massive), czyli AŻ 32, 64, 128, 254, 512 :astonished:

**Beamforming** to rozszerzenie do MIMO, coś innego niż MIMO, uzbrojenie MIMO w kolejne narzędzie, ale to już inne zjawisko. Beamforming to celowanie w UE mocą sygnału.

> **Deep edge** - sam kraniec zasięgu anteny

Beamforming fakty:

- używany na dużych f (głównie uzywany w paśmie 26GHz, na 3.4-3.8 już mniej, a na 700MHz to już prawie wcale, bo tam przecież nie ma na deep edge nawet problemów)
- polepszenie sygnał na deep edge
- dużo mniejsze zużycie energii w antenie
  - no bo nie jest dookoła wysyłane tylko w jedno konkretne miejsce, policz całke objętości byku
- czas koherencji (czas efektu Dopplera) większa atenuacja kiedy są obiekty po drodze i mamy więcej problemy z f 
- Z tymi beamami to nie jest tak że one gonią za userem. Antena ma Beam w jakimś kierunku i tam przełącza UE.  
  - recovery jak ja wychodzę i tracę beama to nowy ma być (requirement mówi że tylko 0ms ma być ten czas) czyli dwa beamy naraz są nadawane
  - Ile antena ma beamów w danej chwili czasowej max?
    - 26GHz --> 64
    - C-band (3.4-3.8) --> 8 dla SCS=15,30,60
    - 700MHz ---> 4
- Beamforming może być cyfrowy, analogowy lub hybrydowy

### 5G Mobility

Są trzy rodzaje:

- Beam Mobility - w obrębie beama --> w obrębie komórki/anteny
- Intra-RAT Mobility - między komórkami ale still w 5G
- Inter-RAT Mobility - między 5G a 4G/3G

> na handover (przepięcie z komórki na komórkę) są dwa powody, albo UE się rusza, albo antena robi load balancing

#### Intra-RAT and Inter-RAT

> Przypomnijmy stany RRC:
>
> idle - nie ma UE w sieci
>
> inactive - UE jest w sieci ale brak sesji
>
> connected - UE jest w sieci i jest sesja

W stanach **IDLE** i **INACTIVE** mamy tzw. UE-trigerred mobility - czyli UE inicjuje. UE ma info do tego dzięki SIB2

W stanie **CONNECTED** z racji, że musi być continuity na sesji. to antena każe UE robić pomiary non-stop i z racji że zna ona całą sięć, to antena decyduje o handover'ze. Ale nie zawsze musi być w to involved 5GC (Core) --> jak gNodeB mają ten sam UPF, to nie trzeba core wystarczy Xn. Handover ma 3 fazy:

- preparation (UE measures serving and neighbour gNodeB)
- execution (przepinanie, dwie anteny naraz wysyłają do UE)
- completion (data forwarding, czyli zanotowanie przepięcia wyżej)

Note: UE capabilities of different RAT are provided in the mobility command

> Kreseczki są na podstawie tego co mierzy UE sib2, i tam nie ma rozróżnienia na sygnał i szum jest tylko moc, więc czasem może być że masz dwie kreseczki a się nie da gadać bo to sam szum little
>
> To się nazywa pomiary aktywne i pasywne pasywne robi UE w idle i inactive no bo po co aktywne nie jest tak groźne bo dane nie są wysyłane a jak jest rrc connected to robi aktywne czyli SNR 

#### Beam Mobility

W całości jest handlowany przez warstwy od PHY do RLC max, core nie jest involved

> Skopiuje slajd i dam komy zanotowane podczas wykładu, bo mi się nie chce więcej :tired_face: :cold_sweat: :thermometer:

**Beam Correspondence**

Jak jest Correspondence to ten sam beam jest używany do tranismicji UL i DL

![](img/27.png)

W jednym momencie nadaje antena tylko jeden beam przez 5ms potem zmienia na kolejny. Co każdy subframe trzeba robić wszystkie beamy 

**Beam mobility and Power measurements**

- Mamy tutaj dwie strony UE i network
- Power measurements mogą mieć dwa tryby:
  - Iddle mode - w celu  cell (re)selection, synchro of Signal in broadcast messages
  - Connected mode - używany w celu handover, channel state information in reference signals
    - Jak się dzieją?
      - albo UE generuje raporty pomiarowe periodycznie (okresowo) albo triggerują je zdarzenia (wejście w komórkę sąsiędnią)
    - Raporty (co mają mierzyć (object to measure) i co jak mają wyglądać) są opisywane przez network
- Network adjusts physical control and user channels for beam adaptation
- Jest wymaganie, że interruption time spowodowany przełączeniem beamów ma wynosić 0ms, stąd są dedykowane resources na random access na kanale PRACH



#### Mobility & Security

Jak wiadomo cała transmisja między UE a gNodeB jest szyfrowana 

>  przynajmniej w teorii xd, bo tak naprawdę to operatorzy mają to w piździe, więc nie cała jest szyfrowana)

Szyfrowanie wiadomo odbywa się za pomocą jakiegoś klucza, więc jak UE i antena mają jakiś klucz którym szyfrują, to jak UE zmieni antenę, to ten klucz już musi mieć taki jaki pasuje w nowej antenie. Na dole slajd, który nic nie wyjaśnia.

![](img/26.png)

# Core

> Ogólnie w radio jest jeden chuj jak LTE oprócz beamforming. Ofdm jest ten sam 
>
> W telco softwaryzacja jest nowa, w IT już jest dawno
>
> Dla bezpieczeństwa jest katastrofa, jak jest problem to nie wiadomo czy to problem chmury Amazona, kibernetesa, vmware czy nokii softu, a wcześniej jak cała szafa była od vendora, no to ten
>
> User plane nie zmieniamy nic od LTE, a w core można się bawić 

Między designowaniem EPC (Core 4G) a 5GC (Core 5G) w IT bardzo dużo się zadziało wirtualizacja wprowadziła dwa koncepty SDN i NFV, tak właściwie to 5G to jest dopasowanie sieci mobilnych pod te nowe wynalazki - Jordi po chwili opisu jakie zmiany zaszły w IT powiedział:

![](img/29.png)

No dobra, ale co konkretnie daje nam wirtualizacja? Opisuje to ten slajd

Plusy:

- elastyczność
- koszt
- time to market 

Wady:

- największa wada writualizacji to wydajność
- druga poważna wada to bezpieczeństwo (przypomniaj sobie CIA Triad)
  - Jak padnie chmura, która niezależy od nas, to padną też nasze serwisy

## 5G Core - drive factors

Czyli jakie nowinki technologiczne przyczyniły się do developmentu tego core.

### Containers and VMs

> Kto opisał wgl tę wirtualizację?
>
> ETSI NFV, jest też OPNFV, ale świat poszedł w stronę ETSI
>
> Ogólnie ETSI z całego 3GPP jest najmocniejsze

![](img/28.png)

Na rysunku mamy ewolucje z maszyn wirtualnych na kontenery. Jakie są wady i zalety kontenerów?

**Wady**

- są młodsze
  - zawsze w IT jest tak, że to co młodsze to gorsze, bo nie wygooglujesz, bo nie wiadomo jak działa z czymś tam, często na dany problem trafiasz jako pierwszy z tego powodu np. ja trzymam się z dala od Windows 11

**Zalety**

- mniejsze latency na nich jest, apka bezpośrednio korzysta z zasobów systemu, nie ma layeringu jak w VM
- resilience (odporność)
- portability - kontenery można ez przenosić sobie
- short-lived services - jak potrzebuje jakiegoś serwisuy nie cały czas tylko na kilka minut, to z kontenerami jest to możliwe, z VM już gorzej
- problem split - duży problem rozbijam sobie na mniejsze kontenerki
- reusability - mogę jeden serwis w wielu miejscach używać. Np UDM jest używany przez AMF i PCF

### Software jako microservices

Microservices : software development by reducing the software to small independent software services with well defined APIs

- Scalability - jak jest mały ruch w sieci to płace za małe zużycie zasobów, jak duży to skaluje to co mam i dopiero płace za więcej
- Easy development - każdy programista powie, że development jest prostszy przy microserwisach (gorzej z integracją hehehe)
- Network service is a set of microservices 
- Microservice instances may be easily added removed
- Each microservice with own life cycle

### Network Automation

Network automation

- Based on SON ( Self Organising Network): self configuration , optimization , & healing
  - Czyli taki Kubernets
- Makes use of AI/ML
  - Czyli takie Nephio

### Cloud Native

Chmury mają dużo wad ale overall wychodzą na plus.

- Infrastructure agnostic
- Software decomposition and life cycle --> microservices
- Resilience : Independence of SW components and isolation
- Orchestration : State and data optimization
- Automation ( e.g ., Kubernetes based Container as a Service)

## LTE interctonnection

![](img/32.png)

To już było przed pierszym kolo. Chodzi o to, że 5GC umie gadać z Radio Access Network z 4G.

Dwie opcje są zaznaczone jako commercial

- Option 3 - to co mamy teraz w Polsce, czyli RAN 5G, ale core jest z 4G
  - To nazywamy Non-Standalone, czyli nie stoi samo to 5G, jest wspierane przez elementy 4G
- Option 2 - to do czego dążymy, 5G standalone, za jakiś czas robię przetarg na to w PLK XD
  - standalone (czyli stoi sam) 5G stoi samo, czyli i RAN i Core jest 5G

## Service Based Architecture

![](img/30.png)

To co widać na obrazku to NF'y (**Network Function**). Nie trzeba się ich uczyć. Najważniejsze jest to, że są one na wspólnej szynie i każdy NF oferuje jakieś serwisy, z których inne NF'y mogą korzystać. 

Przykładowo UE chce się zalogować do sieci, ten request dostanie AMF (tylko AMF i UPF mają połączenie do kogoś spoza core'a). AMF żeby wypełnić swoją misję czyli zarejestrowanie UE w sieci, a potem danie mu sesji danych musi użyć serwisów swoich kolegów, którzy specjalizują się w małych kroczkach, które w makro skali złożą się na to. Więc tak, po pierwsze to AMF musi zatentykować i zautoryzować UE. Odzywa się w tym celu do AUSF - AUthentication Server Function "Mordo, czy to UE (numer IMSI) to ja mogę wpuścić do sieci?". Zauważ, że w kodzie AMF cała logika związana z autentykacją to będzie wykonanie zapytania do AUSF i potem dostanięcie odpowiedzi od niego, a ten cały bałagan się za tym kryjący chowamy do AUSF. AUSF odpowie do AMF albo że tak, albo że nie, albo żeby UE podało jakieś dodatkowe rzeczy do uwierzytelnienia. Jak już AMF od AUSF wie, że UE może być zalogowane, to AMF teraz pyta PCF (Policy and Charging Function), czy to UE ma dostęp do sesji danych (czy płaci abonament itp.), więc wysyła zapytanie do PCF "mordo, czy to UE (numer IMSI), to może u nas korzystać z neta?". PCF mu odpowie tak lub nie, albo tak, ale tylko do 20 Mbit/s max, albo "tak, ale tylko YouTube" (są takie pakiety/taryfy dla klientów). No to jak już AMF wie, że to UE jest zautentykowane i że może korzystać z neta, to zleci do SMF (Session Management Function) zestawienie sesji danych. Wyśle do niego request "Daj temu UE sesje do netu na 20Mbit/s". SMF to wykona i odpowie "mordo, załatwione". 

Czyli generalnie chodzi o to, że każdy NF ma "swoją brożkę", w czymś się specjalizuje i to wystawia na świat jako **services**, a inne NF'ymogą się do tych services zwrócić o pomoc w wypełnianiu swojego zadania. 

Uwaga, to też jest tak, że jak np. AUSF dostanie od AMF prośbę o autentykację, to AUSF korzysta z serwisu UDM (Unified Data Management), żeby sprawdzić credentiale tego usera). A SMF jak dostanie prośbę o zestawienie sesji, to tak naprawdę wybiera odpowiedni UPF i tam zleca zestawienie tej sesji.

> To podobnie jak preze firmy każe dyrektorowi sporządzić raport, który ma 5 rozdziałów. Dyrektor dostanie to zadanie ale tak naprawdę to poprosi 5 kierowników, każdego o jeden rozdział. Potem Ci kierownicy dadzą to swoim pracownikom do zrobienia itd.. Każdy dołoży tu swoje 5 groszy i w kupie siła.

![](img/31.png)

To jest to samo co rysunek wcześniej (ten z szyną), tylko że....

Ogólnie jak mamy to odzywanie się między NF'ami to nie jest przecież tak, ze każdy NF odzywa się do każdego NF'a istnieją jakieś podzbiory NF'ów do jakich odzywa się dany NF. I taki "reference point representation" właśnie pokazuje te podzbiory.

### Zalety SBA

- Functional Disaggregation
  - Bardzo skomplikowany element z 4G jak MME, został zdekomponowany na dużo prostsze elementy.
  - MME robił tak dużo, że jego funkcjonalności są tak naprawdę "spread" prawie po całym 5G, ale głownie rozeszło się to na AMF, SMF, SEAF
- Client-Server: decopling NF-consumer and NF-producer
  - NF-producer - NF który wystawia swój service
  - NF-consumer - NF który korzysta z tego service
- Light Service-based interfaces
  - Te services, które udostępniają NF'y są udostępnianie na interfejsach, które nazywam **Service-based interfaces (SBI)**
- SBI
  - Te interfejsy są zrobione według REST
    - REST to taki jakby framework do robienia api, udostępniania danych, taki jakby styl architektoniczny
  - Używają protokołu HTTP 
    - HTTP to protokół, który implementuje REST 
    - Używane metody: GET, POST, PUT, DELETE
  - Identyfikowane za pomocą URI - Uniform Resource Identifiers

#### Protocol Stack

![](img/33.png)

NF to ta najwyższa warstwa logika tego co jest przesyłane. 

A ta logika jest przesyłana w JSONACH.

A te JSONY w HTTP

#### Example

Czyli np. jak wcześniej był przykład, że AMF pyta AUSF czy ten UE jest legit i można go zalogować do sieci.

AUSF takowy service ma wystawiony na interfejsie o nazwie `Nausf_UEAuthentication`. 

No więc teraz AMF tworzy pakiet HTTP a w niego wsadza Json taki:

```json
{
    "imsi": 41243125132132,
    "password": "legiatochuje"
}
```

> Imsi to międzynarowy identyfikator karty SIM, takie id usera w sieci, coś jak nr tel ale dla maszyn a nie dla ludzi

No i AMF wysyła tego JSON pakietem HTTP używając metody ` POST` na interfejs ` Nausf_UEAuthentication`. 

To sobie leci tam przez sieć TCP/IP i blah blah blah, nie będe mówił przecież, uczymy się tego piąty rok i raczej nie krew w piach.

I potem AUSF odpowiada:

```json
{
    "isAuthenticated" = "true"
}
```

Ofc. to jak wyląda ten JSON itp. to ja uprościłem i wymyśliłem. Oficjalna specyfikacja jest tutaj https://www.etsi.org/deliver/etsi_TS/129500_129599/129509/15.01.00_60/ts_129509v150100p.pdf 

<img src="img/34.png" style="zoom:70%;" />

Tu mamy ogólnie jak wygląda takie zapytanie. Nie tylko AMF może pytać AUSF o autentykacje (5G Core jest mega elastyczny), dlatego tak po lewej jest NF Service Consumer. POST to metoda HTTP /ue-authentications to kawałek URI, który mówi o jaki dokładnie service chodzi, a authenticationInfo to json z imsi czy coś. No i potem widać jak to dalej leci

### NRF

No dobra wszystko fajnie z tym core. Są NF'y one ze sobą eleganko współpracują i wszystko bangla.

Ale zastanawiałeś się młody człowieku skąd NF-consumer ma 

- po pierwsze wiedzieć że drugi NF (z którego może skorzystać) w ogóle istnieje
- po drugie jaki jest jego adres IP (żeby wysłać do niego zapytanie to trzeba ten adres znać co nie)
- po trzecie jakie zbiór service'ów ma ten NF

No i tu z pomocą przychodzi NRF (**Network Repository Function**). Jest to jeden z NF'ów, którzy trzyma oraz dystrybuuje info o innych NF'ach. Niezłe jaja co.

Czyli generalnie to jak włączasz nowy NF do core, to jedyne co mu konfigurujesz to adres IP NRF. Wtedy ten nowy NF odezwie się do NRF i od niego dostanie całe info o innych NF'ach, które jest potrzebne do współpracy z nimi (ich adresy IP i oferowane service'y). Oczywiście też ten nowy NF sam "zarejestruje" się w NRF, żeby inne NF'y mogły też się o nim dowiedzieć.

Takie odkrywanie NF'ów za pomocą NRF nazywa się **NF Discovery**.

Takie wpisywanie się do NRF jako nowy NF to **NF Registration**.

Na dole slajd:

![](img/35.png)

O co chodzi z tym Communication? Mam o tym [oddzielny pliczek](SBA/5G Service-Based Architecture.md)

Link: https://github.com/0x41gawor/zeszyty-22z/blob/master/TESM/SBA/5G%20Service-Based%20Architecture.md
