# TNL Proces-tool

Losse mini-app: beschrijf een proces in gewone taal → **Claude** zet het om naar een
BPMN-diagram → je past het visueel aan in een volwaardige editor (bpmn-js, dezelfde
motor als de Camunda web-modeler).

Staat **los** van de andere tools en van Supabase. Niets hiervan raakt de Offerte-app
of de database.

## Starten (lokaal)

Dubbelklik `start-server.bat` (start een lokale server op http://localhost:3005), of
open `index.html` rechtstreeks in de browser.

## Anthropic-sleutel

Klap in de zijbalk **"API-sleutel"** open en plak je `sk-ant-…`. De sleutel wordt
**enkel in je browser** bewaard (localStorage) en gaat rechtstreeks naar Anthropic via
de `anthropic-dangerous-direct-browser-access`-header. Hij komt **nooit** in een
bestand of in git.

> Dit is bedoeld voor lokaal/persoonlijk gebruik. Wil je de tool ooit publiek hosten
> (GitHub Pages), dan zetten we er een kleine proxy (bv. Cloudflare Worker) voor, zodat
> de sleutel serverside blijft. Dat is een latere stap, geen herbouw.

## Hoe het werkt

1. Je tekst → Claude (`claude-opus-4-8`, structured output) → JSON-procesmodel
   (stappen, beslissingen/gateways, pijlen).
2. JS bouwt daar semantische BPMN 2.0 XML van.
3. `bpmn-auto-layout` berekent de plaatsing (coördinaten).
4. bpmn-js laadt het → jij sleept/wijzigt vrij.
5. Opslaan = **Download .bpmn** (standaard BPMN 2.0 XML).

## Bewust later

- **Supabase-bibliotheek**: processen bewaren, zoeken, koppelen aan NextStones/Tools.
- **Proxy** voor publiek hosten (key serverside).
- **Lanes/zwembanen** (rollen TNL/Klant/Derde) bij het genereren.
- **Camunda-uitvoering**: de opgeslagen BPMN-XML is het standaardformaat dat een
  Camunda-engine inleest — je rijdt je dus niet vast.

## Verwijderen

Map weggooien. Klaar. (Geen repo, geen database, geen cloud-restjes zolang je niet
deployt.)
