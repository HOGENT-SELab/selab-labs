# System Engineering Lab - Opdrachten

Deze repository bevat de opdrachten voor het vak System Engineering Lab, dat deel uitmaakt van de [Bachelor Toegepaste Informatica](https://www.hogent.be/opleidingen/bachelors/toegepaste-informatica/) aan [HOGENT](https://www.hogent.be/).

Het doel van deze opdrachten is om vertrouwd te raken met concepten zoals Linux, (container) virtualisatie, netwerken en cloud computing.

## Teamleden

Lijst alle teamleden op met hun GitHub gebruikersnaam:

| Name      | GitHub username                         |
| :-------- | :-------------------------------------- |
| Student 1 | [username](https://github.com/username) |
| Student 2 | [username](https://github.com/username) |
| Student 3 | [username](https://github.com/username) |
| Student 4 | [username](https://github.com/username) |
| Student 5 | [username](https://github.com/username) |

## Inhoudstafel

- `opdrachten/` bevat alle opdrachten.
- `cheat-sheets/` bevat de cheat sheets en checklists per student. Dit bevat ook een handleiding om een probleem tijdens de opdrachten te debuggen.
- `opvolging/` bevat de verslagen van de opvolgingsgesprekken (lector vult deze aan).
- `verslagen/` bevat de verslagen van de opdrachten (jullie maken deze).

## Help, ik heb een mac

De nieuwe Apple Silicon processoren zorgen tijdens de opdrachten van System Engineering Lab  wel eens voor problemen aangezien deze gebruik maken van de ARM-architectuur. De virtuele machines die o.a. voor dit OLOD gebruikt worden, gebruiken deze architectuur niet. Hierdoor is het iets meer werk om de virtuele machines aan te maken, maar het is wel mogelijk.

Er zijn drie opties om virtuele machines aan te maken op macbooks met Apple Silicon:

- **UTM (voorkeur)**: <https://mac.getutm.app/>
  - Dit is gratis te downloaden via de website, in de App Store wordt er \$ 9,99 voor gevraagd. Als je de developers wil bedanken voor hun werk, download je via de App Store. In het andere geval via de website.
  - Dit is momenteel de **voorkeursoplossing**.
- Parallels: <https://www.parallels.com/nl/>
  - Dit is geen gratis software en kost wel wat.
  - Er geldt 50% korting voor studenten: <https://www.parallels.com/nl/landingpage/pd/education/>.
- VirtualBox for ARM: <https://www.virtualbox.org/wiki/Testbuilds>
  - In de toekomst zou dit de voorkeursoplossing moeten worden, maar momenteel is deze nog onstabiel.

### Ubuntu draaien in UTM

1. Download het ISO-bestand voor Ubuntu Desktop LTS voor ARM architecturen via <https://cdimage.ubuntu.com/jammy/daily-live/pending/>.
2. Volg de stappen uit de documentatie van UTM onder **Creating a new virtual machine**: <https://docs.getutm.app/guides/ubuntu/#creating-a-new-virtual-machine>.
   - In deze stappen spreekt men wel over een Ubuntu Server ISO-bestand, dit vervang je logischerwijs door het gedownloade Ubuntu Desktop ISO-bestand.
   - Stap 7 mag je overslaan.
3. Na het doorlopen van deze 9 stappen, heb je een werkende Ubuntu Desktop virtuele machine.

## License information

The assignment and all documentation are shared under the [Creative Commons Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/) license. All code (both scaffolding and testing code) is subject to the MIT license. See [LICENSE.md](LICENSE.md) for details.

Questions and remarks about this assignment are welcome (use the Issues), as well as improvements, fixes, etc. (you can submit a Pull Request). However, technical support on getting the setup working, or on solving the assignment is reserved to students take the courses for which it was developed.
