---
layout: two-cols
layoutClass: gap-16
---

# Du MÅ ikke skille tilstandene

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

Altså, fikk dere også en sånn god følelse i kroppen nå?

Akkurat for servertilstand, er det veldig vanlig å bruke TanStack Query (eller useSWR, som gjør mye av det samme). 

TanStack Query gjør ikke datahenting. Dere ser vi har definert en fetcher. Men dataene som blir hentet, håndterer den i en tilstand.

Denne tilstanden er lagret på en cache-key. Dermed, om vi henter dataene fra et annet sted i appen, kan vi bruke den cachede dataen. 

Vi ser også at vi får egne tilstander for isLoading og error out of the box, uten at vi trenger å ha egen useState for dem. Det forenkler koden.

-->
