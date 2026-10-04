# GO! Leerplannen API

Deze repository bundelt technische documentatie en voorbeelden om programmatisch met de **GO!-leerplannen** te werken, zowel voor het basisonderwijs als voor het secundair onderwijs.

| | Basisonderwijs | Secundair onderwijs |
|---|---|---|
| **API** | Curriculum API (officieel gedocumenteerd) | Leerplannen API van GO! Navigator (geen documentatie van Smartschool) |
| **Statische export** | – | JSON-export (september 2025) |
| **Doelen laten selecteren** | Navigator BaO Selector + demo | – |
| **Map** | [`basisonderwijs/`](basisonderwijs/README.md) | [`secundair/`](secundair/README.md) |

---

## Basisonderwijs

Voor het basisonderwijs (GO! Navigator BaO) is er:

- de **Curriculum API**, met een officiële OpenAPI-specificatie en een Postman-collectie, om curricula en hun volledige structuur uit te lezen:

  ```text
  https://g-o.smartschool.be/curriculum/api/v1
  ```

- de **Navigator BaO Selector**, waarmee een gebruiker vanuit een eigen toepassing leerplandoelen kiest. De selectie komt via `window.postMessage` terug. Zie [`basisonderwijs/navigator-bao-selector.md`](basisonderwijs/navigator-bao-selector.md) voor de werking en de demo;
- de **kenniskaart leerplanconcept**, om de opbouw van en de samenhang tussen de doelen te begrijpen.

Meer info: [`basisonderwijs/README.md`](basisonderwijs/README.md).

## Secundair onderwijs

Voor het secundair onderwijs is er:

- een statische **JSON-export** van alle GO!-leerplannen (momentopname september 2025);
- de **Leerplannen API** die GO! Navigator zelf gebruikt:

  ```text
  https://g-o.smartschool.be/navigator/api/v1
  ```

> **Let op:** voor de Leerplannen API secundair onderwijs werd **geen documentatie voorzien door Smartschool**. De Postman-collectie in deze repository werd zelf samengesteld op basis van de netwerkverzoeken van de Navigator-webapplicatie.

Meer info: [`secundair/README.md`](secundair/README.md).

---

## Demo

De demo van de Navigator BaO Selector staat in [`basisonderwijs/selector-demo/`](basisonderwijs/selector-demo/) en wordt via GitHub Pages gepubliceerd. De root van de site ([`index.html`](index.html)) is een overzichtspagina die naar de demo en de documentatie verwijst.

De demo is een statische webpagina zonder backend: alles wordt enkel in het geheugen bewaard.

---

## Structuur

```text
.
├── index.html                      Overzichtspagina (GitHub Pages)
├── basisonderwijs/
│   ├── README.md
│   ├── navigator-bao-curricula-api.openapi.yaml
│   ├── navigator-bao-curricula-api.postman_collection.json
│   ├── navigator-bao-curricula-api.postman_collection.readme.md
│   ├── navigator-bao-selector.md
│   ├── navigator-bao-selector-postmessage-protocol.pdf
│   ├── kenniskaart-leerplanconcept.pdf
│   └── selector-demo/              Demo-integratie van de selector
└── secundair/
    ├── README.md
    ├── GO-leerplannen-secundair_2025-09.json
    ├── navigator-so-leerplannen-api.postman_collection.json
    └── navigator-so-leerplannen-api.postman_collection.readme.md
```

---

## Disclaimer

Dit project is bedoeld als technisch integratievoorbeeld.

- De Curriculum API en het Selector-protocol voor het basisonderwijs zijn officieel gedocumenteerd en kunnen in de toekomst wijzigen.
- De Leerplannen API voor het secundair onderwijs werd niet door Smartschool gedocumenteerd. De beschrijving in deze repository is afgeleid uit het gebruik door de Navigator-webapplicatie zelf, en routes en responsemodellen kunnen zonder aankondiging wijzigen.

Gebruik voor de actuele inhoud van de leerplannen steeds **https://pro.g-o.be/themas/leerplannen/go-navigator/**.
