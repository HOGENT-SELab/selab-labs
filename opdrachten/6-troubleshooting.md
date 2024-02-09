# Opdracht 6 - Shoot the trouble

In de vorige opdrachten hebben we al verschillende servers opgezet, waaronder een databankserver, een webserver, een Vaultwarden wachtwoordkluis en Portainer. Deze servers werden geïmplementeerd met behulp van kant-en-klare stappenplannen die jullie eenvoudig konden volgen.

In deze opdracht starten we met een machine waarop verschillende configuratiefouten zijn opgetreden. Het is aan jullie om deze fouten op te sporen en te corrigeren, zodat de machine volledig operationeel is voor de demonstratie.

## :mortar_board: Leerdoelen

TODO: Leerdoelen formuleren

## :memo: Evaluatiecriteria

Toon na afwerken het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze opdracht! Criteria voor beoordeling:

- [ ] Er is een volledig werkende virtuele machine volgens de eindsituatie.
- [ ] Je hebt een verslag gemaakt op basis van het template.
- [ ] De cheat sheet werd aangevuld met nuttige commando's die je wenst te onthouden voor later.

## Probleemstelling

Tijdens het uitvoeren van de vorige opdrachten hebben jullie waarschijnlijk al gemerkt dat niet alles van de eerste keer lukt en dat bepaalde zaken niet werken zoals ze zouden moeten. Dit is vergelijkbaar met situaties die je kan tegenkomen in het bedrijfsleven, waarbij je geconfronteerd wordt met problemen die moeten worden opgelost door fouten op te sporen en te corrigeren.

Troubleshooting is dan ook een essentiële vaardigheid voor toekomstige systeembeheerders, en in deze opdracht willen we jullie kennis laten maken met deze vaardigheid. Om deze opdracht succesvol af te ronden, zul je een systematische aanpak moeten hanteren om de mogelijke problemen te detecteren en in een logische volgorde op te lossen.

Het is dus belangrijk om alle kennis toe te passen die je in de voorgaande opdrachten hebt opgedaan. Veel succes!

## Opdracht

### Beginsituatie

Download de aangepaste 'kapotte' virtuele machine vanaf Chamilo voor jouw groep en importeer deze in Virtualbox. In elke machine zijn **precies vijf fouten** aangebracht. **Alle vereiste pakketten zijn reeds geïnstalleerd.** Het is ook niet de bedoeling om alles opnieuw handmatig te installeren en te configureren, zoals reeds in de labs is gedaan, maar om gericht te zoeken naar wat niet goed werkt.

### Gewenste eindsituatie

Het doel is om ervoor te zorgen dat de virtuele machine aan het einde van de opdracht de volgende diensten correct aanbiedt:

- Webserver (apache2)
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20>.
  - Het is mogelijk om bestanden naar de webserver (`/www/data`) te uploaden via FileZilla in de hostomgeving via 192.168.56.20, poort 22 (via SFTP).
- Databankserver (mariadb)
  - Moet bereikbaar zijn via MySQL Workbench in de hostomgeving via 192.168.56.20, poort 3306 voor de gebruiker `mariadb` en het wachtwoord `letmein!`.
  - Moet alleen toegankelijk zijn vanaf de VM zelf via het MySQL-commando voor de gebruiker `wordpressapp` en het wachtwoord `wordpressapp`.
- Wordpress
  - Moet bereikbaar zijn via de browser in de hostomgeving via <https://192.168.56.20/wordpress> en gebruikt de database `wordpressdb`.
- Er moet een verbinding gemaakt kunnen worden via ssh van buitenaf naar 192.168.56.20 op poort 22 voor de gebruiker `vmextra` en het wachtwoord `vmextra`.
- Vaultwarden en Portainer draaien via Docker Compose, net als in opdracht 5. Beide pagina's zijn extern bereikbaar via een beveiligde verbinding:
  - Portainer: <https://192.168.56.20:8080>
  - Vaultwarden: <https://192.168.56.20:9443>
