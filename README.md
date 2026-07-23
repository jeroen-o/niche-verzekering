# Nicheverzekeringen

Statische kennispagina over nicheverzekeringen in Nederland: waarom reguliere
verzekeraars afwijzen, wat een nicheverzekeraar doet, hoe volmacht werkt, en waar
je terechtkunt (de Vereende als nicheverzekeraar, Hera Life als nichevolmacht /
volmacht boutique).

E�n bestand, geen build-step, geen dependencies, geen externe API's.

## Inhoud

| Bestand | Doel |
|---|---|
| `index.html` | De volledige site: HTML, CSS en JS in één bestand |
| `404.html` | Foutpagina voor GitHub Pages |
| `robots.txt` | Indexatieregels |
| `sitemap.xml` | Sitemap (pas de URL aan) |
| `.github/workflows/pages.yml` | Automatische deploy naar GitHub Pages |
| `CNAME.example` | Sjabloon voor een eigen domein |

## Lokaal bekijken

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Of open `index.html` gewoon in de browser — er is geen server nodig.

## Publiceren op GitHub Pages

```bash
git init
git add .
git commit -m "Eerste versie nicheverzekeringen"
git branch -M main
git remote add origin https://github.com/GEBRUIKERSNAAM/nicheverzekeringen.git
git push -u origin main
```

Daarna in GitHub: **Settings → Pages → Source: GitHub Actions**. De workflow in
`.github/workflows/pages.yml` publiceert bij elke push naar `main`.

Eigen domein? Hernoem `CNAME.example` naar `CNAME`, zet je domein erin en richt
bij je DNS een CNAME-record in naar `GEBRUIKERSNAAM.github.io`.

## Huisstijl aanpassen

Alle kleuren, fonts en radii staan in één `:root`-blok bovenaan `index.html`.

De site volgt de huisstijl van Wildschönau Tourismus (re-design 2023, Fabian
Gwiggner): verdonkerde blauw- en oranjetinten, licht afgeronde vormen en het
lettertype **TT Norms Pro** (Sans + Serif, TypeType).

- **Kleuren zijn benaderd.** Vervang de hex-waarden in `:root` door de exacte
  merkkleuren zodra je die hebt.
- **TT Norms Pro is een betaald lettertype** en zit niet in deze repo. Heb je een
  webfont-licentie? Zet de `.woff2`-bestanden in `assets/fonts/` en haal het
  `@font-face`-blok bovenaan `index.html` uit commentaar. Zonder licentie valt de
  site terug op Avenir Next / Segoe UI en Georgia.

## Inhoud aanpassen

De risico-router zit onderaan `index.html` in een klein script. Vragen en
uitkomsten staan in de objecten `Q1`, `Q2` en `ROUTES`; de routeringslogica in
`decide()`. Geen build-step nodig: opslaan en verversen.

## Toegankelijkheid en privacy

- Responsief tot mobiel, zichtbare toetsenbordfocus, `prefers-reduced-motion`
  wordt gerespecteerd.
- Geen cookies, geen tracking, geen localStorage, geen externe requests. Daardoor
  is er geen cookiebanner nodig.

## Juridisch — lees dit voor publicatie

Deze site is **informatief**. Het is geen financieel advies, geen aanbod en geen
bemiddeling in de zin van de Wet op het financieel toezicht.

- Zodra de site bezoekers actief naar aanbieders leidt met de bedoeling dat er een
  verzekering tot stand komt (aanvraagformulier, leadgeneratie, affiliate), kan dat
  als **bemiddelen** worden gezien en geldt er een AFM-vergunningplicht.
- Genoemde tarieven, acceptatiegrenzen en volmachten komen uit openbare bronnen en
  kunnen zijn gewijzigd. Overweeg per bedrag een controledatum te vermelden;
  verouderde premies zijn een misleidingsrisico (art. 4:19 Wft).
- AFM-vergunningnummers en Kifid-aansluitnummers op de site horen bij de
  betreffende aanbieder, niet bij deze site. Laat dat zo staan.
- Neem geen logo's, beeldmerken of claims van derden over. Kleur en lettertype
  alleen zijn niet beschermd; de combinatie met een logo kan dat wel zijn.
- Vul een eigen impressum/contactblok in voordat je live gaat.

## Licentie

Code: MIT (zie `LICENSE`). De inhoudelijke teksten mag je vrij hergebruiken en
aanpassen; controleer feiten en tarieven zelf voordat je publiceert.
