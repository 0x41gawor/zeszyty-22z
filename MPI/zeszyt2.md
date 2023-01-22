- [ ] Na czym polega NFV, architektura i główne komponenty na przykładzie ETSI MANO. Przyczyny czemu sieci ewoluują w tym kierunku.
- [ ] Cel i zasada działania edge computing. Różnica między fog, edge oraz MEC. Architektura MEC i przykładowe zastosowania
- [ ] Jakie są i naczym polegają modele świadczenia usług wykorzystujących technikę chmur obliczeniowych. Kiedy ją stosujemy i dlaczego może być opłacalne. Omów jej ograniczenia i zagrożenia.
- [ ] Czym jest orkiestracja. Podstawowe funkcje. Czym różni się od zarządzania. Czym różnią się funkcje orkiestracji w centrach danych od systemów obliczeń na brzegu sieci
- [ ] Zadanie optymalizacyjne - MEC
- [ ] Zadanie optymalizacyjne - CDN
- [ ] Zadanie optymalizacyjne - VNF
- [ ] Zadanie optymalizacyjne - to inne

# Wprowadzenie

## Nowe Techniki

### Wirtualizacja infrastruktury - NFV

NFV - Network Function Virtualization

Koncept architektury sieciowej wykorzystujących technologie wirtualizacji wykorzystywane w IT. Wirtualna funkcja sieciowe (VNF - Virtual Network Function) jest zaimplementowana jako maszyna wirtualna lub jako kontener. https://en.wikipedia.org/wiki/Network_function_virtualization#History

Czemu sieci ewoluują w tym kierunku, na co to pozwala?

![](img2/1.png)

Na odzielenie ról, nowe modele biznesowe i na elastyczność.

> InP to na przykład Cellnex

> Nie jesteśmy zależni od hardware jebać ciscoi juniper. Co z wydajnością jeśli to soft? Generalnie jak jest sam soft to wydajność spada.
> UPF 
> Ale mamy zrównoleglenie, więc stawiam bardzo dużo UPFów ograniczonych i no nawet w worst case niech będzie że jeden UPF na jedno połączenie
> Drugi trend to wspieranie hardwarem i właśnie na tych Infra są te rzeczy udostępnione.

Głowne cechy tego rozwiązania:

- **elastyczność** - Każdy SP powinien mieć możliwości stworzenia dowolnej topologii sieci, rutingu i metody przekazu danych i mieć możliwość zaimplementowania protokołów sterowania niezależnych od sieci fizycznej i innych VN.

  - >  Protokół IP jest passe i dzięki wirtualizacji jak ktoś wpadnie na super pomysł nowego protokołu to łatwiej to zaimplementować.

- **ułatwione zarządzanie** - wprowadzenie modularności zarządzania siecią – zarządzanie na każdym poziomie.

  - > Więc wydajność gorzej, ale poprawiamy to jak się da (wspieranie hardware'em) i tak już nie ma odwrotu od NFV Bo jest proste zarządzenie itp a ten spadek kompensujemy.
    > Łatwiej się zarządza ale skomplikowanie jest większe w sensie zrozumieć to wszystko jest trudniej 

No ok, ale NFV to architektura, jak więc ona wygląda?

Na rysunku widzimy jeden node, na którym odpalone jest 3 funkcje sieciowe, a obok dołączone do tego node'a są systemy Management and Orchestration.

![](img2/2.png)

**OSS/BSS** - to co u operatora telco najważniejsze - charging, policy itp.

**EM** - Element Management. Czyli coś co zarządza lokalnie danym elementem. Jakiś agent **VNF Manager**?

**VNF** - Virtual Network Function - czyli to co jest wirtualizowane, gwóźdź programu

**Virtualisation Layer** - warstwa odpowiedzialna za wirtualizację - VirtualBox, VMware, Docker, kvm, conteinerd

**NFV Orchestrator** - dwie funkcje:

- orekiestracja zasobów infrastruktury across wiele Virtualised Infrastrucure Manager 
- zarządzanie cyklem życia usług

**Virtualised Infrastructure Manager** - sterowanie i zarządzanie NFVI (infra) compute, storage and network resources. Np. Kubernetes tym jest.

**VNF Manager** - zarządzanie cyklem życia instancji VNF. Management and orchestration aspects of a VNF include traditional Fault Management, Configuration Management, Accounting Management, Performance Management, and Security Management (FCAPS).



#### Główne cechy VNF



### Software Defined Network

