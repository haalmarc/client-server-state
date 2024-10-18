---
transition: fade
---

# Verktøy for tilstand

- useState
- useRef
- useContext
- useReducer
- URL-parameter
- Redux
- Zustand
- MobX
- Jotai
- TanStackQuery
- useSWR

<!--
Det finnes en del verktøy for tilstand. 

De fem første her kommer med React ut fra boksen, mens resten er eksterne.

React har altså ingen innebygde verktøy for server-tilstand.

-->
---

# Verktøy for tilstand

|     | Klient          | Server            |
| --- | --------------- | ----------------- |
| Lokal | useState<br/>useRef |  |
| Global | useContext<br/>useReducer<br/>URL-parameter<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai | TanStack Query<br/>useSWR |

<!--
Verktøyene er beregnet for ulike tilstander, så du må velge fra riktig gruppe av verktøyer.

Du har useState og useRef som er for lokal klienttilstand, 

en drøss med verktøy for global klient-tilstand, også har du hvert fall to populære verktøy for å håndtere servertilstand.

Jeg tror overbruken av verktøy for global klient-tilstand henger igjen fra da folk brukte det til også servertilstand. 

-->