---
# You can also start simply with 'default'
theme: seriph
title: Klient- og servertilstand
info: |
  ## Slidev Starter Template
  Presentation slides for developers.
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true
---

# Alt du trenger å vite om klient- og servertilstand

I en klient-rendret React-applikasjon

<!--

I dag får dere vite alt dere trenger å vite om klient- og servertilstand. 

Men før vi går i gang, kan alle reise seg? La oss ta en liten avstemning. Hvis du syns det er lett å jobbe med tilstand, sitt ned. Jeg blir stående.

... **Avstemning**. 

Tilstandshåndtering i frontend er noe av det **vanskeligste vi gjør**. Du skal håndtere tilstander for alt fra skjemafelter og darkmode til innlogging og andre API-data. 

Jeg tror mye av kaoset rundt tilstandshåndtering har vært på grunn av en **misforståelse** rundt tilstandstyper. Vi har behandlet helt ulike tilstander som om de var de samme. Og det har skapt unødvendig mye kode, dårligere brukeropplevelser og dårligere ytelse.

Som dere ser fra taglinen, så blir fokuset i dag på tilstander i en **klient-rendret applikasjon**. Altså hvor du først rendrer applikasjonen, så begynner datahentingen å skje. Konseptene vil også være relevante for server-rendret applikasjon, men det er et litt annet beist. 

-->

---
src: ./pages/basic-useeffect.md
---

---
src: ./pages/differences-state.md
---

---
src: ./pages/useeffect-to-tanstack.md
---

---
src: ./pages/about-sync.md
---

---
src: ./pages/sync-mutation.md
---

---
src: ./pages/optimistic-mutation.md
---

---
src: ./pages/optimistic-code.md
---

---
src: ./pages/local-global-diff.md
---

---
src: ./pages/local-global-code.md
---

---
src: ./pages/state-tools.md
---

---
src: ./pages/redux.md
---


