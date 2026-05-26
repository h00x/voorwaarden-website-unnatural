# voorwaarden.unnatural.nl

Statische website met de algemene voorwaarden van Unnatural Concepts.

## Structuur

```
.
├── index.html              Root: redirect naar huidige versie
├── 2026-05/                Versie mei 2026 (permanent)
│   ├── index.html          HTML-weergave
│   └── voorwaarden.pdf     PDF-download
├── archief/
│   └── index.html          Overzicht van alle versies
├── render.yaml             Render.com deployment config
└── README.md
```

## Het principe: versies zijn onveranderlijk

Elke uitgebrachte versie van de voorwaarden krijgt een eigen permanente URL onder
`/<jaar>-<maand>/`. Eenmaal gepubliceerd wordt deze inhoud **nooit meer gewijzigd**.
Klanten waarmee een overeenkomst is gesloten kunnen op deze manier altijd de versie
raadplegen die op dat moment van toepassing was.

Wijzigingen leiden tot een nieuwe versie op een nieuwe URL.

## Een nieuwe versie publiceren

1. **Maak een nieuwe map** met de datum in YYYY-MM formaat, bijvoorbeeld `2027-03/`.
2. **Plaats de nieuwe PDF** in die map als `voorwaarden.pdf`.
3. **Kopieer de HTML** van de vorige versie naar de nieuwe map en pas de inhoud aan:
   - Werk de tekst aan waar nodig
   - Vervang alle vermeldingen van de oude versie (titel, banner, meta-data, footer)
   - Werk `<link rel="canonical">` bij
4. **Update de root** `index.html`: pas de redirect en canonical aan zodat deze naar
   de nieuwe versie wijzen.
5. **Update `archief/index.html`**: voeg een nieuwe `version-card` toe bovenaan,
   verplaats de `current`-klasse en status-badge naar de nieuwe versie.
6. **Update `render.yaml`**: voeg een cache-regel toe voor de nieuwe versiepad.
7. **Commit en push** — Render deployt automatisch.

## Deployment op GitHub Pages

Als je liever GitHub Pages gebruikt (gratis, geen Render-account nodig):

1. In de GitHub repo: **Settings → Pages**.
2. Source: `Deploy from a branch`, branch: `main`, folder: `/ (root)`.
3. Voeg een `CNAME`-bestand toe in de root met als inhoud: `voorwaarden.unnatural.nl`.
4. Bij je DNS: CNAME-record `voorwaarden` → `<jouw-username>.github.io`.
5. GitHub Pages regelt automatisch HTTPS via Let's Encrypt.

Let op: GitHub Pages ondersteunt geen custom headers, dus de cache-config uit
`render.yaml` werkt daar niet. Voor een document dat zelden wijzigt is dat geen groot
probleem.

## Lokaal testen

```bash
# Python 3
python3 -m http.server 8000

# Node.js
npx serve .

# Open http://localhost:8000
```

## Verwijzen vanaf je hoofdwebsite

Op `unnatural.nl` (in de footer bijvoorbeeld):

```html
<a href="https://voorwaarden.unnatural.nl/2026-05/">Algemene voorwaarden</a>
```

## Verwijzen vanuit offertes

Gebruik in offertes een formulering die zowel de versie als de URL benoemt:

> *Op deze offerte zijn de algemene voorwaarden van Unnatural Concepts van toepassing,
> versie mei 2026, permanent te raadplegen op
> https://voorwaarden.unnatural.nl/2026-05/. Een kopie is bijgevoegd.*

Stuur daarnaast de PDF mee als bijlage. Twee bewijsstukken (URL + bijlage) is robuust.
