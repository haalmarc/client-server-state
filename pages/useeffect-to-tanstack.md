---
layout: two-cols
layoutClass: gap-16
---

# Verktøy for servertilstand

<Formexample />

::right::

````md magic-move {lines: true}

```ts {all}
export function ProfileForm() {
  const [email, setEmail] = useState("");
  const [userCount, setUserCount] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

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

  return (

  );
}
```

```ts {all}
import { useQuery } from "@tanstack/react-query";

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

```ts {1-7,12-15}
async function fetchUserCount() {
  const response = await fetch('https://api.example.com/user-count');
  if (!response.ok) {
    throw new Error('Failed to fetch user count');
  }
  return response.json();
}

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

````

<!--
Skillet mellom klient- og server-tilstand tvinger deg ikke til å bruke visse verktøy, men som vi har sett kan det bli ganske komplisert og rotete. Og det er uten å ha nevnt caching.

Hva skjer om vi bytter ut vår egen kode med TanStack Query, som er **beregnet** for server-tilstand?

[click] Altså, fikk dere også en sånn god følelse i kroppen nå?

TanStack Query er det mest populære verktøyet for servertilstand, og dere skjønner kanskje hvorfor? Vi får mye funksjonalitet ut av boksen, som data, loading og error i egne tilstander. 

Det er et verktøy vi bruker i klienten, og som håndterer dataflyten mellom klient og server.

Også okay da, jeg skal gjøre bildet litt ærligere, med litt mer kode. TanStack Query gjør ikke selve datahentingen. 

[click] For det har vi definert en fetcher, som vi mater inn i useQuery. 

Og dataene som blir hentet fra serveren, putter TanStack Query i en egen cache på klienten, lagret på en cache-nøkkel. Dermed, om vi henter dataene fra et annet sted i appen, slipper vi å hente dataene på nytt, og kan bruke den cachede dataen.

-->
