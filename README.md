# Nicheverzekeringen

Statische kennispagina over nicheverzekeringen in Nederland: waarom reguliere
verzekeraars afwijzen, wat een nicheverzekeraar doet, hoe volmacht werkt, en waar
je terechtkunt (de Vereende als nicheverzekeraar, Hera Life als nichevolmacht /
volmacht boutique).

Geen build-step, geen dependencies, geen externe requests, geen cookies.

## Structuur

```
.
├─ index.html                    Hoofdpagina: HTML, CSS en JS in één bestand
├─ colofon.html                  Colofon, disclaimer, Wft-afbakening
├─ privacy.html                  Privacyverklaring (AVG)
├─ toegankelijkheid.html         Toegankelijkheidsverklaring (WCAG 2.2 AA)
├─ 404.html                      Foutpagina
├─ favicon.ico
├─ site.webmanifest
├─ robots.txt
├─ sitemap.xml
├─ llms.txt                      Samenvatting voor taalmodellen (GEO)
├─ CHANGELOG.md
├─ LICENSE                       MIT
├─ .editorconfig
├─ .gitignore
├─ .nojekyll                     Zet Jekyll-verwerking uit op Pages
├─ CNAME.example                 Hernoemen naar CNAME bij eigen domein
├─ assets/
│  ├─ og-image.png               1200×630 sharing-afbeelding
│  ├─ icon-192.png, icon-512.png, apple-touch-icon.png
│  └─ fonts/                     Hier je gelicentieerde TT Norms Pro woff2's
├─ .well-known/security.txt
└─ .github/workflows/pages.yml   Auto-deploy naar GitHub Pages
```

## Voor publicatie invullen

Twee placeholders staan door de repo heen. Zoek en vervang:

| Placeholder | Waar | Vervang door |
|---|---|---|
| `GEBRUIKERSNAAM` | `index.html`, `robots.txt`, `sitemap.xml`, `security.txt` | Je GitHub-gebruikersnaam of je eigen domein |
| `VUL IN` / `VUL-IN@VOORBEELD.NL` | `colofon.html`, `privacy.html`, `index.html`, `security.txt` | Bedrijfsgegevens en e-mailadres |

```bash
grep -rn "GEBRUIKERSNAAM\|VUL IN\|VUL-IN" . --include="*.html" --include="*.txt" --include="*.xml"
```

## Lokaal bekijken

```bash
python3 -m http.server 8000   # http://localhost:8000
```

Of open `index.html` direct in de browser; een server is niet nodig.

## Publiceren op GitHub Pages

```bash
git init
git add .
git commit -m "Eerste versie nicheverzekeringen"
git branch -M main
git remote add origin https://github.com/GEBRUIKERSNAAM/nicheverzekeringen.git
git push -u origin main
```

Daarna in GitHub: **Settings → Pages → Source: GitHub Actions**. De workflow
publiceert bij elke push naar `main`.

Eigen domein? Hernoem `CNAME.example` naar `CNAME`, zet je domein erin en maak bij
je DNS een CNAME-record naar `GEBRUIKERSNAAM.github.io`.

## Huisstijl aanpassen

Alle kleuren, fonts en radii staan in één `:root`-blok bovenaan `index.html`
(de subpagina's hebben hetzelfde blok).

De site volgt de huisstijl van Wildschönau Tourismus (re-design 2023, Fabian
Gwiggner): verdonkerde blauw- en oranjetinten, licht afgeronde vormen en het
lettertype **TT Norms Pro** (Sans + Serif, TypeType).

- **De hex-waarden zijn benaderd.** De stylesheet van wildschoenau.com is niet
  uitleesbaar; de kleuren zijn afgeleid uit de merkbeschrijving. Haal de exacte
  codes met DevTools (Inspecteren → Computed) en overschrijf ze in `:root`.
- **TT Norms Pro is een betaald lettertype** en zit niet in deze repo. Met een
  webfont-licentie: zet de `.woff2`-bestanden in `assets/fonts/` en haal het
  `@font-face`-blok bovenaan `index.html` uit commentaar. Zonder licentie valt de
  site terug op Avenir Next / Segoe UI en Georgia.
- Wijzig je kleuren, controleer dan het contrast opnieuw (minimaal 4,5:1 voor
  tekst) en werk `toegankelijkheid.html` bij.

## Inhoud aanpassen

De risico-router zit onderaan `index.html` in een klein script. Vragen en
uitkomsten staan in de objecten `Q1`, `Q2` en `ROUTES`; de routeringslogica in
`decide()`. Opslaan en verversen, meer is er niet.

Pas je feitelijke inhoud aan, werk dan ook bij:
- de controledatum in de sectie **Bronnen en verantwoording**;
- de datum bij de bankgarantietarieven;
- de FAQ-antwoorden in het JSON-LD-blok onderaan `index.html` (die staan er dubbel
  in, voor rich results in zoekmachines);
- `CHANGELOG.md` en `<lastmod>` in `sitemap.xml`.

## Toegankelijkheid en privacy

- Skip-link, landmarks, zichtbare toetsenbordfocus, `prefers-reduced-motion`,
  responsief tot 320 px, aparte printstijl.
- Geen cookies, trackers, localStorage of externe requests. Daardoor is er geen
  cookiebanner nodig — dat verandert zodra je analytics, een formulier of
  ingesloten content van derden toevoegt.

## Vindbaarheid: SEO en GEO

**Klassieke SEO**
- Titel en meta description bevatten het kernbegrip; één `<h1>` met "Nicheverzekeringen".
- Eén onderwerp per sectie, met een `<h2>` die de zoekvraag letterlijk beantwoordt.
- Canonical, Open Graph, Twitter card, `max-snippet:-1` en `max-image-preview:large`.
- `sitemap.xml` met `lastmod` en een image-entry; `robots.txt` verwijst ernaar.
- Interne links met beschrijvende ankertekst in plaats van "lees meer".
- Eén bestand zonder externe requests: snel laden helpt de ranking.

**GEO (vindbaarheid in AI-antwoorden)**
- Sectie **In het kort** bovenaan: zes vragen met een zelfstandig leesbaar antwoord.
  Antwoordmachines citeren graag korte, complete alinea's die zonder context kloppen.
- **Woordenlijst** met tien definities, ook als `DefinedTermSet` in JSON-LD.
- JSON-LD-graaf: `WebSite`, `WebPage` (met `speakable`), `Article` (met `about` en
  `mentions`), `DefinedTermSet` en `FAQPage` met acht vraag-antwoordparen.
- Expliciete controledatum bij elke sectie met cijfers, plus een bronsectie. Modellen
  hechten waarde aan dateerbare, herleidbare uitspraken.
- `llms.txt` in de root: een markdownsamenvatting met de kernfeiten, bedoeld voor
  taalmodellen die de site verwerken.
- `robots.txt` staat GPTBot, ClaudeBot, PerplexityBot, Google-Extended en soortgelijke
  crawlers expliciet toe. Wil je juist níet in AI-antwoorden verschijnen, zet die
  regels dan om naar `Disallow`.

**Bijhouden**
- Werk `lastmod` in `sitemap.xml`, `dateModified` in JSON-LD, de datum in `llms.txt` en
  de controledatums in de tekst tegelijk bij.
- Verandert een FAQ-antwoord in de tekst, pas dan ook het JSON-LD-blok aan; die twee
  moeten identiek blijven, anders is het gestructureerde data die niet klopt met de pagina.

## Juridisch — lees dit voor publicatie

Deze site is **informatief**. Het is geen financieel advies, geen aanbod en geen
bemiddeling in de zin van de Wet op het financieel toezicht.

- Zodra de site bezoekers actief naar aanbieders leidt met de bedoeling dat er een
  verzekering tot stand komt (aanvraagformulier, leadgeneratie, affiliate), kan dat
  als **bemiddelen** worden gezien en geldt er een AFM-vergunningplicht.
- Genoemde tarieven, acceptatiegrenzen en volmachten komen uit openbare bronnen,
  gecontroleerd op 23 juli 2026. Houd de controledatum actueel; verouderde premies
  zijn een misleidingsrisico (art. 4:19 Wft).
- De uitspraak dat een gespecialiseerde partij "soms goedkoper" is, is bewust
  generiek gehouden. Koppel die claim niet aan een specifieke aanbieder zonder
  actuele onderbouwing — dan wordt het een vergelijkende claim.
- AFM-vergunningnummers en Kifid-aansluitnummers op de site horen bij de
  betreffende aanbieder, niet bij deze site. Laat dat zo staan.
- Neem geen logo's, beeldmerken of claims van derden over. Kleur en lettertype
  alleen zijn niet beschermd; de combinatie met een logo kan dat wel zijn.
- Vul het colofon in voordat je live gaat (art. 3:15d BW).

## Licentie

Code: MIT (zie `LICENSE`). De teksten mag je hergebruiken en aanpassen; controleer
feiten en tarieven zelf voordat je publiceert.
