# GO! Navigator BaO Selector

De GO! Navigator BaO Selector laat een gebruiker vanuit een externe webapplicatie leerplandoelen van het basisonderwijs selecteren. Deze pagina beschrijft hoe de selector werkt en hoe de [demo](selector-demo/) hem gebruikt.

De volledige, officiële specificatie van het protocol staat in [`navigator-bao-selector-postmessage-protocol.pdf`](navigator-bao-selector-postmessage-protocol.pdf). Onderstaand overzicht is een beknopte samenvatting.

## Selector openen

De selector kan geopend worden als popup, als tab of in een `iframe`:

```text
https://g-o.smartschool.be/navigator-bao/selector/basisonderwijs
```

Optioneel met query parameters om een specifiek curriculum en/of curriculumitem te tonen: `?curriculumId=<uuid>&curriculumItemId=<uuid>`.

## Communicatie via `postMessage`

De communicatie tussen de toepassing en Navigator gebeurt via de browser-API `window.postMessage`.

### Basisflow

```text
Applicatie
   │
   │ opent Navigator (popup of iframe)
   ▼
Navigator Selector
   │
   │ ready
   ▼
Applicatie
   │
   │ setSelection (optioneel, enkel na ready)
   ▼
Navigator Selector
   │
   │ gebruiker selecteert doelen
   │
   │ save
   ▼
Applicatie
```

Navigator stuurt volgende **event messages**:

- `ready` – de selector is geïnitialiseerd en klaar om commands te ontvangen;
- `save` – de gebruiker heeft zijn selectie opgeslagen (`data: { selection }`);
- `close` – de selectortab wordt gesloten.

De toepassing kan enkel **na** het ontvangen van `ready` een **command message** naar Navigator sturen. Momenteel is er één command: `setSelection`, om een bestaande selectie in de selector te zetten.

Een selectie-item (`SimpleSelectionItem`) bestaat uit:

```typescript
type SimpleSelectionItem = {
    curriculumIdentifier: string;
    curriculumItemIdentifier: string;
};
```

De identifiers zijn dezelfde als die van de [Curriculum API](README.md#curriculum-api). Zo kan een opgeslagen selectie later opnieuw opgezocht worden in de curriculumstructuur.

---

## Demo

De map [`selector-demo/`](selector-demo/) bevat een eenvoudige toepassing waarin opdrachten aangemaakt worden en één of meerdere leerplandoelen via Navigator geselecteerd worden. De demo is ook online te bekijken via GitHub Pages (zie de [hoofd-README](../README.md#demo)).

```text
selector-demo/
├── index.html
├── css/
│   └── site.css
└── js/
    ├── app.js
    └── navigator.js
```

### `navigator.js`

Bevat de koppeling met GO! Navigator.

De `NavigatorSelector`:

- opent de selector;
- luistert naar `ready`, `save` en `close`;
- controleert of berichten afkomstig zijn van `https://g-o.smartschool.be`;
- kan een bestaande selectie opnieuw naar Navigator sturen.

### `app.js`

Bevat de logica van de demo.

Wanneer Navigator een selectie terugstuurt, worden onder andere volgende gegevens gebruikt:

```text
curriculumIdentifier
curriculumItemIdentifier
text
category
type
breadcrumbs
```

De demo bewaart alles enkel in het geheugen en heeft geen backend of database nodig.
