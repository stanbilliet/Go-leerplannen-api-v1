# Leerplannen secundair onderwijs

Voor het secundair onderwijs zijn de GO!-leerplannen op twee manieren beschikbaar:

1. een statische **JSON-export** van alle leerplannen;
2. de **Leerplannen API** die GO! Navigator zelf gebruikt.

## Inhoud

| Bestand | Omschrijving |
|---|---|
| [`GO-leerplannen-secundair_2025-09.json`](GO-leerplannen-secundair_2025-09.json) | JSON-export van de GO!-leerplannen secundair onderwijs (momentopname september 2025). |
| [`navigator-so-leerplannen-api.postman_collection.json`](navigator-so-leerplannen-api.postman_collection.json) | Postman-collectie voor de Leerplannen API van GO! Navigator. Niet gedocumenteerd door Smartschool, zelf samengesteld op basis van het netwerkverkeer van Navigator. Zie de bijhorende [readme](navigator-so-leerplannen-api.postman_collection.readme.md). |

---

## JSON-export

Er is een statische JSON-export beschikbaar van de leerplannen secundair onderwijs:

**https://gofier.be/JSON_GO_leerplannen_2025-09.json**

Deze staat, als momentopname van september 2025, ook in deze map: [`GO-leerplannen-secundair_2025-09.json`](GO-leerplannen-secundair_2025-09.json).

> **Let op:** gebruik voor de actuele, up-to-date versie van de leerplannen steeds **https://pro.g-o.be/themas/leerplannen/go-navigator/** — de lokale JSON-kopie is enkel een momentopname en kan verouderd zijn.

---

## Leerplannen API

De leerplannen kunnen ook rechtstreeks opgehaald worden via de API die GO! Navigator zelf gebruikt:

```text
https://g-o.smartschool.be/navigator/api/v1
```

> **Let op:** voor deze API werd **geen documentatie voorzien door Smartschool**. De Postman-collectie [`navigator-so-leerplannen-api.postman_collection.json`](navigator-so-leerplannen-api.postman_collection.json) werd zelf samengesteld op basis van de netwerkverzoeken van de Navigator-webapplicatie. Routes en responsemodellen kunnen zonder aankondiging wijzigen.

Belangrijkste routes:

- `GET /leerplannen/list` – lijst van alle leerplannen;
- `GET /leerplannen/{leerplanId}` – metadata van één leerplan;
- `GET /leerplannen/{leerplanId}/structure/{schooljaar}` – volledige structuur van een leerplan (bv. schooljaar `2026-2027`);
- `GET /leerplannen/{leerplanId}/{schooljaar}/combined-view` – gekoppelde weergave (bv. basisvorming);
- `GET /global-labels/available` – beschikbare globale labels.

Zie de [readme bij de collectie](navigator-so-leerplannen-api.postman_collection.readme.md) voor de details.

---

## Openbare versie van GO! Navigator

Naast de API bestaat er een publiek toegankelijke, read-only versie van GO! Navigator:

**https://g-o.smartschool.be/navigator/leerplannen**

> Welkom bij de openbare versie van GO! Navigator. Voor degenen die geen toegang hebben tot Smartschool, biedt deze publieke versie van GO! Navigator de mogelijkheid om door de leerplannen te bladeren.
>
> De Helpdesk, Materialenbank en didactische fiches zijn niet opgenomen in deze publieke versie.
