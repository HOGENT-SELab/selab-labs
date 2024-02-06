# Verslagen

Deze map bevat alle verslagen van de opdrachten, geschreven in [Markdown](https://guides.github.com/features/mastering-markdown/).

**Correcte Markdown is vrij eenvoudig, dus neem de moeite om het te leren!** Een goede teksteditor zoals Visual Studio Code biedt ondersteuning voor het schrijven van Markdown (bv. HTML-preview, controleren van codeerstijl, opschoning van tabellen, enz.). Maak hier gebruik van, zodat je zeker weet dat wanneer je je rapporten naar GitHub pusht, ze correct zijn opgemaakt.

Kopieer het bestand `verslag-template.md` naar een nieuw bestand voor elke opdracht, bijvoorbeeld `1-package-managers.md` voor de eerste opdracht.

**Houd (per student) een cheat sheet bij met alle commando's die je regelmatig gebruikt.** Dit zal je helpen als je je een bepaald commando niet kunt herinneren tijdens een demo, of wanneer je aan je opdrachten werkt.

## Opmaaktips

- Je kan beginnen met het leren van Markdown door [deze gids](https://guides.github.com/features/mastering-markdown/) van GitHub te lezen.
- De GitHub-documentatie heeft een uitgebreide [sectie over Markdown](https://docs.github.com/en/github/writing-on-github) en de specifieke uitbreidingen van de standaard Markdown-syntax.
- Je kan ook de [oorspronkelijke documentatie over Markdown](https://daringfireball.net/projects/markdown/) lezen.

### Maak geen schermafbeeldingen van terminalsessies

Het invoegen van afbeeldingen kost tijd en is volledig onnodig in het geval van interactie met een op tekst gebaseerde terminal. Markdown heeft een functie genaamd [fenced code blocks](https://docs.github.com/en/github/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks). Kopieer eenvoudig de tekst in de terminal en plak deze in je Markdown-document. Als je de taal van de code specifiëert, wordt syntax-highlighting ingeschakeld.

Hier is een voorbeeld. Controleer zowel de broncode als hoe deze wordt weergegeven in bv. de preview van VS Code of GitHub!

```console
$ vagrant status
Huidige machinestatussen:

dockerlab                 actief (virtualbox)

De VM is actief. Om deze VM te stoppen, kun je `vagrant halt` uitvoeren om
het krachtig af te sluiten, of je kunt `vagrant suspend` uitvoeren om eenvoudigweg
de virtuele machine op te schorten. In beide gevallen, om het opnieuw te starten,
voer eenvoudig `vagrant up` uit.
```

Het voordeel is dat dit minder ruimte inneemt dan een afbeelding, en je kan nog steeds de commando's kopiëren/plakken in een terminal!

### Afbeeldingen invoegen

Je kan afbeeldingen invoegen met de volgende code:

```markdown
![alternatieve tekst](pad/naar/afbeelding.jpg)
```

Vervang "alternatieve tekst" door een beschrijving van de afbeelding (eigenlijk een bijschrift). Het pad naar de afbeelding zelf wordt gespecificeerd tussen de haakjes `()`. Merk op dat je relatieve paden kan gebruiken. Maak een submap met bijvoorbeeld de naam `img` om alle schermafbeeldingen en afbeeldingen op te slaan die je in je verslag wil opnemen. Een goede teksteditor helpt je bij het voltooien van het pad naar de afbeelding. Bijvoorbeeld in VS Code: begin met het typen van de naam van je map met afbeeldingen en druk op `Ctrl+Spatie`. Het toont een keuzelijst met een overzicht van alle afbeeldingen, inclusief een voorbeeld.

### Opmaak van tabellen

Markdown-tabellen worden opgemaakt met het "pipe-symbool", `|`, bijvoorbeeld:

```markdown
|     Lorem      | ipsum dolor                        |
| :------------: | :--------------------------------- |
|    zit amet    | markdownum exclamant renarrant     |
| obvius admissa | Dryopen cognita desectum *et modo* |
```

De weergegeven versie ziet eruit als:

|     Lorem      | ipsum dolor                        |
| :------------: | :--------------------------------- |
|    zit amet    | markdownum exclamant renarrant     |
| obvius admissa | Dryopen cognita desectum *et modo* |

Het is niet verplicht om de pipe-symbolen uit te lijnen. Als je alle spaties verwijdert, wordt het exact hetzelfde weergegeven. Natuurlijk is een mooi uitgelijnde tabel leesbaarder. Maak je geen zorgen, een goede teksteditor kan Markdown-tabellen formatteren en de pipe-symbolen uitlijnen. In VS Code zal bv. `Alt+Shift+F` het huidige document opnieuw formatteren (`Ctrl+Shift+I` op Linux). Raadpleeg de documentatie van de *Markdown All in One*-extensie voor meer informatie.
