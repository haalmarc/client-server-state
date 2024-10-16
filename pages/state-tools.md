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
Det finnes en del verktøy for tilstand. Fire av fra lista her kommer med React ut fra boksen, mens resten er eksterne.

-->
---

# Verktøy for tilstand

|     | Klient          | Server            |
| --- | --------------- | ----------------- |
| Lokal | useState<br/>useRef   | TanStack Query<br/>useSWR |
| Global | useContext<br/>useReducer<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai | TanStack Query<br/>useSWR |

<!--
Verktøyene er beregnet for ulike tilstander. Du har useState og useRef som er for lokal klienttilstand, en drøss med verktøy for global klient-tilstand, også har du hvert fall to populære verktøy for å håndtere servertilstand. 

Jeg håper du nå har blitt litt klokere på hvilken gruppe du bør velge verktøy fra. Hvilket verktøy fra gruppa du skal velge, avhenger av din kontekst og preferanse.

-->