# Synkronisere mellom klient og server

````md magic-move {lines: true}

```ts {3-6}
export function ProfileForm() {

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
  });

  return (

  );
}
```

```ts {3-7}
export function ProfileForm() {

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
    staleTime: 1000 * 30,
  });

  return (

  );
}
```

```ts {6}
export function ProfileForm() {

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
    staleTime: Infinity,
  });

  return (

  );
}
```

````

<!-- 
Dette med at servertilstanden blir endret av andre, gjør at om vi henter data en gang, kan det 2 sekunder senere være utdatert fordi andre har oppdatert dataene.

Dermed er en utfordring i servertilstand å holde dataene mellom klient og server oppdatert. TanStack Query lagrer dataene på en cache i klienten, og vil ikke i utgangspunktet hente nye data før dataene er regnet som gamle.

[click] Dette kan du styre med staleTime, som er satt til 5 minutter som standard. Om du ønsker oftere oppdateringer, kan du overstyre. 

[click] Også er det også tilfeller vi ikke bryr oss om at andre endrer dataene i bakgrunn. Med mindre vi har et dashboard hvor vi ønsker live-updates eller vi har en maks brukergrense, så er det ikke så farlig om antall brukere er oppdatert. Da kan vi sette staleTime til Infinity, som sier at dataene aldri kommer til å bli gamle, så ny henting vil ikke skje.


-->