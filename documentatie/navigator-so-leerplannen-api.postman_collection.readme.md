# Postman collection – GO! Navigator Secundair Leerplannen API

`navigator-so-leerplannen-api.postman_collection.json` is een Postman-collectie om de API te verkennen die GO! Navigator voor het **secundair onderwijs** gebruikt om leerplannen, hun structuur en labels op te halen.

> **Herkomst van deze documentatie:** voor deze API werd **geen documentatie voorzien door Smartschool**. De collectie werd zelf samengesteld op basis van de netwerkverzoeken die de webapplicatie GO! Navigator ([g-o.smartschool.be/navigator/leerplannen](https://g-o.smartschool.be/navigator/leerplannen)) uitvoert, vastgelegd in een HAR-export. Ze bevat enkel routes die in die sessie effectief voorkwamen.
>
> Omdat de API niet publiek gedocumenteerd is, kunnen routes en responsemodellen zonder aankondiging wijzigen. Dit in tegenstelling tot de [Curricula API voor het basisonderwijs](navigator-bao-curricula-api.openapi.yaml), waarvoor wel officiële documentatie beschikbaar is.

## Importeren

1. Open Postman.
2. **Import** → kies `navigator-so-leerplannen-api.postman_collection.json`.
3. De collectie "GO! Navigator Secundair - Leerplannen API" verschijnt met de mappen **Leerplannen** en **Labels**.

## Collection variables

| Variabele | Voorbeeldwaarde | Omschrijving |
|---|---|---|
| `baseUrl` | `https://g-o.smartschool.be` | Basis-URL van het GO!-platform |
| `leerplanId` | `76f187bd-4a96-4c0c-b102-3fbeb5dc7aeb` | Id van een leerplan, op te halen via **Lijst leerplannen** |
| `schooljaar` | `2026-2027` | Schooljaar waarvoor de structuur opgevraagd wordt |

## Requests

Alle routes starten met `{{baseUrl}}/navigator/api/v1`.

### Leerplannen

- **Lijst leerplannen** — `GET /leerplannen/list`
  Lijst van alle beschikbare leerplannen (in de vastgelegde sessie: 580 items). Elk item bevat o.a. `id`, `title`, `number`, `extraInformation`, `isVisible`, `metadata` en `capabilities`. Gebruik `id` als `leerplanId`.

- **Leerplan details** — `GET /leerplannen/{{leerplanId}}`
  Metadata van één leerplan: o.a. `id`, `group`, `number`, `title`, `image`, `isVisible`, `granteeGroupId`, `capabilities`, `infoBlocks` en `metadata`.

- **Leerplanstructuur** — `GET /leerplannen/{{leerplanId}}/structure/{{schooljaar}}`
  Hiërarchische structuur van één leerplan voor het gekozen schooljaar: o.a. `id`, `title`, `type`, `part`, `metadata`, `children` en `config`.

- **Combined view** — `GET /leerplannen/{{leerplanId}}/{{schooljaar}}/combined-view`
  De gecombineerde weergave die Navigator naast de eigen leerplanstructuur toont, bv. de gekoppelde basisvorming (*Basisvorming • arbeidsmarktfinaliteit • 3e graad* voor het voorbeeldleerplan). Geeft een array terug.

### Labels

- **Beschikbare globale labels** — `GET /global-labels/available`
  Globale labels die in Navigator beschikbaar zijn (in de vastgelegde sessie: 562 labels) met o.a. `id`, `platformId`, `identifier`, `text`, `color` en `isVisible`.

Elke request bevat eenvoudige Postman-tests (status 200, JSON-response en een controle op de verwachte vorm van de response).

## Opmerking

Bij deze API-calls werden geen `Authorization`-, `Cookie`- of CSRF-headers meegestuurd: de routes lijken publiek toegankelijk, net zoals de [openbare versie van GO! Navigator](README.md#openbare-versie-van-go-navigator).
