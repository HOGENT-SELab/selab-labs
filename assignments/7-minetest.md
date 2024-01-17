# Opdracht 7 - Een Minetest server opzetten <!-- omit in toc -->

## Inhoud <!-- omit in toc -->
- [Inleiding](#inleiding)
- [Probleemstelling](#probleemstelling)
- [Opdracht](#opdracht)
  - [Stap 1 - Aanmaken Ubuntu Server VM](#stap-1---aanmaken-ubuntu-server-vm)
  - [Stap 2 - Installeer de Minetest server](#stap-2---installeer-de-minetest-server)
  - [Stap 3 - Start Minetest bij systeemopstart](#stap-3---start-minetest-bij-systeemopstart)
- [Evaluatie](#evaluatie)


## Inleiding

In de vorige labo's hebben we al heel wat servers opgezet: een databankserver, een webserver, een Vaultwarden wachtwoordkluis en Portainer. In dit labo zal je een Minetest server opzetten.

Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze labo-opdracht!

## Probleemstelling

Velen van jullie zullen de term "server" voor het eerst gehoord hebben bij multiplayer games. De server is het toestel waarop een match/wereld/... gehost wordt. De server zorgt er ook voor dat gamers samen kunne spelen door hen te joinen in deze match/wereld/... In dit labo zullen we een Minetest server opzetten. Minetest is een open source Minecraft clone en is volledig gratis te downloaden op <https://www.minetest.net/>.

| ![Minetest](./img/minetest/minetest.png) |
| :--------------------------------------: |
|           Figuur 1. Minetest.            |

## Opdracht

### Stap 1 - Aanmaken Ubuntu Server VM

Maak een Ubuntu Server VM. **Let op!** Dit is niet hetzelfde als de standaard Ubuntu VM die we tot nu toe gebruikt hebben. Ubuntu Server heeft geen GUI: alles gebeurt in een terminal met tekst. Dit wordt ook zo gedaan in de bedrijfswereld. Een server heeft geen GUI nodig; dit verspilt toch enkel CPU- en GPU-kracht.

Zoek op <https://www.osboxes.org/> een VirtualBox image voor Ubuntu Server. Het versienummer speelt hierbij geen grote rol. In serveromgevingen wordt typisch een Long Time Support (LTS) versie gekozen.

- Wat is de laatste LTS-versie van Ubuntu?

**Tip:** je hebt mogelijks Netplan (<https://netplan.io/>) nodig om de netwerkinterfaces te configureren. Zorg ervoor dat configuratie persistent is tussen verschillende boots van de server (het commando `ip` is hiervoor niet geschikt). Gebruik de [documentatie](https://netplan.readthedocs.io/en/latest/) als startpunt. Hier vind je verschillende tutorials, maar ook handige how-to guides.

**Tip:** installeer SSH op de VM. Zo kan je via een terminal op je eigen pc een SSH-verbinding openen naar de server. In de praktijk heb je ook nooit rechtstreeks toegang tot de server. In een VirtualBox server VM kan je ook niet kopiëren/plakken, dit kan je enkel via een SSH-verbinding naar de server doen. Via SSH heb je ook geen last van verkeerde toetsenbordinstellingen.

### Stap 2 - Installeer de Minetest server

Installeer de **dedicated** Minetest server op de Ubuntu Server VM. Je bent vrij om te kiezen hoe de installatie uitgevoerd zal worden. Er zijn diverse manieren om dit doel te bereiken, de ene manier is al wat moeilijker of meer werk dan de andere.

- Wat betekent "dedicated" hier?
- Welke mogelijkheden qua installatie heb je gevonden? Welke heb je gekozen en waarom?

Probeer ook of andere teamleden via een LAN-netwerk kunnen inloggen op de Minetest server zodat jullie samen kunnen spelen. Wat moet je hiervoor aanpassen of instellen? **Let op!** Het schoolnetwerk zal de verbindingen tegenhouden. Als je dit wil uittesten, maak je best even gebruik van een mobiele hotspot op de campus.

### Stap 3 - Start Minetest bij systeemopstart

Zorg ervoor dat de Minetest server gestart wordt telkens als de VM opstart.

Afhankelijk van jouw keuze kan je onderstaande tip al dan niet gebruiken. Er is nl. een oplossing waarbij je geen `systemd` service nodig hebt.

**Tip:** in een oplossing heb je een `systemd` service nodig om de Minetest server te starten bij systeemopstart, net zoals je bijvoorbeeld de `apache2.service` hebt voor een Apache2 server. Meer informatie hierover vind je op <https://manpages.ubuntu.com/manpages/xenial/en/man5/systemd.service.5.html>. Een uitgewerkt voorbeeld vind je bij stap 4 op <https://www.vultr.com/docs/how-to-setup-a-minetest-server-on-ubuntu-17-04/>. **We herhalen:** zijn deze stappen de eenvoudigste/snelste weg naar een werkende Minetest server?

## Evaluatie

Toon na afwerken het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze labo-opdracht! Criteria voor beoordeling:

- Er is een dedicated Minetest server opgezet op een Ubuntu Server VM.
- Er kan op ingelogd worden op deze server vanop het fysiek toestel.
- De Minetest server draait nog steeds na een herstart van de VM, zonder manuele tussenkomst.
- Teamgenoten kunnen binnen hetzelfde LAN-netwerk inloggen op de Minetest server.
  - **Let op!** op het schoolnetwerk wordt dit niet toegestaan. Dit kan wel aangetoond worden via een mobiele hotspot.
- Een degelijk en duidelijk opgemaakt verslag is te vinden op de documentenruimte van de groep. Hieraan staan minstens volgende zaken:
  - Wie heeft wat gedaan (= taakverdeling)?
  - Wie was de verslaggever? Dit is telkens een andere student.
  - De antwoorden op de vragen uit deze opdracht. Noteer alles wat je niet begrijpt zodat je dit kan vragen aan je begeleider.
  - Ervaren struikelblokken mét aanpak om tot een oplossing te komen.
- De cheat sheet werd aangevuld met nuttige commando's die je wenst te onthouden voor later.
