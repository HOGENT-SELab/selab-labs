# Opdracht 3 - Een webserver opzetten in een virtuele omgeving

In de vorige opdracht heb je een databaseserver opgezet in een virtuele machine (VM). In deze opdracht gaan we verder met die VM en rusten we deze uit met een webserver. Het einddoel is om in een webbrowser op het hostsysteem de website te tonen die draait op je VM.

## :mortar_board: Leerdoelen

- Je kan een SSH-server installeren en configureren.
- Je kan een SSH-verbinding opzetten vanaf een fysiek toestel naar een virtuele machine.
- Je kan een webserver opzetten in een virtuele omgeving.
- Je kan bestanden kopiëren naar de Document Root van de webserver.
- Je kan een webserver beveiligen met SSL.
- Je kan een webserver beveiligen met een firewall.
- Je kan een webserver beveiligen met fail2ban.

## :bar_chart: Evaluatiecriteria

Toon na het afronden het resultaat aan je begeleider. Elk teamlid moet in staat zijn om het resultaat te demonstreren bij de oplevering van deze opdracht! Criteria voor beoordeling:

- [ ] Je kan de VM opstarten.
- [ ] Je kan met FileZilla (of een vergelijkbare applicatie) bestanden naar de Document Root van de webserver kopiëren.
- [ ] De website is te zien in een webbrowser op het fysieke systeem via URL <https://192.168.56.20>.
- [ ] Je kan aantonen dat de firewall actief is en dat de juiste poorten zijn toegestaan in de firewall:
  - [ ] Je kan aantonen dat je nog steeds kan verbinden via SSH of SFTP.
  - [ ] Je kan aantonen dat de MySQL Workbench nog steeds kan verbinden met de VM.
  - [ ] Je kan aantonen dat je website nog steeds bereikbaar is.
- [ ] Je kan aantonen dat fail2ban actief is.
- [ ] Je kan de inhoud van het **jail.local** bestand tonen en toelichten.
- [ ] Je kan met de **fail2ban** command line client aantonen dat de **findtime**, **maxretry** en **bantime** juist zijn ingesteld. Je kan deze begrippen toelichten.
- [ ] Je kan aantonen dat je via SSH kan inloggen op de VM vanaf jouw fysieke toestel en dat fail2ban jouw IP-adres blokkeert als je te veel foutieve inlogpogingen doet.
- [ ] Je kan aantonen dat een IP-adres op de whitelist niet wordt geblokkeerd.
- [ ] Je hebt een verslag gemaakt op basis van het template.
- [ ] De cheat sheet is aangevuld met nuttige commando's die je wil onthouden.
- [ ] Je kan een correct antwoord geven op de vragen die zijn aangeduid met een :question:.

> Opmerking voor studenten TIAO: elk teamlid toont een deel van de evaluatiecriteria. Individuele extra's worden individueel toegelicht.

## :question: Probleemstelling

Het opzetten van een webserver is een van de basisvaardigheden van een systeembeheerder. Ook softwareontwikkelaars hebben baat bij kennis over hoe een Linux webserver werkt en opgezet wordt. De meeste webapplicaties draaien immers op een Linux server. Ook bij mobiele applicaties is er meestal sprake van een backend-server in de cloud (voor aanmelden, opslaan van gegevens, enz.).

## :memo: Opdracht

### Stap 1 - Installatie

> **Tip:** Het is verstandig om een snapshot van je VM te maken (de VM met de databaseserver) voordat je aan deze procedure begint. Als er iets misgaat met je VM, kan je altijd terugkeren naar een vorige snapshot.

Voer de volgende stappen uit:

- Installeer de Apache2 HTTP Server op de VM.
- Controleer of de Apache service draait en welke netwerkpoorten in gebruik zijn:
  - :question: Luistert de Apache netwerkservice alleen naar de loopback-interface zoals MySQL? Of is de service meteen ook van buitenaf toegankelijk? Hoe controleer je dit?
  - :question: Zal de Apache service opstarten (enabled) bij het opstarten van de VM? Hoe controleer je dit?
- Controleer _binnen je VM_ of je de standaardwebsite kan zien die op de VM draait:
  - Open een webbrowser en surf naar <http://localhost>, <http://127.0.0.1>, of het host-only IP-adres van je VM (normaal `192.168.56.20`).
  - Lees de informatie op deze website grondig!
- Controleer of je de standaardwebsite kan zien vanaf je fysieke hostsysteem:
  - Open een webbrowser en surf naar het host-only IP-adres van je VM.

:question: Als je op de VM een website wil publiceren, moet je de HTML- en andere bestanden in de zogenaamde **Document Root** zetten. Wat is het pad naar deze map?

### Stap 2 - Een statische website publiceren

In deze stap gaan we een statische website van je fysieke systeem kopiëren naar de VM en ervoor zorgen dat die zichtbaar is in onze webbrowser. Zorg dat je op je fysieke systeem een webpagina of website hebt (bijvoorbeeld uit de OLOD's Web Development) die je kan publiceren op de VM.

Een Linux-systeem is typisch beveiligd zodat je niet zomaar bestanden naar de Document Root kan kopiëren. We geven hier de nodige commando's, waarvan er een aantal reeds aan bod zijn gekomen in het vak Computer Systems. Later in de opleiding leer je meer in detail wat deze precies doen.

Eerst maak je de gebruiker **osboxes** lid van de groep **www-data**:

```bash
sudo usermod -aG www-data osboxes
```

Vervolgens maak je de Document Root eigendom van de groep **www-data**:

```bash
sudo chgrp -R www-data /pad/naar/document/root
```

> **Opgelet**: `/pad/naar/document/root` moet je uiteraard vervangen door het pad naar de Document Root op jouw systeem.

Tenslotte ken je alle leden van de groep **www-data** schrijfrechten toe op de Document Root:

```shell
sudo chmod -R g+w /pad/naar/document/root
```

Om bestanden te kopiëren naar de VM ga je een SSH-server installeren. Mogelijks heb je dit al gedaan in de vorige opdracht. Zo niet, installeer dan OpenSSH met het commando:

```bash
sudo apt install openssh-server
```

:question: Met welke twee commando's kan je controleren of de SSH-server draait, en op welke poort?

Gebruik `systemctl` om de SSH-server op te starten en te activeren indien dit nog niet het geval is.

Op je fysieke systeem open je nu FileZilla (of een vergelijkbare applicatie zoals Cyberduck op macOS). Maak een verbinding met de VM. Hier volgen de instructies voor FileZilla, pas dit zelf aan voor jouw gekozen applicatie:

- Host: `192.168.56.20`
- Gebruikersnaam: `osboxes`
- Wachtwoord: (vul zelf in)
- Poort: (vul zelf het poortnummer van de OpenSSH-server in)
- Klik op `Snelverbinden`
- Als `lokale site` (linkerhelft van het venster) ga je naar de directory met de website die je wil publiceren
- Als `externe site` (rechterhelft) ga je naar de Document Root van Apache.
- Kopieer je website naar de VM

Controleer tenslotte dat de website zichtbaar is in de webbrowser op het fysieke systeem.

> **Pro Tip**: Je kan ook het commando **scp** (_secure copy_) gebruiken om bestanden te kopiëren tussen je host en je VM.

### Stap 3 - Een webserver beveiligen met SSL

In productieomgevingen is het belangrijk dat een publiek toegankelijke webserver voldoende beveiligd is. In een testomgeving zoals onze VM is dat minder van belang, maar we willen toch dat jullie ervan bewust zijn welke minimale beveiligingsinstellingen nodig zijn. We zullen daarom verschillende acties uitvoeren om een basisbeveiliging op onze webserver aan te bieden.

Activeer de **ssl** module voor Apache, zodat clients kunnen verbinden met SSL/TLS:

```bash
sudo a2enmod ssl
sudo a2ensite default-ssl
sudo systemctl reload apache2
```

In de adresbalk van je webbrowser laat je de URL naar de website nu voorafgaan door `https://` in plaats van `http://`. Dit versleutelt de informatie die tussen de webbrowser en de webserver uitgewisseld wordt. Test dit uit, zowel binnen je VM, als vanaf je fysieke systeem.

> **Opgelet:** Je webbrowser zal een waarschuwing geven dat de verbinding niet veilig is. De reden hiervoor is dat het gegenereerde certificaat, dat in principe aantoont dat de website beheerd wordt door een betrouwbare partij, niet ondertekend is door een erkende **Certificate Authority**. In een testomgeving is het niet mogelijk om een officieel certificaat te bekomen. Je mag de waarschuwing dus negeren en doorgaan naar de website.

:question: Welke netwerkpoort wordt gebruikt voor HTTPS? Met welk commando kan je dit opzoeken?

### Stap 4 - Een webserver beveiligen met een firewall

In deze stap ga je een firewall instellen die enkel verkeer doorlaat naar de netwerkpoorten van services die over het netwerk toegankelijk moeten zijn. De firewall op Ubuntu wordt beheerd via het commando **ufw** (Uncomplicated FireWall).

De firewall in Linux draait op kernelniveau, waar het packet filtering systeem **netfilter** heet. Traditioneel gebruikte men de **iptables** commando's om netfilter te configureren, maar **ufw** biedt een eenvoudigere interface.

Een firewall gaat dus netwerkpakketten filteren nog voor ze ooit de applicatie bereiken. Een applicatie kan een TCP/IP poort open hebben staan, terwijl de netfilter geconfigureerd is om pakketten naar deze poort te laten vallen. Op die manier is de service onbereikbaar. Omgekeerd kan ook: de netfilter laat de pakketten door, terwijl de applicatie niet op de juiste poort en/of interface luistert. Wanneer "het niet werkt" moet je dus zowel controleren dat de firewall de pakketten doorlaat, als controleren dat de service op de juiste poort luistert, en misschien best ook even kijken of de service nog steeds draait.

Voer deze stappen uit:

1. Bepaal welke netwerkpoorten gebruikt worden voor resp. SSH, HTTP, HTTPS en MySQL.
2. Zoek op hoe je via het commando **ufw** de firewall kan activeren en activeer deze.
3. Zorg ervoor dat het verkeer op de poorten uit stap 1 door de firewall toegelaten wordt.
4. Test of alle netwerkdiensten nog bereikbaar zijn vanop je fysieke systeem.
5. :question: Met welk commando kan je de status van de firewall met een overzicht van alle toegelaten poorten opvragen?

> **Opmerking**: Vaak merken we dat studenten die een firewall instellen zeggen dat ze een bepaalde poort "open gezet" hebben. We willen erop wijzen dat deze terminologie eigenlijk niet klopt. Een "open poort" betekent dat er een service actief is en luistert op een bepaalde poort. Als je een firewall instelt, dan laat je verkeer toe naar die poort. Beide staan los van elkaar. Je kan in je firewall-instellingen verkeer doorlaten naar een gesloten poort (omdat de service niet draait). Let op de correcte terminologie en verwar beide begrippen niet!

### Stap 5 - Een webserver beveiligen met fail2ban

Elke server op het internet loopt voortdurend risico om aangevallen te worden. Een vaak voorkomende aanval is een **brute force attack**: een programma probeert alle mogelijke combinaties van letters, cijfers en andere tekens om het wachtwoord van een account te raden. Deze programma's worden ook wel bots genoemd en proberen in te loggen als `root`, `admin` of andere vaak voorkomende accounts. Om dit te voorkomen gaan we **fail2ban** installeren en configureren.

Fail2ban detecteert mislukte inlogpogingen op verschillende soorten services. Wanneer er vanuit een bepaald IP-adres te veel foutieve aanmeldpogingen gebeuren, herkent fail2ban dit als een aanval en wordt dit IP-adres voor een bepaalde tijd geblokkeerd. In deze opdracht gaan we fail2ban gebruiken om onze SSH-toegang te bewaken.

#### Installatie

- Installeer **fail2ban** via **apt**.
- Gebruik **systemctl** om fail2ban op te starten bij het starten van de VM.
  - :question: Hoe kan je opzoeken of dit correct gebeurd is?

#### Configuratie van een jail

- Kopieer het bestand **/etc/fail2ban/jail.conf** naar **/etc/fail2ban/jail.local**. In dit **jail.local** bestand plaatsen we alle instellingen voor onze **jails**. Jails zijn verzamelingen van alle IP-adressen die we blokkeren.

- Verwijder de inhoud van dit bestand en begin met de volgende eenvoudige configuratie:

  ```ini
  [sshd]
  port    = ssh
  logpath = %(sshd_log)s
  backend = %(sshd_backend)s
  ```

- :question: Zoek op wat je met de volgende parameters kan bereiken:

  - **findtime**
  - **maxretry**
  - **bantime**

  Deze informatie is terug te vinden in een man-pagina. Zoek deze.

- Configureer fail2ban zodat het een IP-adres blokkeert bij 6 foutieve aanmeldpogingen via SSH, binnen een tijdspanne van 3 minuten. Het IP-adres wordt dan voor 15 minuten geblokkeerd.

- Herstart fail2ban om de nieuwe instellingen te activeren.

#### Testen

- Probeer aan te melden via SSH vanaf jouw fysieke toestel. Test eerst of je met de juiste aanmeldgegevens kan inloggen (bv. via FileZilla).
- Log nu terug uit en probeer meermaals in te loggen met een fout wachtwoord. Normaal zal fail2ban jou blokkeren als je te veel foutieve pogingen onderneemt.
  - Hoe ervaar je dit?
  - Geeft SSH je nog iets van toelichting?
- :question: Zoek op hoe je de fail2ban command line client kan gebruiken om de volgende vragen te beantwoorden:
  - Hoe kan je zien welke jails geconfigureerd zijn?
  - Hoe kan je zien welke IP-adressen geblokkeerd zijn?
  - Hoe kan je de **findtime**, **maxretry** en **bantime** opvragen van de **sshd** jail?
  - Hoe kan je jouw IP-adres terug vrijmaken zonder te wachten tot de blokkeertijd verlopen is?

#### Uitzondering toevoegen

Soms wil je dat bepaalde IP-adressen nooit geblokkeerd worden. Je kan dit adres dan **whitelisten**.

- Voeg een extra VM toe. Je kan hiervoor een nieuwe VDI downloaden (dit mag ook een andere versie of distributie zijn), of de bestaande image dupliceren met behulp van de **Virtual Media Manager** tool in VirtualBox.
- Ken deze VM alleen een host-only adapter (of host-only network op macOS) toe en dus geen NAT.

  ![Host-Only adapter](./img/webserver/hostonly.png)

- Stel het IP-adres van deze VM in op `192.168.56.30`, zoals eerder beschreven in [Opdracht 2](https://github.com/HOGENT-SELab/selab-labs/blob/main/opdrachten/2-databankserver.md#stap-2---virtuele-machine-aanmaken).
- Verifieer dat je vanuit deze VM kan pingen naar de VM met je webserver en fail2ban (normaliter `192.168.56.20`).
- Zoek in de documentatie van fail2ban hoe je een IP-adres kan whitelisten, en doe dit voor het adres `192.168.56.30`. Herstart daarna fail2ban.

Normaal kan je nu zoveel foutieve inlogpogingen doen als je wil, fail2ban zal deze VM niet blokkeren. Als je foutieve inlogpogingen probeert vanaf een andere VM of jouw fysieke toestel, zal fail2ban deze wel blokkeren.

## :rocket: Mogelijke uitbreidingen

### Hydra

Wil je eens kijken hoe fail2ban zich gedraagt met een aanvalstool? Zorgt fail2ban voor voldoende beveiliging? Je kan de tool Hydra loslaten op jouw VM om dit te valideren. Enkele tutorials vind je op:

- <https://www.linuxfordevices.com/tutorials/linux/hydra-brute-force-ssh>
- <https://linuxconfig.org/ssh-password-testing-with-hydra-on-kali-linux>
- En nog veel meer op YouTube, Google, ... . Gebruik de zoektermen "ssh", "hydra", "brute force", ...

:question: Er is zelfs nog een betere manier om brute force tools en bots totaal geen kans te geven. Weet je welke manier? Hoe kan je dit instellen?

### Awesome selfhosted

Je kan ook proberen om een applicatie van de [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) lijst op te zetten op jouw virtuele machine. Dit is een lijst van open-source software die je zelf kan hosten. Je kan bijvoorbeeld een blog, een wiki, een chatapplicatie, een CI/CD tool... opzetten. Zoek een applicatie die je interessant vindt en probeer deze op te zetten op jouw VM.
