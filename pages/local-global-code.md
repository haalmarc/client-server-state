---
transition: fade
---

# Lokal og global tilstand

````md magic-move {lines: true}

```ts {all|2,25-26|3,18,5-13}
export function ProfileForm() {
  const [email, setEmail] = useState("");
  const [userCount, setUserCount] = useState(null);

  useEffect(() => {
    const fetchUserCount = async () => {
      const response = await fetch("https://api.example.com/user-count");
      const data = await response.json();
      setUserCount(data.count);
    };

    fetchUserCount();
  }, []);

  return (
    <div>
      <h1>Opprett ny bruker</h1>
      <p>Antall brukere: {userCount}</p>

      <form>
        <label>
          E-post:
          <input
            type="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
        </label>
        <button type="submit">Opprett bruker</button>
      </form>
    </div>
  );
}
```

```ts {1,3,6|12,14,15,18}
export function ProfileForm() {
  ...
  const { isDarkMode, setIsDarkMode } = useContext(DarkModeContext);
  ...
  return (
    <div className={isDarkMode ? "dark-mode" : ""}>
      ...
    </div>
  );
}

export const DarkModeContext = createContext<DarkModeContextType | undefined>(undefined);

export const DarkModeProvider: React.FC = ({ children }) => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  return (
    <DarkModeContext.Provider value={{ isDarkMode, setIsDarkMode }}>
      {children}
    </DarkModeContext.Provider>
  );
};
```

```ts {3,14-15,19-21}
export function ProfileForm() {
  ...
  const { userCount } = useContext(UserCountContext);
  ...
  return (
    <div>
      ...
    </div>
  );
}

const UserCountContext = createContext<UserCountContextType | undefined>(undefined);

export const UserCountProvider: React.FC = ({ children }) => {
  const [userCount, setUserCount] = useState<number | null>(null);

  const fetchUserCount = async () => {
    try {
      const response = await fetch("https://api.example.com/user-count");
      const data = await response.json();
      setUserCount(data.count);
    } catch (error) {
      console.error("Error fetching user count:", error);
    }
  };

  useEffect(() => {
    fetchUserCount();
  }, []);

  return (
    <UserCountContext.Provider value={{ userCount }}>
      {children}
    </UserCountContext.Provider>
  );
};
```

```ts {*|0}
useEffect(() => {
  const controller = new AbortController();
  const fetchUserCount = async (retries = 3, delay = 1000) => {
    setLoading(true);
    try {
      const response = await fetch("https://api.example.com/user-count", {
        signal: controller.signal,
      });
      const data = await response.json();
      setUserCount(data.count);
    } catch (e) {
      if (retries > 0) {
        setTimeout(() => {
          fetchUserCount(retries - 1, delay * 2);
        }, delay);
      } else {
        setError("En feil skjedde");
      }
    } finally {
      setLoading(false);
    }
  };

  return () => {
    controller.abort();
  };

  fetchUserCount();
}, []);
```

```ts {4-7}
export function ProfileForm() {
  const [email, setEmail] = useState("");

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
  });

  return (

  );
}
```

```ts {4-7,15-18}
export function ProfileForm() {
  const [email, setEmail] = useState("");

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
  });

  return (

  );
}

export function Dashboard() {
  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
  });

  return (

  );
}


```

````

<!-- 
Tilbake til det første kode-eksempelet vi så, hvilken del av denne koden er lokal eller global?

[click] Igjen ser vi denne klient-tilstanden for skjemafeltet epost. Denne tilstanden bor kun i denne komponenten, så den er lokal.

[click] Så har vi tilstanden for antall brukere. Den hentes her inne med en fetch i en useEffect. Denne tilstanden er også lokal. Den eksponeres ikke ut.

[click] Et typisk eksempel på global klient-tilstand er darkmode. Her bruker vi React context til å hente ut dark-mode verdier. 

[click] En React context er altså et sted vi definerer en tilstand, som vi kan konsumere flere steder i applikasjonen.

[click] Når det gjelder hentingen av antall brukere, så kunne vi gjort gjort den global ved å putte den i en contextprovider.

Men da kommer vi tilbake igjen med problemet vi først snakket om.

[click] det er mange hensyn å ta ved denne måten å hente asynkron data.

[click] Så hva gjør vi?

[click] Det er ikke for ingen grunn jeg har prekt så mye om TanStack Query. Den dataen vi henter med TanStack query er også global.

[click] Det betyr at andre deler av applikasjonen får tilgang til den cachede dataen i TanStack Query, og må ikke nødvendigvis gjøre en ny request. Og det med bare så få kodelinjer.

-->