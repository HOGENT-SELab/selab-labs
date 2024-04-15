# Opdracht 6 - Shoot the trouble

In de vorige opdrachten hebben we al verschillende servers opgezet, waaronder een databankserver, een webserver, een Vaultwarden wachtwoordkluis en Portainer. Deze servers werden geïmplementeerd met behulp van kant-en-klare stappenplannen die jullie eenvoudig konden volgen.

In deze opdracht starten we met een machine waarop verschillende configuratiefouten zijn opgetreden. Het is aan jullie om deze fouten op te sporen en te corrigeren, zodat de machine volledig operationeel is voor de demonstratie.

## :mortar_board: Leerdoelen

- Je kan een systematische aanpak hanteren om problemen te detecteren en op te lossen.
- Je kan de kennis die je hebt opgedaan in de voorgaande opdrachten toepassen om problemen op te lossen.
- Je kan een gegeven virtuele machine opzetten en configureren volgens de gewenste eindsituatie.

## :memo: Evaluatiecriteria

Toon na afwerken het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze opdracht! Criteria voor beoordeling:

- [ ] Er is een volledig werkende virtuele machine volgens de eindsituatie.
- [ ] Je hebt een verslag gemaakt op basis van het template.
  - [ ] Het verslag bevat een duidelijke beschrijving van de problemen die je hebt gevonden mét de oplossingen.
- [ ] De cheat sheet werd aangevuld met nuttige commando's die je wenst te onthouden voor later.

## Probleemstelling

Tijdens het uitvoeren van de vorige opdrachten hebben jullie waarschijnlijk al gemerkt dat niet alles van de eerste keer lukt en dat bepaalde zaken niet werken zoals ze zouden moeten. Dit is vergelijkbaar met situaties die je kan tegenkomen in het bedrijfsleven, waarbij je geconfronteerd wordt met problemen die moeten worden opgelost door fouten op te sporen en te corrigeren.

Troubleshooting is dan ook een essentiële vaardigheid voor toekomstige systeembeheerders, en in deze opdracht willen we jullie kennis laten maken met deze vaardigheid. Om deze opdracht succesvol af te ronden, zul je een systematische aanpak moeten hanteren om de mogelijke problemen te detecteren en in een logische volgorde op te lossen. Het document [debugging-selab.md](../cheat-sheets/debugging-selab.md) kan je hierbij helpen.

Het is zeer belangrijk om alle kennis toe te passen die je in de voorgaande opdrachten hebt opgedaan. Veel succes!

## Opdracht

### Voorbereiding

Maak een nieuwe VM aan met volgende specificaties:

- 1 CPU
- 4 GB RAM
- 126 MB display memory
- GEEN HDD, we koppelen deze later
- 2 netwerkadapters:
  - #1: NAT
  - #2: Host-only adapter gekoppeld aan 192.168.56.1/24 netwerk met DHCP van 192.168.56.100-192.168.56.254

Download een van de aangepaste 'kapotte' harde schijven van de virtuele machine (.VDI):
- <insert link broken one>
- <insert link broken two>
- <insert link broken three>
- <insert link broken four>
- <insert link broken five>

**Er zijn 5 verschillende schijven voorzien dus iedereen neemt een andere schijf binnen zijn groep.** Koppel deze bij e door jou niuew aangemaakte VM in Virtualbox. Op de VDI is **Ubuntu 22.04 LTS** voorgeïnstalleerd.

:warning: De VM bevat geen **GEEN** GUI, enkel de CLI (Command Line Interface) is beschikbaar. De toetsenbordindeling is QWERTY US (Dit mag je in VM aanpassen indien nodig)

### Beginsituatie

In elke machine zijn **precies vijf basisfouten**, fouten in verband met reeds uitgevoerde labo's, aangebracht en **één extra fout** voor een **nieuwe service Planka** (https://planka.app/). **Alle vereiste pakketten zijn reeds geïnstalleerd.** Het is ook niet de bedoeling om alles opnieuw handmatig te installeren en te configureren, zoals reeds in de opdrachten werd gedaan, maar om gericht te zoeken naar wat niet (goed) werkt. Alle bestanden in verband met de docker containers vind je in de VM in de map of submappen van `~/docker`.

Volgende accounts werden reeds **correct** aangemaakt:

| Service             | Username                      | Password                             |
| ------------------- | ----------------------------- | ------------------------------------ |
| Ubuntu              | trouble                       | shoot                                |
| SSH                 | trouble                       | shoot                                |
| MariaDB<br /><br /> | admin<br />appusr<br />wpuser | letmein!<br />letmein!<br />letmein! |
| Wordpress           | wpuser                        | letmein!                             |
| Planka              | troubleshoot@selab.hogent.be  | shoot                                |
| Portainer           | admin                         | troubleshoot                         |

Volgende accounts moet je zelf nog aanmaken, **dit is dus geen fout!**, eens alles goed geconfigureerd is:

| Service     | Username                      | Password |
| ----------- | ----------------------------- | -------- |
| Minetest    | trouble                       | shoot    |
| Vaultwarden | troubleshoot@selabs.hogent.be | shoot    |

Volgende poorten werden opgesteld/gekoppeld (Dit moet gecontroleerd worden!):

- HTTP: 80
- HTTPS: 443
- MySQL: 3306
- Planka: 3000
- Portainer: 9443
- SSH: 22
- Vaultwarden: 4123

### Afwijking ten op zichte van labo's

Omdat zoals hierboven vermeld er geen GUI voorzien is zijn volgende instellingen anders of niet gebeurd zoals in de labo's:

- Statisch ip: dit is gebeurd door gebruik te maken van `netplan`. Lees zeker de man-page na voor de werking en configuratie hiervan.
- Automatisch aanmelden en screenlock werden niet ingesteld en moeten ook niet ingesteld worden. Deze zijn geen onderdeel van het labo.
- Aangezien we geen domeinnaam hebben draait Wordpress niet op https maar http, dus zonder ssl.

### Gewenste eindsituatie

Het doel is om ervoor te zorgen dat de virtuele machine aan het einde van de opdracht de volgende diensten correct aanbiedt:

- Netwerk
  - Het toestel beschikt over internet
  - Het toestel kan via externe host gepingd worden op 192.168.56.20.
- Webserver (apache2)
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20>.
  - Het is mogelijk om via de Ubuntu gebruiker bestanden naar de webserver (in map`/www/data`) te uploaden via FileZilla (of een gelijkaardige tool) vanuit de hostomgeving via 192.168.56.20, poort 22 (via SFTP). ⚠️ Je overschrijft echter niet het door ons aangeleverde `index.html` bestand.
- Databankserver (mariadb)
  - Databank `appdb` moet bereikbaar zijn via MySQL Workbench in de hostomgeving via 192.168.56.20, poort 3306 voor de gebruiker `appusr` en het wachtwoord `letmein!`.
  - Moet alleen lokaal toegankelijk zijn vanaf de VM zelf via het MySQL-commando voor de gebruiker `admin` en het wachtwoord `letmein!` en via de MySQL Workbench maar enkel dan via een SSH connectie.
- Wordpress
  - Moet bereikbaar zijn via de browser in de hostomgeving via <http://192.168.56.20:8080> voor de gebruiker `wpuser` en het wachtwoord `letmein!` en gebruikt de database `wpdb`.
  - Er moet een post aangemaakt zijn (met inhoud naar keuze)
- SSH
  - Er moet een verbinding gemaakt kunnen worden via ssh van buitenaf naar 192.168.56.20 op poort 22 voor de gebruiker `trouble` en het wachtwoord `shoot`.
- Docker
  - Vaultwarden, Minetest en Portainer draaien via Docker Compose, net als in opdracht 5.
    - Vaultwarden en minetest gebruiken lokale mappen voor data
    - Portainer gebruikt een docker volume voor zijn data
  - Beide pagina's zijn extern bereikbaar via een beveiligde verbinding en kunnen op ingelogd worden:
    - Portainer: <https://192.168.56.20:9443>
    - Vaultwarden: <https://192.168.56.20:4123>
  - Minetest is mogelijk om spel te joinen door minetest client te gebruiken op de host via <https://192.168.56.20:30000> voor de gebruiker `trouble` en het wachtwoord `shoot`.
  - Planka draait via een aparte docker compose serivce (~/docker/planka) en is bereikbaar via https://192.168.56.20:3000 voor de gebruiker `admin` en het wachtwoord `troubleshoot`.

#### Schermafbeeldingen eindsituatie

| ![Apache2](./img/troubleshoot/troubleshoot_apache.png) |
| :----------------------------------------------------: |
|                   Figuur 1. Apache2.                   |

| ![Wordpress](./img/troubleshoot/troubleshoot_wordpress.png) |
| :---------------------------------------------------------: |
|        Figuur 2. Wordpress met zelf aangemaakte post        |
