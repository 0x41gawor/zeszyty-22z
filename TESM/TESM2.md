# 15

Innowacyjności

- Massive MIMO
- Połączenie się przez Wi-Fi (użycie modemów wifi jako stacji bazowych i dzięki temu operator tam gdzie komuś świadczy internet ma zwiększone pokrycie)
- 5G używa OFDM (tak jak 4G)
- 5G też może używać NOMA (bardziej energooszczędne) ale NOMA jeszcze nie ma jednak 5G i jest zdecydowane że będzie w 6G
- Shared Spectrum Access. Niektóre połączenie będą mieli większy priorytet i będą potrzebowali szersze pasmo np. mission critical policja, powódź itd.

RAN był podzielony

- część elektryczna zmienia bity na sygnał radiowy
- a niżej pod anteną było pudełeczko

To teraaz to pudełeczko się podzieli na dwa (DU+CU)

Dlaczego CU na kilka anten?

Bo są niektóre funkcjonalności radiowe że ne trzeba robić ich  na każde antena.

Dzięki temu na CU operuje kilkoma antenami, to jak jakiś user ma kiepski zasięg to ja mogę użyć kilku anten dla niego

# 16

device to device communication - komórka rozmawia z komórką bez anteny

flexible networks - nowe use case biznesowe bo cala siec jest softwaryzowana i wirtualizowana

VM vs kontener w 5G --> wygrywają kontenery

to daje dużą elastyczności jak jakiś operator chce dodać nowego NF'a no to dodaje

(kiedyś planowano np, zeby w Polsce było NF od bezpieczeństwa)

Fronthaul interfejs radiowy mędzy user a antena

Backhaul między antena i core

antena na latarni ma mniejszą moc, 

ogarnij ten integrated backhaul i fronthaul bo nwm ocb

Flexible duplex.  FDD - wysyłam i odbieram na różnych częstotliwościach, TDD - odstępy czasowe time sloty na uplink i downlink, TDD jest lepiej kiedy mamy duży throughput Technologicznie możliwe, prawnie nie bo UKE decyduje jaka jest duplex na daną `f` mimo, że antena potrafi sobie zmieniać.

(UKE patrzy po prostu ile vendorów na danej f ma co --> antymonopol np. Nokie nie ma FDD na jakiejśtam)

