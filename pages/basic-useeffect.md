---
layout: two-cols
layoutClass: gap-16
---

# useState og useEffect

<Formexample />

::right::

<v-click>

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

```ts {4,8,16,9,13}
export function ProfileForm() {
  const [email, setEmail] = useState("");
  const [userCount, setUserCount] = useState(null);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    const fetchUserCount = async () => {
      setLoading(true);
      try {
        const response = await fetch("https://api.example.com/user-count");
        const data = await response.json();
        setUserCount(data.count);
      } catch (e) {
        console.error(e);
      } finally {
        setLoading(false);
      }
    };

    fetchUserCount();
  }, []);

  return (

  );
}
```

```ts {5,15}
export function ProfileForm() {
  const [email, setEmail] = useState("");
  const [userCount, setUserCount] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUserCount = async () => {
      setLoading(true);
      try {
        const response = await fetch("https://api.example.com/user-count");
        const data = await response.json();
        setUserCount(data.count);
      } catch (e) {
        setError("En feil skjedde");
      } finally {
        setLoading(false);
      }
    };

    fetchUserCount();
  }, []);

  return (

  );
}
```

```ts {8,12-14,24-26}
export function ProfileForm() {
  const [email, setEmail] = useState("");
  const [userCount, setUserCount] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();
    const fetchUserCount = async () => {
      setLoading(true);
      try {
        const response = await fetch("https://api.example.com/user-count", {
          signal: controller.signal,
        });
        const data = await response.json();
        setUserCount(data.count);
      } catch (e) {
        setError("En feil skjedde");
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


```ts {9,17-24|all}
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

````

</v-click>

<!--
Her ser vi et enkelt skjema der du kan opprette en bruker og følge med på antall brukere som er lagd.

Det er også enkel kode her. Vi har en useState for å holde rede på tilstanden når brukeren skriver. Så når brukeren skriver, oppdateres skjemafeltet seg med en gang.

Vi har også en annen tilstand, for å vise antall brukere. Denne starter som null, men etter henting av data i en useEffect, blir den satt til en verdi. Også denne er med useState.

Jeg vet ikke med dere, men syns dere det mangler noe her?
Vi gjør jo en fetch. Så det kan jo ta litt tid før vi får dataene, så la oss putte på en loading-status.

Også er det jo sånn at siden vi gjør en fetch, så kan jo kallet feile av en eller annen grunn. Så la oss putte på en status for feil.

Også ønsker vi ikke å belaste servern hvis komponente unmounter, så vi legger til en abortcontroller.

Også kan det jo hende at fetchen feiler av en obskur grunn, så vi vil retry-e først vi gir opp.

Det er med andre ord ganske stor forskjell på tilstanden for å skjemafeltet og tilstanden for å holde rede på antall brukere. De er helt forskjellige typer tilstander. Den ene er klient-tilstand, som er eid av brukeren. Mens den andre er server-tilstand, som er eid av serveren. Å forstå forskjellene hjelper oss å forstå kompleksiteten på de ulike tilstandene, og hvilke muligheter de gir. La oss se nærmere på forskjellene. 
-->
