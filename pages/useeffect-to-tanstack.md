---
layout: two-cols
layoutClass: gap-16
---

# Du klarer deg med en hammer...

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
Skillet mellom klient- og server-tilstand fører ikke til at du MÅ bruke visse verktøy. Som vi så, kan du implementere alle funksjonalitetene henting av data krever selv. Men det er komplekst og kan bli rotete. Og her har vi ikke snakka om caching en gang.

Hva skjer om vi bytter ut vår custom kode med et verktøy som TanStack Query?

[click] Altså, fikk dere også en sånn god følelse i kroppen nå?

Akkurat for servertilstand, er det veldig vanlig å bruke TanStack Query, og dere skjønner kanskje hvorfor? Vi får mye funksjonalitet ut av boksen, som loading og error i egne tilstander.

Også okay da, jeg skal gjøre bildet litt ærligere, med litt mer kode. TanStack Query gjør ikke datahenting. 

[click] For det har vi definert en fetcher. Men dataene som blir hentet, håndterer TanStack Query i en egen tilstand, lagret på cache-nøkkelen. Dermed, om vi henter dataene fra et annet sted i appen, kan vi bruke den cachede dataen.

-->
