# Welcome to [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- `pnpm install`
- `pnpm run dev`
- visit <http://localhost:3030>

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev at the [documentation](https://sli.dev/).

# Presentasjon

Ved presentasjon, åpne localhost:3030 i to faner.
I den ene fanen skriver du presenter, e.g. http://localhost:3030/presenter. 

Da vil du kunne se notater i ett vindu, mens det andre synces idet du bytter faner.

Husk også å aktivere dark-mode i visningen.

## Mobil som fjernkontroll

- Sjekk IP på nettverk på Mac: 
  - WiFi -> Detaljer -> IP-adresse
- Kjør kommando for å tillate remote access (kan utelate passord):
  - pnpm dev --remote=passord
  - Her får du også URL-er du skal besøke på laptop eller mobil
- Besøk URL public slide show for laptop.
- Besøk remote control URL tilsvarende IP-en din på nettleser på telefon.

OBS. Noen begrensninger med mobil som fjernkontroll, så her er noen tips:

- For neste slide, sveip inni "Current"-vindu. Pil-knappene frem og tilbake er veldig små, så lett å trykke feil, som tar deg ut av kontroll.
- Sveip 4 sekunder før du egentlig vil bytte slide. Presentasjonen ser ut til å jevnt svare, men det kan ta litt tid.
- Av samme grunn, kun sveip én gang. Ellers hoper det seg hopp, og du hopper over mange slides.
- Om du ønsker å vise interaksjon med komponenter, må du endre på visningsvinduet. Du må derfor bruke laptop, og endringer i presentation-mode vises ikke i publikumsvisningen.

# Tips

- Start nytt sli.dev prosjekt og initier git. Siden du kan gjøre endringer i både IDE-en og i presentasjonen, er det lett å gjøre endringer du ikke ønsker og som kan tulle til formatering. Det kan du enkelt legge merke til og reverte med git.
- Også nyttig å ha default templates tilgjengelig mens du lager slide for første gang, for å se hvilke funksjonaliteter du kan bruke.
- Når du legger til ny fil du vil importere i slides.md, start terminalen på nytt. For ellers vil det kræsje.
- Legg til .prettierignore og ignorer `*.md`. Markdown i sli.dev krever viss formatering, som blir ødelagt av prettier.

