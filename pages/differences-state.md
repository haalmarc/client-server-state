# Klient- vs server-tilstand

| Klient | Server |
| --- | --- |
| Klient-eid |  |
| Bare deg som endrer |  |
| Flyktig |  |
| Synkron |  |

<!-- 
La oss se nærmere på forskjellene.

- Klient-eid: Det er deg som bruker som eier klient-tilstanden. Klient-tilstanden er lagret lokalt på din enhet, enten det er nettleser eller app.
- Bare du endrer den: Klient-tilstanden er din, og det er ingen andre som kan endre den.
- Flyktig: Samtidig er klient-tilstanden også flyktig, siden den bare bor hos deg, så den kan slettes idet du lukker nettleseren.
- Synkron: Det at vi eier klient-tilstanden, gjør den også synkron. Den er umiddelbar tilgjengelig, og endres raskt.

Alle disse 4 faktorene gjør klient-tilstanden lett å jobbe med. Det er kun du som kan endre noe, så få ting kan gå galt.

-->
---

# Klient- vs server-tilstand

| Klient | Server |
| --- | --- |
|  | Server-eid |
|  | Flere som endrer |
|  | Lagret over tid |
|  | Asynkron |

<!--
På den andre siden har vi server-tilstand (altså egentlig asynkron tilstand, men oftest er det data som bor på en server et eller annet sted). 

- Server-eid: Server-tilstand er server-eid. Den tilstanden bor bortpå en server, vekk fra oss, så det vi har tilgjengelig hos oss, er ikke nødvendigvis i sync med det som bor på serveren.
- Endret av flere brukere: Også er det ikke bare vi som endrer dataene. Også andre personer har lagret dataene på serverne og kan endre den.
- Lagret over tid: Siden data lagres på annet sted enn nettleseren, så kan vi også beholde tilstanden over tid, selv om nettleseren lukkes.
- Asynkron: Siden server-tilstanden er lagret vekk fra oss, tar det tid for data å reise fra serveren til klienten. Altså tar det tid fra vi forespør data til vi får den, og det kan være endringer fra vi spør til vi får den.
-->

---

# Klient- vs server-tilstand

| Klient | Server |
| --- | --- |
| Klient-eid | Server-eid |
| Bare deg som endrer | Flere som endrer |
| Flyktig | Lagret over tid |
| Synkron | Asynkron |

<!--
Det er altså noen forskjeller på disse tilstandene.
-->