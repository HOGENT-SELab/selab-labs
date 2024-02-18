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

### Beginsituatie

Download de aangepaste 'kapotte' virtuele machine vanaf Chamilo voor jouw groep en importeer deze in Virtualbox. In elke machine zijn **precies vijf fouten** aangebracht. **Alle vereiste pakketten zijn reeds geïnstalleerd.** Het is ook niet de bedoeling om alles opnieuw handmatig te installeren en te configureren, zoals reeds in de opdrachten is gedaan, maar om gericht te zoeken naar wat niet (goed) werkt.

De VM heeft volgende specificaties:

- 1 CPU
- 4 GB RAM
- 126 MB display memory
- 50 GB dynamische HDD
- Ubuntu 22.04 LTS
  - **GEEN** GUI, enkel CLI (Command Line Interface)
  - Toetsenbordindeling is QWERTY US (Dit mag je in VM aanpassen indien nodig)

Volgende accounts werden aangemaakt:

- Ubuntu & SSH:
  - Gebruikersnaam: `trouble`
  - Wachtwoord: `shoot`
- MySQL:
  - Gebruikersnaam: `mariadb`
  - Wachtwoord: `letmein!`
  - Gebruikersnaam: `appusr`
  - Wachtwoord: `letmein!`
  - Gebruikersnaam: `wpuser`
  - Wachtwoord: `letmein!`
- Wordpress
  - Gebruikersnaam: `wpuser`
  - Wachtwoord: `letmein!`
- Vaultwarden:
  - Gebruikersnaam: `troubleshoot@selabs.hogent.be`
  - Wachtwoord: `troubleshoot`
- Portainer:
  - Gebruikersnaam: `admin`
  - Wachtwoord: `troubleshoot`

Volgende poorten werden opgesteld/gekoppeld (Dit moet gecontroleerd worden!):

- HTTP: 80
- HTTPS: 443
- MySQL: 3306
- SSH: 22
- Portainer: 9443
- Vaultwarden: 4123

### Gewenste eindsituatie

Het doel is om ervoor te zorgen dat de virtuele machine aan het einde van de opdracht de volgende diensten correct aanbiedt:

- Netwerk
  - Het toestel beschikt over internet
  - Het toestel kan via externe host gepingd worden op 192.168.56.20.
- Webserver (apache2)
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20>.
  - Het is mogelijk om via de Ubuntu gebruiker bestanden naar de webserver (`/www/data`) te uploaden via FileZilla (of een gelijkaardige tool) in de hostomgeving via 192.168.56.20, poort 22 (via SFTP).
- Databankserver (mariadb)
  - Moet bereikbaar zijn via MySQL Workbench in de hostomgeving via 192.168.56.20, poort 3306 voor de gebruiker `appusr` en het wachtwoord `letmein!`.
  - Moet alleen toegankelijk zijn vanaf de VM zelf via het MySQL-commando voor de gebruiker `mariadb` en het wachtwoord `letmein!`.
- Wordpress
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20/wordpress> voor de gebruiker `wordpressapp` en het wachtwoord `letmein!` en gebruikt de database `wordpressdb`.
- SSH
  - Er moet een verbinding gemaakt kunnen worden via ssh van buitenaf naar 192.168.56.20 op poort 22 voor de gebruiker `trouble` en het wachtwoord `shoot`.
- Docker
  - Vaultwarden, Minetest en Portainer draaien via Docker Compose, net als in opdracht 5.
    - Vaultwarden en minetest gebruiken lokale mappen voor data
    - Portainer gebruikt een docker volume voor zijn data
  - Beide pagina's zijn extern bereikbaar via een beveiligde verbinding en kunnen op ingelogd worden:
    - Portainer: <https://192.168.56.20:9443>
    - Vaultwarden: <https://192.168.56.20:4123>
  - Minetest is mogelijk om spel te joinen via <https://192.168.56.20:30000>

#### Schermafbeeldingen eindsituatie

| ![Apache2](./img/troubleshoot/troubleshoot_apache.png) |
| :----------------------------------------------------: |
|                   Figuur 1. Apache2.                   |

| ![Wordpress](./img/troubleshoot/troubleshoot_wordpress.png) |
| :---------------------------------------------------------: |
|                    Figuur 2. Wordpress.                     |
