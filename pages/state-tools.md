---
transition: fade
---

# Verktøy for tilstand

- useState
- useRef
- useContext
- useReducer
- Redux
- Zustand
- MobX
- Jotai
- TanStackQuery
- useSWR

<!--
Det finnes en del verktøy for tilstand. 

De fire første her kommer med React ut fra boksen, mens resten er eksterne.

-->
---

# Verktøy for tilstand

|     | Klient          | Server            |
| --- | --------------- | ----------------- |
| Lokal | useState<br/>useRef   | TanStack Query<br/>useSWR |
| Global | useContext<br/>useReducer<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai | TanStack Query<br/>useSWR |

<!--
Verktøyene er beregnet for ulike tilstander. Du har useState og useRef som er for lokal klienttilstand, 

en drøss med verktøy for global klient-tilstand, også har du hvert fall to populære verktøy for å håndtere servertilstand.

Så hvordan velger du blant disse verktøyene? 

Om du driver med asynkron data, altså en forespørsel til noe eksternt, bruker du et verktøy for servertilstand. 

Om du driver med tilstand som klienten har kontroll over, start med en lokal useState. Om du trenger å ha global state, kommer du langt med Reacts context eller useReducer. 

Jeg tror overbruken av verktøy for global klient-tilstand henger igjen fra da folk brukte det til også servertilstand, men nå fins det enklere, bedre verktøy. 

-->