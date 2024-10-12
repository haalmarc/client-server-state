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

````

</v-click>
