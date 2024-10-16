---
transition: fade
---

# Verktøy for tilstand

<v-click hide>

![](../images/dan_abramov_redux.png){width=500px lazy}

</v-click>

<v-after>

![](../images/josh_beat_saber_edit.gif){width=500px lazy}

</v-after>

<!--

Du skal sjeldent trenge Redux, med all dens kompleksitet. Selv Dan Abramov, som var en av skaperne av Redux, sier han sliter med å finne usecases for det.

[click] Så kommer Josh Comeau og lager dette sjuke redigeringsprogrammet for beat-saber, med nettopp Redux. 

Hans poeng er at Redux kan passe bra på klient-tunge applikasjoner, som photoshop eller redigering som dette, hvor det meste foregår på klient-tilstand. Selv om du også har noe sync med skyen.



-->

---
transition: fade
---

# Verktøy for tilstand

|     | Klient          | Server            |
| --- | --------------- | ----------------- |
| Lokal | useState<br/>useRef   | TanStack Query<br/>useSWR |
| Global | useContext<br/>useReducer<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai | TanStack Query<br/>useSWR |

<!--

Alt dette er for å si at du bør ta utgangspunkt i hvilken tilstand du har med å gjøre, så velge verktøy. Jeg håper jeg har gjort det klarere hvilken gruppe av verktøy du skal velge fra, så vil det spesifikke verktøyet avhenge av din kontekst og preferanse.

-->

---
transition: fade
---

<!--

Blank

-->
