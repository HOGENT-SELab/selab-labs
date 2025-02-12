# Opdracht 6 - Shoot the trouble

In de vorige opdrachten hebben we verschillende servers opgezet, waaronder een databankserver, een webserver, een Vaultwarden wachtwoordkluis en Portainer. Deze servers werden geïmplementeerd met behulp van kant-en-klare stappenplannen die jullie eenvoudig konden volgen.

In deze opdracht starten we met een machine waarop verschillende configuratiefouten zijn opgetreden. Het is aan jullie om deze fouten op te sporen en te corrigeren, zodat de machine volledig operationeel is voor de demonstratie.

## :mortar_board: Leerdoelen

- Je kan een systematische aanpak hanteren om problemen te detecteren en op te lossen.
- Je kan de kennis die je hebt opgedaan in de voorgaande opdrachten toepassen om problemen op te lossen.
- Je kan een gegeven virtuele machine opzetten en configureren volgens de gewenste eindsituatie.

## :bar_chart: Evaluatiecriteria

Toon na het afronden het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze opdracht! Beoordelingscriteria:

- [ ] Er is een volledig werkende virtuele machine volgens de eindsituatie.
  - [ ] De VM heeft toegang tot internet en kan gepingd worden op 192.168.56.20.
  - [ ] De webserver is beschikbaar op <https://192.168.56.20> met de nodige SFTP-mogelijkheden.
  - [ ] De databank is beschikbaar via MySQL Workbench op 192.168.56.20:3306 (`appusr letmein!`).
  - [ ] De WordPress-website is beschikbaar via <http://192.168.56.20:8080> (`wpuser letmein!`).
  - [ ] De VM is bereikbaar via SSH op 192.168.56.20:22 (`trouble shoot`).
  - [ ] De Docker services zijn correct geconfigureerd:
    - [ ] Vaultwarden is bereikbaar op <https://192.168.56.20:4123>.
    - [ ] Portainer is bereikbaar op <https://192.168.56.20:9443>.
    - [ ] Minetest is bereikbaar op <https://192.168.56.20:30000> (`trouble shoot`).
    - [ ] Planka is bereikbaar op <http://192.168.56.20:3000> (`[trouble OF troubleshoot@selab.hogent.be] shoot`).
- [ ] Je hebt een verslag gemaakt op basis van de template.
  - [ ] Het verslag bevat een duidelijke beschrijving van de gevonden problemen en de oplossingen. **Per type machine is er een aparte beschrijving!**
- [ ] De cheat sheet is aangevuld met nuttige commando's die je wil onthouden.

> Opmerking voor studenten TIAO: elk teamlid toont **individueel alle** evaluatiecriteria met de eigen VM. Individuele extra's worden individueel toegelicht.

## :question: Probleemstelling

Tijdens het uitvoeren van de vorige opdrachten hebben jullie waarschijnlijk al gemerkt dat niet alles in één keer lukt en dat bepaalde zaken niet werken zoals ze zouden moeten. Dit is vergelijkbaar met situaties die je kan tegenkomen in het bedrijfsleven, waarbij je geconfronteerd wordt met problemen die moeten worden opgelost door fouten op te sporen en te corrigeren.

Troubleshooting is dan ook een essentiële vaardigheid voor toekomstige systeembeheerders. In deze opdracht willen we jullie kennis laten maken met deze vaardigheid. Om deze opdracht succesvol af te ronden, zul je een systematische aanpak moeten hanteren om de mogelijke problemen te detecteren en in een logische volgorde op te lossen. Het document [debugging-selab.md](../cheat-sheets/debugging-selab.md) kan je hierbij helpen.

Het is zeer belangrijk om alle kennis toe te passen die je in de voorgaande opdrachten hebt opgedaan. Veel succes!

## :memo: Opdracht

### Voorbereiding

Maak een nieuwe VM aan met de volgende specificaties:

- 1 CPU
- 4 GB RAM
- 128 MB display memory
- **Geen** HDD, deze koppelen we later
- 2 netwerkadapters:
  - #1: NAT
  - #2: Host-only adapter gekoppeld aan het 192.168.56.1/24 netwerk met een DHCP-bereik van 192.168.56.100 tot 192.168.56.254

Download een van de vooraf gemaakte 'defecte' harde schijven van de virtuele machine (.VMDK) van onze [OneDrive](https://hogent.sharepoint.com/:f:/s/DepartementDIT/En_TExvdCDVFit73n9j4HU4BaOVlQRfE1sTlJH4mi5e6wQ?e=aH4h4D).

**Er zijn 5 verschillende schijven beschikbaar, dus iedereen neemt een andere schijf binnen zijn groep.** Koppel deze aan de door jou nieuw aangemaakte VM in VirtualBox. Op de schijf is **Ubuntu 22.04 LTS** voorgeïnstalleerd.

:warning: De VM bevat **geen** GUI, enkel de CLI (Command Line Interface) is beschikbaar. De toetsenbordindeling is QWERTY US (dit mag je in de VM aanpassen indien nodig).

### Beginsituatie

In elke machine zijn **precies vijf basisfouten** aangebracht, fouten in verband met reeds uitgevoerde labo's, en **één extra fout** voor een **nieuwe service Planka** (<https://planka.app/>). **Alle vereiste pakketten zijn reeds geïnstalleerd.** Het is niet de bedoeling om alles opnieuw handmatig te installeren en te configureren, zoals reeds in de opdrachten werd gedaan, maar om gericht te zoeken naar wat niet (goed) werkt. Alle bestanden in verband met de docker containers vind je in de VM in de map `~/docker`.

De volgende accounts zijn reeds **correct** aangemaakt:

| Service   | Gebruikersnaam                 | Wachtwoord   |
| --------- | ------------------------------ | ------------ |
| Ubuntu    | trouble                        | shoot        |
| SSH       | trouble                        | shoot        |
| Wordpress | wpuser                         | letmein!     |
| Planka    | <troubleshoot@selab.hogent.be> | shoot        |
| Portainer | admin                          | troubleshoot |

De volgende accounts moet je zelf nog aanmaken of nakijken, zodra alles goed geconfigureerd is (**dit is dus geen fout!**):

| Service     | Gebruikersnaam                  | Wachtwoord                           |          |
| ----------- | ------------------------------- | ------------------------------------ | -------- |
| Minetest    | trouble                         | shoot                                | aanmaken |
| Vaultwarden | <troubleshoot@selabs.hogent.be> | shoot                                | aanmaken |
| MySQL       | admin<br />appusr<br />wpuser   | letmein!<br />letmein!<br />letmein! | nakijken |

De volgende poorten zijn gekoppeld (dit moet gecontroleerd worden!):

- HTTP: 80
- HTTPS: 443
- Minetest: 30000
- MySQL: 3306
- Planka: 3000
- Portainer: 9443
- SSH: 22
- Vaultwarden: 4123

### Afwijkingen ten opzichte van de labo's

Omdat er, zoals hierboven vermeld, geen GUI is voorzien, zijn de volgende instellingen anders of niet uitgevoerd zoals in de labo's:

- Statisch IP: dit is ingesteld met behulp van `netplan`. Lees zeker de man-page na voor de werking en configuratie hiervan.
- Automatisch aanmelden en screenlock zijn niet ingesteld en hoeven ook niet ingesteld te worden. Deze maken geen deel uit van het labo.
- Aangezien we geen domeinnaam hebben, draait WordPress niet op https maar op http, dus zonder SSL.
- De `docker-compose.yml` voor Portainer/Minetest/Vaultwarden maakt gebruik van variabelen die worden ingevuld via een .env-bestand (ook in de map `~/docker`). De variabelen zijn correct en hoeven dus niet meer aangepast te worden in een van de twee bestanden.
- Planka is geïnstalleerd volgens de installatie-instructies voor Docker Compose die te vinden zijn op de officiële website. De installatie is via een apart Docker Compose bestand (`~/docker/planka/`), dus los van die voor Portainer/Minetest/Vaultwarden. Deze blijven ook gescheiden.
- :warning: Voor Planka is in het Docker Compose bestand de waarde voor `restart: on-failure`, zoals vermeld in de officiële documentatie, aangepast naar `restart: always` omdat dit anders problemen gaf. Laat dit dus ook zo staan. Dit wordt niet als fout beschouwd!

### Gewenste eindsituatie

Het doel is om ervoor te zorgen dat de virtuele machine aan het einde van de opdracht de volgende diensten correct aanbiedt:

- Netwerk
  - De virtuele machine beschikt over internet.
  - De virtuele machine kan via een externe host gepingd worden op 192.168.56.20.
- Webserver (Apache2)
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20>.
  - Het is mogelijk om via de Ubuntu-gebruiker bestanden naar de webserver (in map `/var/www`) te uploaden via FileZilla (of een gelijkaardige tool) vanuit de hostomgeving via 192.168.56.20, poort 22 (via SFTP). ⚠️ Overschrijf echter niet het door ons aangeleverde `index.html` bestand.
- Databankserver (MySQL)
  - De databank `appdb` moet bereikbaar zijn via MySQL Workbench in de hostomgeving via 192.168.56.20, poort 3306 voor de gebruiker `appusr` en het wachtwoord `letmein!`.
  - Moet alleen lokaal toegankelijk zijn vanaf de VM zelf via het MySQL-commando voor de gebruiker `admin` en het wachtwoord `letmein!` en via de MySQL Workbench, maar dan enkel via een SSH-verbinding.
- WordPress
  - Moet bereikbaar zijn via de browser in de hostomgeving via <http://192.168.56.20:8080> voor de gebruiker `wpuser` en het wachtwoord `letmein!` en gebruikt de database `wpdb`.
  - Er moet een post aangemaakt zijn (met inhoud naar keuze).
- SSH
  - Er moet een verbinding gemaakt kunnen worden via SSH van buitenaf naar 192.168.56.20 op poort 22 voor de gebruiker `trouble` en het wachtwoord `shoot`.
- Docker
  - Vaultwarden, Minetest en Portainer draaien via Docker Compose, zoals in opdracht 5.
    - Vaultwarden en Minetest gebruiken lokale mappen voor data.
    - Portainer gebruikt een Docker volume voor zijn data.
  - Beide pagina's zijn extern bereikbaar via een beveiligde verbinding en er kan ingelogd worden via:
    - Portainer: <https://192.168.56.20:9443>
    - Vaultwarden: <https://192.168.56.20:4123>
  - Bij Minetest is het mogelijk om een spel te joinen door de Minetest-client te gebruiken op de host via <https://192.168.56.20:30000> voor de gebruiker `trouble` en het wachtwoord `shoot`.
  - Planka draait via een aparte Docker Compose service (~/docker/planka/) en is bereikbaar via <http://192.168.56.20:3000>, niet via https, voor de gebruiker `trouble` of `troubleshoot@selab.hogent.be` en het wachtwoord `shoot`.

#### Schermafbeeldingen eindsituatie

Zo ziet de webpagina van Apache eruit:

![Apache2](./img/troubleshoot/troubleshoot_apache.png)

Zo ziet de WordPress-website eruit:

![WordPress](./img/troubleshoot/troubleshoot_wordpress.png)

## 🚀 Mogelijke uitbreidingen

Je kan proberen om een applicatie van de [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) lijst op te zetten op jouw virtuele machine. Dit is een lijst van open-source software die je zelf kan hosten. Je kan bijvoorbeeld een blog, een wiki, een chatapplicatie, een CI/CD tool... opzetten. Zoek een applicatie die je interessant vindt en probeer deze op te zetten op jouw VM.
