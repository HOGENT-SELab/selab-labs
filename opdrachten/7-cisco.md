# Opdracht 7 - Het opzetten, configureren en testen van een eenvoudig netwerk in Packet Tracer

In deze opdracht zal je een compleet IPv4- en IPv6-netwerk opzetten met PC's, switches en een router in Cisco [Packet Tracer](https://www.netacad.com/courses/packet-tracer).

De instructies in deze opdracht zijn wat bondiger. Je zal beroep moeten doen op de kennis en ervaring die je hebt opgedaan in het OLOD Computer Networks I.

## :mortar_board: Leerdoelen

- Je kan een correct addresseringsschema opstellen voor IPv4 en IPv6.
- Je kan een gesimuleerd netwerk opzetten in Cisco Packet Tracer.
- Je kan een router, switch en computer correct instellen en zo het gesimuleerd netwerk functioneel maken.
- Je kan een SSH-verbinding opzetten naar een router of switch.

## :bar_chart: Evaluatiecriteria

Toon na afwerken het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze opdracht! Criteria voor beoordeling:

- [ ] Je hebt een correct adresseringsschema voor IPv4 uitgewerkt en kan dit toelichten.
- [ ] Je hebt een correct adresseringsschema voor IPv6 uitgewerkt en kan dit toelichten.
- [ ] PC1 kan pingen naar SW1, R1, SW2 en PC4 over IPv4.
- [ ] PC1 kan pingen naar PC4 over IPv6.
- [ ] De begeleider selecteert willekeurig een van volgende toestellen: SW1, R1, SW2. Je kan op dit toestel het volgende demonstreren:
  - [ ] Je kan inloggen via de consolekabel.
  - [ ] Er is een wachtwoord ingesteld voor console en privileged EXEC mode.
  - [ ] Er is een MOTD ingesteld.
  - [ ] Wachtwoorden staan geëncrypteerd in de running config.
  - [ ] Er zijn geen ongewenste DNS lookups.
  - [ ] De startup config is weggeschreven.
  - [ ] Je kan via IPv4 pingen naar zowel SW1, R1, SW2.
- [ ] Je kan vanuit PC1 een SSH-verbinding openen naar SW1 en R1 via IPv4.
- [ ] Je hebt een verslag gemaakt op basis van het template.
- [ ] De cheat sheet is aangevuld met nuttige commando's die je wil onthouden.
- [ ] Je kan een correct antwoord geven op de vragen die zijn aangeduid met een :question:.

> Opmerking voor studenten TIAO: elk teamlid toont een deel van de evaluatiecriteria, eventueel op een ander toestel.

## Probleemstelling

Een bedrijf of organisatie kan tegenwoordig niet meer functioneren zonder een netwerk. Een netwerk gebruikt **switches** om toestellen met elkaar te verbinden en **routers** om netwerken met elkaar te verbinden. In onze simulatie willen we graag twee subnetten opstellen en deze met elkaar verbinden volgens de **topologie** zoals weergegeven in onderstaande figuur.

![Overzicht netwerk](./img/cisco/netwerk.png)

## :memo: Opdracht

### Stap 1 - Topologie

- Zorg ervoor dat je de laatste versie van Packet Tracer geïnstalleerd hebt.
- Bouw in Packet Tracer een netwerk zoals op bovenstaand schema.

  - Dit netwerk heeft **twee subnetten**:

    - Subnet 0: hosts PC1 en PC2, switch SW1, interface G0/0/0 van R1.
    - Subnet 1: hosts PC3 en PC4, switch SW2, interface G0/0/1 van R1.

  - De router is een **4331 Cisco router**.
  - De switches zijn elk een **2960 Cisco switch**.

- Verbind de toestellen met de juiste kabels.
- Je zal de computers PC1, PC2 en PC3 gebruiken om in te loggen op de switches en routers, en deze vervolgens te configureren. Verbind dus de volgende toestellen met behulp van **consolekabels**:
  - PC1 met switch SW1
  - PC2 met router R1
  - PC3 met switch SW2

### Stap 2 - Bijwerken software op router/switch

Sommige commando's uit de volgende stappen werken enkel indien de software versie op jouw switch of router 15 of hoger is. Dit controleer je via het commando `show version`. Is dat niet zo dan voer je eerste de instructies uit zoals vermeld op deze site: <https://yaser-rahmati.gitbook.io/rahmati-academy/Tutorials-Library/cisco-adademy/cisco-packet-tracer/use-a-tftp-server-to-upgrade-a-cisco-ios-image>. Je voert de instructies op elk apparaat afzonderlijk uit tot elke router en switch over minstens versie 15 beschikt.

### Stap 3 - Basisconfiguratie van de toestellen

- Configureer elk toestel (R1, SW1 en SW2) als volgt:

  - Maak verbinding met de switch via de consolekabel.
  - Geef de switch een naam volgens de opgegeven topologie.
  - Voorkom ongewenste DNS lookups.
  - Stel wachtwoorden in voor de priviliged EXEC mode en de toegang via de consolepoort.
  - Zorg ervoor dat wachtwoorden geëncrypteerd zijn in de configuratie.
  - Stel de volgende MOTD (= Message Of The Day) banner in: `Toegang enkel voor bevoegden!`.

- Bewaar de configuratie zodat deze niet verloren raakt bij een `reload` en test dit uit.
- :question: Hoe toon je de huidige configuratie?
- :question: Hoe toon je de IOS-versie?

### Stap 4 - IPv4

#### Stap 4.1 - Opstellen van het IPv4 adresseringsschema

> :warning: **Let op:** Je gebruikt dezelfde adresseringsschema's binnen jouw groep. Dat maakt het bv. eenvoudiger om elkaars problemen op te sporen, enz.

- Bepaal het te subnetten netwerk en dus het **netwerkadres** a.d.h.v.:

  - een random gegenereerd IPv4-adres via <https://commentpicker.com/ip-address-generator.php>;
  - een random gegenereerde prefixlengte via <https://www.random.org/integers/?num=1&min=8&max=24&col=5&base=10&format=html&rnd=new>;

  - :warning: **Let op:** Kies een geen prefixlengte /8, /16 of /24.

- Verdeel dit netwerk in 4 subnetten van **gelijke grootte**.
- Geef voor elk subnet (Vergeet dit niet op te nemen in het verslag!):
  - het netwerkadres
  - het broadcastadres
  - het subnetmask
  - het maximum aantal uitdeelbare hostadressen.
- Vul onderstaande tabel aan. Je mag zelf de IPv4-adressen kiezen waar mogelijk.

| **Toestel** | **Interface** | **Subnetnr.** | **IPv4-adres** | **Subnetmask** | **IPv4-adres default gateway** |
| ----------- | ------------- | ------------- | -------------- | -------------- | ------------------------------ |
| PC1         | NIC           | 0             |                |                |                                |
| PC2         | NIC           | 0             |                |                |                                |
| PC3         | NIC           | 1             |                |                |                                |
| PC4         | NIC           | 1             |                |                |                                |
| SW1         | VLAN 1        | 0             |                |                |                                |
| SW2         | VLAN 1        | 1             |                |                |                                |
| R1          | G0/0/0        | 0             |                |                | n.v.t.                         |
| R1          | G0/0/1        | 1             |                |                | n.v.t.                         |

#### Stap 4.2 - Configuratie van de router

- Configureer elke interface met:
  - Het correcte IPv4-adres.
  - Een beschrijving die aanduidt met welke switch de interface verbonden is:
    - `LAN to SW1`
    - `LAN to SW2`
- Bewaar de configuratie

#### Stap 4.3 - Configuratie van de switches

- Stel de SVI (= Switch Virtual Interface) in met het correcte IPv4 adres.
- Stel de default gateway in.

#### Stap 4.4 - Configuratie van de PC's

- Stel voor elke PC het statisch IPv4-adres, het subnetmask en de default gateway in.

#### Stap 4.5 - Testen van de verbindingen

Duidt in de volgende tabel aan met `ja` of `nee` of je kan pingen tussen de toestellen:

| **Van/naar** | **PC1** | **PC2** | **SW1** | **R1 (G0/0/0)** | **R2 (G0/0/1)** | **SW2** | **PC3** | **PC4** |
| ------------ | ------- | ------- | ------- | --------------- | --------------- | ------- | ------- | ------- |
| PC1          | n.v.t.  |         |         |                 |                 |         |         |         |
| PC2          |         | n.v.t.  |         |                 |                 |         |         |         |
| SW1          |         |         | n.v.t.  |                 |                 |         |         |         |
| SW2          |         |         |         |                 |                 | n.v.t.  |         |         |
| PC3          |         |         |         |                 |                 |         | n.v.t.  |         |
| PC4          |         |         |         |                 |                 |         |         | n.v.t.  |

- :question: Waarom geeft de eerste ping soms een `Request timed out` foutmelding terwijl de volgende drie wel lukken?

### **Stap 5 - IPv6**

#### Stap 5.1 - Opstellen van het IPv6 adresseringsschema

> :warning: **Let op:** Je gebruikt dezelfde adresseringsschema's binnen jouw groep. Dat maakt het bv. eenvoudiger om elkaars problemen op te sporen, enz.

Er bestaan verschillende types IPv6-adressen zoals link-local adressen (LLA's), global unicast adressen (GUA's). We moeten minstens die twee types configureren op onze interfaces.

- :question:Wat is het verschil tussen een LLA en een GUA en wat is hun functie?

#### Toekenning van link-local adressen (LLAs)

- De PC's hebben zelf al een link-local adres gegenereerd van zodra IPv6 geactiveerd werd.
  - :question:Welk proces wordt er in Packet Tracer gebruikt om de interface ID van dit link-local adres te genereren en toon aan hoe je dit kan zien?
- Voor de interfaces G0/0/0 en G0/0/1 op router R1 gebruiken we FE80::1 als link-local adres.
  - :question:Verklaar waarom je aan beide interfaces op R1 hetzelfde link-local adres kan toekennen.

#### Toekenning van global unicast adressen (GUAs)

Een IPv6-adres bestaat uit 3 delen:

![IPv6 adres opbouw](<img/cisco/IPv6 Packet.png>)

Om de IPv6 adressen van de toestellen te bepalen gaan we als volgt te werk:

**a) Global Routing Prefix (48 bits of 3 hextetten)**

- Gebruik voor de 2 eerste hextetten:  
  `2001:db8:`

  > Deze GUA adresrange mag enkel gebruikt worden voor documentatie, voorbeelden en simulaties zoals Packet Tracer. (zie RFC3849)
  >
  > Indien je met fysieke aparatuur werkt, gebruik je de global prefix die je ISP je toekent (Bekijk zeker eens thuis welke IPv6 prefix je krijgt van je ISP).  
  > Als je geen IPv6 adres krijgt (zoals op het HOGENT netwerk) kan je gebruik maken van ULA's.
  >
  > - :question: Wat is het verschil tussen ULA's en GUA's?
  > - :question: Met welke types IPv4-adressen kan je deze 2 soorten IPv6-adressen vergelijken?

- Genereer voor het 3e hextet een random hexadecimaal getal bestaande uit 4 cijfers via <https://www.browserling.com/tools/random-hex>

**b) Subnet ID (16 bits of 1 hextet)**

- Het 4e hextet wordt gebruikt voor het aanmaken van subnetten.
  - :question:Hoeveel subnetten kunnen we dus maken?
  - :question:Hoeveel hosts kan elk van die subnetten bevatten? (Vergelijk dit aantal nu eens met het totale aantal IPv4-adressen.)
- Je mag je subnet-ID vrij kiezen, maar maak het jezelf zo eenvoudig mogelijk.

**c) Interface ID (64 bits of 4 hextetten)**

- De laatste 4 hextetten vormen de interface-ID. Het identificatienummer van je NIC binnen het subnet.
- Je mag de interface-IDs voor de router en switches zelf kiezen, maar maak het jezelf ook hier niet nodeloos moeilijk.
- De adressen van de PC's laten we hen zelf aanmaken. Dit is 1 van de troeven van IPv6.

  - :question:Hoe heet het proces waarbij een host eigenhandig zijn GUA samenstelt zonder tussenkomst van een DHCP-server?

- Vul onderstaande tabel aan met de IPv6 adressen van de switches en de router. De adressen van de PC's vul je straks aan met de adressen die ze voor zichzelf hebben gecreëerd.

| **Toestel** | **Interface** | **Subnet** | **IPv6-adres (GUA)** | **IPv6-adres (LLA)** | **IPv6-prefixlengte** | **IPv6-adres default gateway** |
| ----------- | ------------- | ---------- | -------------------- | -------------------- | --------------------- | ------------------------------ |
| PC1         | NIC           | 0          |                      |                      | /64                   |                                |
| PC2         | NIC           | 0          |                      |                      | /64                   |                                |
| PC3         | NIC           | 1          |                      |                      | /64                   |                                |
| PC4         | NIC           | 1          |                      |                      | /64                   |                                |
| SW1         | VLAN 1        | 0          |                      |                      | /64                   |                                |
| SW2         | VLAN 1        | 1          |                      |                      | /64                   |                                |
| R1          | G0/0/0        | 0          |                      |                      | /64                   | n.v.t.                         |
| R1          | G0/0/1        | 1          |                      |                      | /64                   | n.v.t.                         |

#### Stap 5.2 - Activeer IPv6 op alle toestellen

IPv6 ondersteuning staat standaard niet aan op de Cisco apparatuur en moet dus eerst geactiveerd worden.

- Doe dit op de routers met het commando

```cisco
Router(config)#ipv6 unicast-routing
```

- Op de switches gebruik je volgende commando's:

```cisco
Switch# configure terminal
Switch(config)# sdm prefer dual-ipv4-and-ipv6 default
Switch(config)# end
Switch# copy running-config startup-config
Switch# reload
```

#### Stap 5.3 - Configureer de router

Stel voor elke interface van de router het correcte LLA- en GUA-adres in.

#### Stap 5.4 - Configureer de switches

- Stel het correcte IPv6-adres in op de SVI (= Switch Virtual Interface).
- Voor IPv6 heb je geen commando om een default gateway in te stellen maar moet je een statische default route instellen in de global configuration mode als volgt:

  ```cisco
  Switch(config)# ipv6 route ::/0 <GUA van de gateway van het netwerk waartoe de switch behoort>
  # bv.: ipv6 route ::/0 2001:db8:8057:1::1
  ```

#### Stap 5.5 - Configureer de PC's

We laten de PC's zichzelf een adres toewijzen. Zet hiervoor de IPv6 configuratie op `Auto` en als alles goed is geconfigureerd zie je automatisch een IPv6 adres verschijnen. Ook de default gateway wordt automatisch ingevuld.

:question: Is dit een LLA of een GUA?

Vul deze adressen in, in de IPv6-tabel uit **stap 5.1**

**Je hebt met IPv6 dus geen administrator of DHCP nodig om je PC's met elkaar te laten communiceren.**

- :question:Welke instelling missen we wel nog om te kunnen surfen op het World Wide Web?

#### Stap 5.5 - Testen van de verbindingen

Duidt in de volgende tabel aan met `ja` of `nee` of je kan pingen tussen de toestellen. Ditmaal uiteraard met de IPv6-adressen.

| **Van/naar** | **PC1** | **PC2** | **SW1** | **R1 (G0/0/0)** | **R2 (G0/0/1)** | **SW2** | **PC3** | **PC4** |
| ------------ | ------- | ------- | ------- | --------------- | --------------- | ------- | ------- | ------- |
| PC1          | n.v.t.  |         |         |                 |                 |         |         |         |
| PC2          |         | n.v.t.  |         |                 |                 |         |         |         |
| SW1          |         |         | n.v.t.  |                 |                 |         |         |         |
| SW2          |         |         |         |                 |                 | n.v.t.  |         |         |
| PC3          |         |         |         |                 |                 |         | n.v.t.  |         |
| PC4          |         |         |         |                 |                 |         |         | n.v.t.  |

### Stap 6 - De routeringstabel

- Hoe toon je de **routeringstabel** op een Cisco router?
  - :question:Hoeveel routes zijn aangeduid met `C`? Wat betekent dit?
  - :question:Hoeveel routes zijn aangeduid met `L`? Wat betekent dit?
  - :question:Hoe kan je de IP-adressen van de interfaces zien (IPv4 en IPv6) en welke interfaces up of down zijn?
  - :question:Hoe kan je de MAC-adressen terugvinden van de interfaces?
- Een default gateway hoeft niet geconfigureerd te worden op een router.
  - :question:Waarom niet?
  - :question:Wanneer zou je in de plaats hiervan wel een **default route** configureren?

### Stap 7 - Instellen SSH-toegang

Configureer de switches en router als volgt:

- Stel het domein `selabs.local` in voor het toestel.
- Genereer een 2048 bits RSA-sleutelpaar.
- Zorg ervoor dat SSH versie 2 wordt gebruikt.
- Configureer een lokale gebruiker voor SSH.
- Activeer SSH op de VTY lines, maar geen telnet
  - :question: Waarom schakelen we telnet uit?
- Configureer de login methode zodat de credentials van de lokale gebruiker opgevraagd worden bij het tot stand brengen van een SSH-verbinding.
- Bewaar de configuratie zodat deze niet verloren raakt bij een `reload` van het toestel.
- Test uit of je met elk toestel een SSH-verbinding tot stand kan brengen. Gebruik het SSH-commando (bv. `ssh -l admin 192.168.1.1`). Duid in de volgende tabel aan met `ja` of `nee` of de SSH-verbinding tussen de toestellen lukt:

| **Van/naar** | **SW1** | **R1 (G0/0/0)** | **R1 (G0/0/1)** | **SW2** |
| ------------ | ------- | --------------- | --------------- | ------- |
| PC1          |         |                 |                 |         |
| PC3          |         |                 |                 |         |

- :question:Werkt SSH ook met IPv6?
  - Tip: voer een `reload` uit op R1, SW1 en SW2 alvorens dit te testen
- :question:Wat is de "SSH timeout" en "maximum authentication retries". Hoe stel ik deze in op 60 seconden en 4 retries?

### Stap 8 - Reflectie

- Welke subnetting (IPv4 of IPv6) was voor jou het eenvoudigst uit te voeren? Waarom?
- Wat was voor jou de moeilijkste stap van de gehele opdracht?
