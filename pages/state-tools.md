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
transition: fade
---

# Verktøy for tilstand

<table>
  <thead>
    <tr>
      <th></th>
      <th>Klient</th>
      <th>Server</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lokal</td>
      <td>useState<br/>useRef<br/>useReducer</td>
      <td>TanStack Query<br/>useSWR</td>
    </tr>
    <tr>
      <td>Global</td>
      <td>useContext<br/>URL-parameter<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai</td>
      <td>TanStack Query<br/>useSWR</td>
    </tr>
  </tbody>
</table>

<!--

Verktøyene er beregnet for ulike tilstander. Som dere ser fra tabellen, er det veldig mange alternativer for global tilstand. 

Jeg tror årsaken til det er fra da folk brukte disse verktøyene til også servertilstand, og hentet data én gang, for så å dele det ut i applikasjonen. Men som vi har sett, fins det bedre verktøy for det, som har en enklere synkronisering av klient og server.

-->

---
transition: fade
---

# Verktøy for tilstand

<table class="second-column-blurred">
  <thead>
    <tr>
      <th></th>
      <th>Klient</th>
      <th>Server</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lokal</td>
      <td>useState<br/>useRef<br/>useReducer</td>
      <td>TanStack Query<br/>useSWR</td>
    </tr>
    <tr>
      <td>Global</td>
      <td>useContext<br/>URL-parameter<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai</td>
      <td>TanStack Query<br/>useSWR</td>
    </tr>
  </tbody>
</table>

<!--

Det letteste skillet er mellom klient- og servertilstand. React kommer ikke med noen innebygde verktøy for asynkron tilstand, så da faller valget på TanStack Query eller useSWR.

-->

---
transition: fade
---

# Verktøy for tilstand

<table class="third-column-blurred">
  <thead>
    <tr>
      <th></th>
      <th>Klient</th>
      <th>Server</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lokal</td>
      <td>useState<br/>useRef<br/>useReducer</td>
      <td>TanStack Query<br/>useSWR</td>
    </tr>
    <tr>
      <td>Global</td>
      <td>useContext<br/>URL-parameter<br/>Redux<br/>Zustand<br/>MobX<br/>Jotai</td>
      <td>TanStack Query<br/>useSWR</td>
    </tr>
  </tbody>
</table>

<!--

Når vi skal velge verktøy for klient-tilstand, er det fortsatt mange valg.

-->

---
transition: fade
---

# Verktøy for klienttilstand

````md magic-move {lines: true}

```ts {1,2}
export function Todos() {
  const [tasks, setTasks] = useState(initialTasks);

  function handleAddTask(text) {
    setTasks([
      ...tasks,
      {
        id: nextId++,
        text: text,
        done: false,
      },
    ]);
  }

  return (
    ...
  );
}

```

```ts {2,5-6,17-19}
export function Todos() {
  const [tasks, dispatch] = useReducer(tasksReducer, initialTasks);

  function handleAddTask(text) {
    dispatch({
      type: 'added',
      id: nextId++,
      text: text,
    });
  }

  return (
    ...
  );
}

function tasksReducer(tasks, action) {
  switch (action.type) {
    case "added": {
      return [
        ...tasks,
        {
          id: action.id,
          text: action.text,
          done: false,
        },
      ];
    }
    case "changed": {
      return tasks.map((t) => {
        if (t.id === action.task.id) {
          return action.task;
        } else {
          return t;
        }
      });
    }
    case "deleted": {
      return tasks.filter((t) => t.id !== action.id);
    }
    default: {
      throw Error("Unknown action: " + action.type);
    }
  }
}

```

```ts {2,5}
export function Todos() {
  const [tasks, dispatch] = useReducer(tasksReducer, initialTasks);

  return (
    <OtherComponent tasks={tasks} />>
  );
}

```

```ts {2,7}
export function Todos() {
  const { tasks } = useContext(TasksContext);
  ...
}

export function OtherSetterComponent() {
  const { setTasks } = useContext(TasksContext);
  ...
}
```

```ts {1,3-6|9,14}
import { create } from 'zustand'

const useTasksStore = create((set) => ({
  tasks: initialTasks,
  addTask: (newTask) => set((state) => ({ tasks: [...state.tasks, newTask] })),
}))

export function Todos() {
  const tasks = useTasksStore((state) => state.tasks)
  ...
}

export function OtherSetterComponent() {
  const addTask = useTasksStore((state) => state.addTask)
  ...
}

```


````

<!-- 

La oss se på et eksempel med oppdatering av todos.

Det er alltid bra å starte lokalt. Da beholder vi kapsuleringen av komponentene, og kan unngå spaghetti-kode. useState er enkelt å starte med. 

[click] Om du har komplisert tilstand, så kan det være nyttig å ta i bruk useReducer. 

Denne funksjonen har React-teamet hentet fra Redux, og lar deg skille tilstandsoppdatering mellom hva brukeren gjør, altså en action, og hvordan du oppdaterer tilstanden, altså reduceren. Dette kan gi mer forståelig kode.

[click] I første omgang kan vi holde oss på lokal klient-tilstand og prop-drille, men når vi prop-driller mer enn 3 lag, gjør det vondt. Da er det på tide å bruke et verktøy for global tilstand.

[click] Vi har allerede sett på React Context. Du kan kombinere det med useState eller useReducer, og dermed får vi dekt både lokal og global klient-tilstand med innebygde verktøy.

Så er spørsmålet om du trenger noe annet.

React Context har noen begrensninger. Når en komponent konsumerer en kontekst, vil den re-rendre når konteksten endrer seg. Så om vi har en komponent som bare setter tasks, vil den re-rendre også om tasks endrer seg, selv om den ikke bruker dataene.

Noen av verktøyene vi har sett på prøver å løse dette. Jeg skal ikke gå gjennom alle, men la oss se på et alternativ.

[click] Zustand er et av verktøyene som løser dette, med et enklere API enn Redux. Her definerer du en hook, hvor vi definerer initiell data og hvordan vi oppdaterer den.

[click] Så kan vi velge hva fra global tilstand vi vil følge med på, enten det er kun data eller kun setter. Da vil komponenten bare re-rendre når noe vi bryr oss om endrer seg.

-->