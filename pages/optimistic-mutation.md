---
layout: two-cols
layoutClass: gap-16
---

# Optimistisk oppdatering

<FormOptimistic />

::right::

<ol>
  <v-click><li>Vi endrer server-tilstanden med en gang</li></v-click>
  <v-click><li>Vi sender en forespørsel til serveren om å endre tilstand</li></v-click>
  <v-click>
    <li>Etter forespørselen er fullført: 
      <ul>
        <li>a) hvis suksess: oppdater server-tilstanden med de faktiske dataene</li>
        <li>b) hvis kallet feiler: rull tilbake</li>
      </ul>
    </li>
  </v-click>
</ol>

<!--

Så servertilstanden er asynkron. Vi må vente på at forespørselen vår går fra klienten, gjør noe på serveren, og så får vi tilbake et svar. Men for å gjøre brukeropplevelsen snappy, kan vi bruke optimistisk oppdatering.

Istedenfor å vente på at forespørselen fullføres, oppdaterer vi klientens servertilstand, før vi får bekreftelse på at forespørselen er vellykket. Optimistiske oppdateringer er ikke noe magisk, men et mønster, som består av 3 steg:

[click] Server-tilstanden endres umiddelbart, for å vise endring til brukeren. Husk også gammel tilstand, tilfelle feil skjer og tilstand rulles tilbake

[click] Et kall gjøres til serveren for å lagre tilstand til server

[click] Etter API-kallet fullføres: a) Hvis kallet var vellykket, oppdater klientens server-tilstand med den nye server-tilstanden. b) Hvis kallet feiler, rull tilbake til gammel tilstand

(demonstrer suksess og feil: skriv inn og trykk opprett bruker. 0.4 sjanse for feil)

-->
