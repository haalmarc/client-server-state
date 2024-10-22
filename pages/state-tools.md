---
transition: fade
---

# Verktøy for tilstand

- useState
- useRef
- useReducer
- useContext
- URL-parameter
- Redux
- Zustand
- MobX
- Jotai
- TanStackQuery
- useSWR

<!--
Det finnes en del verktøy for tilstand. 

De fire første her kommer med React ut fra boksen, URL-parametere kommer med alle nettlesere og resten er eksterne.

Hvordan velger vi verktøy når det fins så mange?

-->
---

# Verktøy for tilstand

|     | Klient          | Server            |
| --- | --------------- | ----------------- |
| Lokal | useState<br/>useRef<br/>useReducer | TanStack Query<br/>useSWR |
| Global | useContext<br/>URL-parameter<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai | TanStack Query<br/>useSWR |

<!--


Verktøyene er beregnet for ulike tilstander. 

TODO: Gråe ut klient mens du snakker om server-tilstand

Det letteste skillet er mellom klient- og servertilstand. React kommer ikke med noen innebygde verktøy for asynkron tilstand, så da faller valget lett på TanStack Query eller useSWR.

TODO: Gråe ut server mens du snakker om klient-tilstand

Som dere ser fra tabellen, er det veldig mange alternativer for global tilstand. Jeg tror årsaken til det er fra da folk brukte disse verktøyene til også servertilstand, og hentet data én gang, for så å dele det ut i applikasjonen. Men som vi har sett, fins det bedre verktøy for det, som har en enklere synkronisering av klient og server.

TODO: Vise kodeeksempel med useState som går over til useReducer

Når vi skal velge verktøy for klient-tilstand, er det fortsatt mange valg. Men vi starter lokalt, så vi beholder kapsuleringen av komponentene. useState er enkelt å starte med. Om du har mer komplisert tilstand, kan du ta i bruk useReducer. Denne funksjonen har React-teamet hentet fra Redux, og lar deg skille tilstandsoppdatering mellom hva du ønsker å oppnå og hvordan du gjør det, som kan gi mer forståelig kode.

I første omgang kan vi holde oss på lokal klient-tilstand og prop-drille, men på et tidspunkt kan vi ønske å dele tilstand på tvers. React Context lar deg dele tilstand på tvers, ved å kombinere det med useState eller useReducer. Dermed får vi dekt både lokal og global klient-tilstand med innebygde verktøy.

Så er spørsmålet om du trenger noe annet.

TODO: Vise kodeeksempel med komponent med context som tar i bruk user.email,
men så endres user.phone, som komponenten ikke bryr seg om.
Så vise tilsvarende med Zustand.

React Context har noen begrensninger. Når en komponent konsumerer en kontekst, og den bryr seg om bare en del av objektet, vil komponenten re-rendre selv om en annen del av objektet endres. Noen av disse andre verktøyene prøver å løse det, som å ha en større "store" av tilstander, men så vil komponenten bare re-rendre avhengig av verdien du abonnerer på.

-->