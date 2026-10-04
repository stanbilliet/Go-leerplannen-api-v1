# Leerplannen basisonderwijs

Voor het basisonderwijs biedt GO! Navigator BaO twee officieel gedocumenteerde manieren om met de leerplannen te werken:

1. de **Curriculum API** om curricula en hun structuur programmatisch uit te lezen;
2. de **Navigator BaO Selector** om een gebruiker zelf leerplandoelen te laten kiezen vanuit een eigen toepassing.

## Inhoud

| Bestand | Omschrijving |
|---|---|
| [`navigator-bao-curricula-api.openapi.yaml`](navigator-bao-curricula-api.openapi.yaml) | OpenAPI 3.0-specificatie van de officiële Navigator BaO Curricula API (endpoints, schema's, foutafhandeling). |
| [`navigator-bao-curricula-api.postman_collection.json`](navigator-bao-curricula-api.postman_collection.json) | Postman-collectie om de API manueel te testen. Zie de bijhorende [readme](navigator-bao-curricula-api.postman_collection.readme.md). |
| [`navigator-bao-selector.md`](navigator-bao-selector.md) | Uitleg over de Navigator BaO Selector en de demo-integratie. |
| [`navigator-bao-selector-postmessage-protocol.pdf`](navigator-bao-selector-postmessage-protocol.pdf) | Officiële documentatie van het `postMessage`-protocol van de selector (command/event messages, integratiegids, volledige message schema's). |
| [`selector-demo/`](selector-demo/) | Demo-toepassing die de selector integreert. |
| [`kenniskaart-leerplanconcept.pdf`](kenniskaart-leerplanconcept.pdf) | Kenniskaart leerplanconcept (structuur, visie, opbouw doelenset, MIA, samenhang). |

---

## Curriculum API

Navigator BaO gebruikt een API om de beschikbare curricula en hun structuur op te halen.

> De volledige, officiële specificatie van deze API staat in [`navigator-bao-curricula-api.openapi.yaml`](navigator-bao-curricula-api.openapi.yaml). Onderstaand overzicht is een beknopte samenvatting.

Base URL:

```text
https://g-o.smartschool.be/curriculum/api/v1
```

Voor GO! Navigator BaO lijken volgende waarden vast te zijn:

```text
platformId = 1071
source = navigator-bao
```

### Curricula ophalen

```http
GET /curricula/1071/{date}/navigator-bao
```

Voorbeeld:

```text
https://g-o.smartschool.be/curriculum/api/v1/curricula/1071/2026-08-12/navigator-bao
```

Dit endpoint geeft de beschikbare curricula terug. Elk curriculum bevat onder andere een unieke `identifier`.

### Structuur van een curriculum ophalen

De `identifier` uit het vorige endpoint kan gebruikt worden om de volledige curriculumstructuur op te halen:

```http
GET /structure/1071/{curriculumIdentifier}/navigator-bao/{date}
```

Voorbeeld voor Nederlands:

```text
https://g-o.smartschool.be/curriculum/api/v1/structure/1071/1071_4d72860b-b6d0-4157-8198-5e397a04d189_navigator-bao/navigator-bao/2026-08-12
```

De response bevat onder andere:

```text
curriculum
tree
configuration
```

`tree` bevat de hiërarchische structuur van het curriculum met onder andere leerplandoelen, tussentitels, labels en relaties tussen curriculumitems.

---

## Navigator BaO Selector

Met de selector kiest een gebruiker zelf leerplandoelen in GO! Navigator, waarna de selectie via `window.postMessage` teruggestuurd wordt naar de eigen toepassing:

```text
https://g-o.smartschool.be/navigator-bao/selector/basisonderwijs
```

Zie [`navigator-bao-selector.md`](navigator-bao-selector.md) voor de werking van het protocol en de uitleg bij de [demo](selector-demo/).

---

## Kenniskaart leerplanconcept

[`kenniskaart-leerplanconcept.pdf`](kenniskaart-leerplanconcept.pdf) geeft een visueel overzicht van het leerplanconcept: de structuur (twaalf doelensets in samenhang), de opbouw van een doelenset (MIA, te hanteren begrippen, doelen die Begrijpen/Gebruiken/Engageren), en de horizontale/verticale samenhang tussen doelen.

Deze kaart is nodig om de opbouw en de relatie tussen de doelen echt te doorgronden, samen met de visie zoals uitgeschreven op:

**https://pro.g-o.be/themas/leerplannen/basisonderwijs/nieuw-leerplan-basisonderwijs/**
