# Opdracht 8 - Shoot the trouble <!-- omit in toc -->

## Inhoud <!-- omit in toc -->

- [Inleiding](#inleiding)
- [Probleemstelling](#probleemstelling)
- [Opdracht](#opdracht)
  - [Beginsituatie](#beginsituatie)
  - [Gewenste eindsituatie](#gewenste-eindsituatie)
- [Evaluatie](#evaluatie)

## Inleiding

In de vorige labo's hebben we al verschillende servers opgezet, waaronder een databankserver, een webserver, een Vaultwarden wachtwoordkluis en Portainer. Deze servers werden geïmplementeerd met behulp van kant-en-klare stappenplannen die jullie eenvoudig konden volgen.

In dit labo starten we met een machine waarop verschillende configuratiefouten zijn opgetreden. Het is aan jullie om deze fouten op te sporen en te corrigeren, zodat de machine volledig operationeel is voor de demonstratie.

## Probleemstelling

Tijdens het uitvoeren van de vorige labo's hebben jullie waarschijnlijk al gemerkt dat niet alles van de eerste keer lukt en dat bepaalde zaken niet werken zoals ze zouden moeten. Dit is vergelijkbaar met situaties die je kan tegenkomen in het bedrijfsleven, waarbij je geconfronteerd wordt met problemen die moeten worden opgelost door fouten op te sporen en te corrigeren.

Troubleshooting is dan ook een essentiële vaardigheid voor toekomstige systeembeheerders, en in dit labo willen we jullie kennis laten maken met deze vaardigheid. Om dit labo succesvol af te ronden, zul je een systematische aanpak moeten hanteren om de mogelijke problemen te detecteren en in een logische volgorde op te lossen.

Het is dus belangrijk om alle kennis toe te passen die je in de voorgaande labo's hebt opgedaan. Veel succes!

## Opdracht

### Beginsituatie

Download de aangepaste 'kapotte' virtuele machine vanaf Chamilo voor jouw groep en importeer deze in Virtualbox. In elke machine zijn **precies vijf fouten** aangebracht. **Alle vereiste pakketten zijn reeds geïnstalleerd.** Het is ook niet de bedoeling om alles opnieuw handmatig te installeren en te configureren, zoals reeds in de labs is gedaan, maar om gericht te zoeken naar wat niet goed werkt.

**Lector info** 

Mogelijke fouten:

- Netwerk
  - Geen host-only netwerkadapter
  - Foute configuratie host-only-adapter
  - Host-only adapter niet ingeschakeld
- Firewall
  - Poorten van bepaalde service niet "geopend"
- Webserver
  - Service apache2 niet enabled
  - Rechten foutief ingesteld op /www/data
- Databankserver
  - Service mariadb2 niet enabled
  - Foutieve rechten voor gebruiker mariadb (enkel conn op localhost) of wordpressdb (enkel extern)
  - Databank Wordpressdb niet aangemaakt
  - Gebruiker wordpressapp niet aangemaakt
- Wordpress
  - Foute configuratiegegevens
  - Installatiepagina niet uitgevoerd
- SSH
  - Service niet enabled
  - Poort niet correct ingesteld
- Docker
  - Service docker niet enabled
  - Docker compose file van Vaultwarden of Portainer leeg, foute poorten, containers omgewisseld van naam, geen ssl

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
- Vaultwarden en Portainer draaien via Docker Compose, net als in labo 5. Beide pagina's zijn extern bereikbaar via een beveiligde verbinding:
  - Portainer: <https://192.168.56.20:8080>
  - Vaultwarden: <https://192.168.56.20:9443>

## Evaluatie

Toon na afloop het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze labo-opdracht. De beoordeling zal plaatsvinden aan de hand van de volgende criteria:

- Er is een volledig werkende virtuele machine volgens de eindsituatie.
- Er is een duidelijk en goed opgemaakt verslag beschikbaar op de documentenruimte van de groep. Dit verslag omvat minimaal de volgende informatie:
  - Een opsomming van de gevonden fouten
  - Per gevonden fout:
    - Uitgevoerde stappen om ze te vinden
    - Uitgevoerde stappen om de fout recht te zetten
    - Een beschrijving van de stappen die zijn ondernomen om deze fouten te vinden.
- De cheat sheet werd aangevuld met nuttige commando's die je wenst te onthouden voor later.
