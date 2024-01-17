# Debugging in System Engineering Lab

Soms werkt jouw oplossing voor SELab niet zoals je zou willen, of soms werkt het helemaal niet. In dit document vind je een stappenplan om te vinden waar het probleem zich zou kunnen bevinden. Om te begrijpen wat er mis gaat, moet je eerst begrijpen hoe het systeem werkt. Lees daarom eerst aandachtig de opgave en de bijhorende documentatie.

> Doorloop eerst alle stappen voor je meteen stap 8 onderneemt. Wat is stap 8? Lees eerst stap 1 t.e.m. 7!

## 1. Netwerkinstellingen

### VirtualBox

Controleer of je de juiste adapters hebt

- Adapter 1: NAT
- Adapter 2: Host-only Adapter
  
Controleer of de Host-only adapter de juiste instellingen heeft en dat exact deze adapter is geselecteerd als adapter 2 van de virtuele machine.

- IPv4 adres: 192.168.56.1
- IPv4 subnetmask: 255.255.255.0
- DHCP-server: inggeschakeld
  - Server adres: 192.168.56.100
  - Server mask: 255.255.255.0
  - Laagste adres: 192.168.56.101
  - Hoogste adres: 192.168.56.254

### Virtuele machine

Controleer of de host-only adapter (`enp0s8`) is ingeschakeld en IP adres 192.168.56.20 heeft.

## 2. ping

Controleer of je kan pingen van de host naar de virtuele machine.

```bash
ping 192.168.56.20
```

Kan je niet pingen en heb je de correcte instellingen? Zet de adapter in de virtuele machine uit en weer aan.

Op Windows kan je proberen om de adapter aan en uit te zetten via de adapterinstellingen in het configuratiescherm van Windows.

## 3. Service checken

Als je iets debugt wat gebruik maakt van een service, controleer dan of de service wel aanstaat.

```bash
systemctl status <service>
```

In de uitvoer zou `active (running)` moeten staan. Indien dit niet het geval is, ga dan verder met de volgende stappen.

## 4. Logs

Mogelijks zie je onderaan het vorige commando een foutmelding. Lees deze en probeer te begrijpen wat er mis is.

Zie je daar niets, dan kan je de logs bekijken via:

- het commando `journalctl` (lees de man-pagina voor meer informatie)
- bestanden in `/var/log` (zoek naar de juiste bestanden voor jouw service)
- mogelijks andere bestanden, afhankelijk van de service (zoek online naar mogelijke locaties)

Begrijp je de foutmelding niet? Zoek dan online naar mogelijke oplossingen.

## 5. Socket checken

Ziet alles er goed uit, maar werkt het nog steeds niet? Controleer dan of de service wel op de juiste interface/poort luistert.

```bash
sudo ss -tlnp
```

## 6. Firewall

Mogelijks is de firewall de boosdoener. Controleer of de firewall aanstaat en of de juiste poorten toegelaten zijn.

```bash
sudo ufw status verbose
```

Indien niet, voeg de poorten toe:

```bash
sudo ufw allow in <poort>/<protocol>
```

## 7. Authenticatie probleem?

Moet je aanmelden om toegang te krijgen tot een service en krijg je een *Access denied* foutmelding? Dan is het waarschijnlijk een authenticatie probleem: foutief wachtwoord, foutieve gebruikersnaam...

Zoek online naar mogelijkheden om bv. het wachtwoord van een gebruiker te resetten.

## 8. Geen idee?

Heb je geen idee wat er mis is? Vraag dan hulp aan jouw begeleider. Vraag geen hulp alvorens je alle vorige stappen hebt doorlopen. Noteer ook bij elke stap wat je hebt gedaan, wat de uitvoer was, wat je bevindingen zijn...
