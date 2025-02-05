# Opdracht 6 - Shoot the trouble

In de vorige opdrachten hebben we al verschillende servers opgezet, waaronder een databankserver, een webserver, een Vaultwarden wachtwoordkluis en Portainer. Deze servers werden geïmplementeerd met behulp van kant-en-klare stappenplannen die jullie eenvoudig konden volgen.

In deze opdracht starten we met een machine waarop verschillende configuratiefouten zijn opgetreden. Het is aan jullie om deze fouten op te sporen en te corrigeren, zodat de machine volledig operationeel is voor de demonstratie.

## 🎓 Leerdoelen

- Je kan een systematische aanpak hanteren om problemen te detecteren en op te lossen.
- Je kan de kennis die je hebt opgedaan in de voorgaande opdrachten toepassen om problemen op te lossen.
- Je kan een gegeven virtuele machine opzetten en configureren volgens de gewenste eindsituatie.

## 📊 Evaluatiecriteria

Toon na afwerken het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze opdracht! Criteria voor beoordeling:

- [ ] Er is een volledig werkende virtuele machine volgens de eindsituatie.
  - [ ] Netwerk: er is internet en het toestel kan gepingd worden op 192.168.56.20
  - [ ] De webserver is beschikbaar op https://192.168.56.20 met nodige SFTP mogelijkheden 
  - [ ] De databank is beschikbaar via MySQL Workbench op 192.168.56.20:3306 (´appusr letmein!´)
  - [ ] De wordpress website is beschikbaar via http://192.168.56.20:8080 (´wpuser letmein!´)
  - [ ] Het toestel is bereikbaar via SSH op 192.168.56.20:22 (´trouble shoot´)
  - [ ] Docker
    - [ ] Vaultwarden is bereikbaar https://192.168.56.20:4123
    - [ ] Portainer is bereikbaar https://192.168.56.20:9443
    - [ ] Minetest is bereikbaar https://192.168.56.20:30000 (`trouble shoot`)
    - [ ] Planka is bereikbaar http://192.168.56.20:3000 (`[trouble OF troubleshoot@selab.hogent.be] shoot`) 
- [ ] Je hebt een verslag gemaakt op basis van de template.
  - [ ] Het verslag bevat een duidelijke beschrijving van de problemen die je hebt gevonden mét de oplossingen. **Per type machine is er een aparte beschrijving!**
- [ ] De cheat sheet is aangevuld met nuttige commando's die je wil onthouden.

## ❓ Probleemstelling

Tijdens het uitvoeren van de vorige opdrachten hebben jullie waarschijnlijk al gemerkt dat niet alles van de eerste keer lukt en dat bepaalde zaken niet werken zoals ze zouden moeten. Dit is vergelijkbaar met situaties die je kan tegenkomen in het bedrijfsleven, waarbij je geconfronteerd wordt met problemen die moeten worden opgelost door fouten op te sporen en te corrigeren.

Troubleshooting is dan ook een essentiële vaardigheid voor toekomstige systeembeheerders. In deze opdracht willen we jullie kennis laten maken met deze vaardigheid. Om deze opdracht succesvol af te ronden, zul je een systematische aanpak moeten hanteren om de mogelijke problemen te detecteren en in een logische volgorde op te lossen. Het document [debugging-selab.md](../cheat-sheets/debugging-selab.md) kan je hierbij helpen.

Het is zeer belangrijk om alle kennis toe te passen die je in de voorgaande opdrachten hebt opgedaan. Veel succes!

## 📝 Opdracht

### Voorbereiding

Maak een nieuwe VM aan met volgende specificaties:

- 1 CPU
- 4 GB RAM
- 128 MB display memory
- **Geen** HDD, we koppelen deze later
- 2 netwerkadapters:
  - #1: NAT
  - #2: Host-only adapter gekoppeld aan 192.168.56.1/24 netwerk met DHCP range van 192.168.56.100 tot 192.168.56.254

Download een van de voorgemaakte 'kapotte' harde schijven van de virtuele machine (.VMDK):

- [Type 1](https://hogent.sharepoint.com/:u:/s/DepartementDIT/EeslQCjABdBKv-0KrRomttgBjxf_lbu-af4xP0S7T9qZ8Q?e=MPaeJe)
- [Type 2](https://hogent.sharepoint.com/:u:/s/DepartementDIT/ETwntn_Fy9pHuv3FXeClDroBxBxB0YOw6xTdZWkAF7fHeQ?e=tgfFbC)
- [Type 3](https://hogent.sharepoint.com/:u:/s/DepartementDIT/EY9R23iC00JHpUrEGz4gV2kBETdGdvYioF5pLQ8dYaM_5w?e=I6wlRS)
- [Type 4](https://hogent.sharepoint.com/:u:/s/DepartementDIT/EbY51tu1QOhDnh_AnU4TIGEBBlOiOTXMrwgXTtSq0ln5jw?e=ABAFYM)
- [Type 5](https://hogent.sharepoint.com/:u:/s/DepartementDIT/EY2MJ4hQbBdGvFWZ4izc3DMBitMzSNGX7by1sfv14Yo0hQ?e=wrlYVf)

**Er zijn 5 verschillende schijven voorzien dus iedereen neemt een andere schijf
binnen zijn groep.** Koppel deze bij de door jou nieuw aangemaakte VM in Virtualbox. Op de schijf is **Ubuntu 22.04 LTS** voorgeïnstalleerd.

:warning: De VM bevat geen **geen** GUI, enkel de CLI (Command Line Interface) is beschikbaar. De toetsenbordindeling is QWERTY US (dit mag je in VM aanpassen indien nodig).

### Beginsituatie

In elke machine zijn **precies vijf basisfouten**, fouten in verband met reeds uitgevoerde labo's, aangebracht en **één extra fout** voor een **nieuwe service Planka** (<https://planka.app/>). **Alle vereiste pakketten zijn reeds geïnstalleerd.** Het is ook niet de bedoeling om alles opnieuw handmatig te installeren en te configureren, zoals reeds in de opdrachten werd gedaan, maar om gericht te zoeken naar wat niet (goed) werkt. Alle bestanden in verband met de docker containers vind je in de VM in de map `~/docker`.

Volgende accounts werden reeds **correct** aangemaakt:

| Service             | Username                       | Password                             |
| ------------------- | ------------------------------ | ------------------------------------ |
| Ubuntu              | trouble                        | shoot                                |
| SSH                 | trouble                        | shoot                                |
| MariaDB<br /><br /> | admin<br />appusr<br />wpuser  | letmein!<br />letmein!<br />letmein! |
| Wordpress           | wpuser                         | letmein!                             |
| Planka              | <troubleshoot@selab.hogent.be> | shoot                                |
| Portainer           | admin                          | troubleshoot                         |

Volgende accounts moet je zelf nog aanmaken, eens alles goed geconfigureerd is (**dit is dus geen fout!**):

| Service     | Username                        | Password |
| ----------- | ------------------------------- | -------- |
| Minetest    | trouble                         | shoot    |
| Vaultwarden | <troubleshoot@selabs.hogent.be> | shoot    |

Volgende poorten werden opengesteld/gekoppeld (dit moet gecontroleerd worden!):

- HTTP: 80
- HTTPS: 443
- Minetest: 30000
- MySQL: 3306
- Planka: 3000
- Portainer: 9443
- SSH: 22
- Vaultwarden: 4123

### Afwijking ten op zichte van labo's

Omdat er, zoals hierboven vermeld, geen GUI voorzien is, zijn volgende instellingen anders of niet gebeurd zoals in de labo's:

- Statisch ip: dit is gebeurd door gebruik te maken van `netplan`. Lees zeker de man-page na voor de werking en configuratie hiervan.
- Automatisch aanmelden en screenlock werden niet ingesteld en moeten ook niet ingesteld worden. Deze zijn geen onderdeel van het labo.
- Aangezien we geen domeinnaam hebben, draait Wordpress niet op https maar http, dus zonder ssl.
- De docker-compose.yml voor Portainer/Mintest/Vaultwarden maakt gebruik van variabelen die opgevuld worden via een .env bestand (ook in de map ∼/docker). De variabelen staan correct en moet je dus niet meer aanpassen noch wijzigen in een van de twee bestanden.
- Planka werd geïnstalleerd volgens de installatie-instructies voor docker compose die terug te vinden zijn op de officiële website. De installatie is via een aparte docker-compose file (~/docker/planka/), dus los van die voor Portainer/Mintest/Vaultwarden. Deze blijven ook gescheiden.
- :warning: Voor planka werd in de docker-compose file de waarde voor `restart: on-failure` zoals die in de officiële documentatie vermeld staat aangepast naar `restart: always` omdat dit anders problemen gaf. Je laat dit dus ook zo staan. Dit is wordt dus niet aanzien als fout!

### Gewenste eindsituatie

Het doel is om ervoor te zorgen dat de virtuele machine aan het einde van de opdracht de volgende diensten correct aanbiedt:

- Netwerk
  - Het toestel beschikt over internet
  - Het toestel kan via externe host gepingd worden op 192.168.56.20.
- Webserver (apache2)
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20>.
  - Het is mogelijk om via de Ubuntu gebruiker bestanden naar de webserver (in map`/var/www`) te uploaden via FileZilla (of een gelijkaardige tool) vanuit de hostomgeving via 192.168.56.20, poort 22 (via SFTP). ⚠️ Je overschrijft echter niet het door ons aangeleverde `index.html` bestand.
- Databankserver (mariadb)
  - Databank `appdb` moet bereikbaar zijn via MySQL Workbench in de hostomgeving via 192.168.56.20, poort 3306 voor de gebruiker `appusr` en het wachtwoord `letmein!`.
  - Moet alleen lokaal toegankelijk zijn vanaf de VM zelf via het MySQL-commando voor de gebruiker `admin` en het wachtwoord `letmein!` en via de MySQL Workbench maar enkel dan via een SSH connectie.
- Wordpress
  - Moet bereikbaar zijn via de browser in de hostomgeving via <http://192.168.56.20:8080> voor de gebruiker `wpuser` en het wachtwoord `letmein!` en gebruikt de database `wpdb`.
  - Er moet een post aangemaakt zijn (met inhoud naar keuze)
- SSH
  - Er moet een verbinding gemaakt kunnen worden via ssh van buitenaf naar 192.168.56.20 op poort 22 voor de gebruiker `trouble` en het wachtwoord `shoot`.
- Docker
  - Vaultwarden, Minetest en Portainer draaien via Docker Compose, zoals in opdracht 5.
    - Vaultwarden en minetest gebruiken lokale mappen voor data
    - Portainer gebruikt een docker volume voor zijn data
  - Beide pagina's zijn extern bereikbaar via een beveiligde verbinding en er kan ingelogd worden via:
    - Portainer: <https://192.168.56.20:9443>
    - Vaultwarden: <https://192.168.56.20:4123>
  - Bij Minetest is het mogelijk om een spel te joinen door de minetest client te gebruiken op de host via <https://192.168.56.20:30000> voor de gebruiker `trouble` en het wachtwoord `shoot`.
  - Planka draait via een aparte docker compose service (~/docker/planka/) en is bereikbaar via <http://192.168.56.20:3000>, niet via https, voor de gebruiker `trouble` of `troubleshoot@selab.hogent.be` en het wachtwoord `shoot`.

#### Schermafbeeldingen eindsituatie

| ![Apache2](./img/troubleshoot/troubleshoot_apache.png) |
| :----------------------------------------------------: |
|                   Figuur 1. Apache2.                   |

| ![Wordpress](./img/troubleshoot/troubleshoot_wordpress.png) |
| :---------------------------------------------------------: |
|        Figuur 2. Wordpress met zelf aangemaakte post        |
