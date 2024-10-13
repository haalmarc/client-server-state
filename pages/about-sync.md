# Syncing

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
    refetchInterval: 1000 * 10,
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

Dermed er en utfordring i servertilstand å holde dataene oppdatert. TanStack Query lagrer dataene på en cache, og vil ikke i utgangspunktet hente nye data før dataene er regnet som gamle.

[click] Dette kan du styre med staleTime, som er satt til 5 minutter som standard. Om du ønsker oftere oppdateringer, kan du overstyre. 

[click] Det finnes også andre måter å hente nye data, som å bruke refetchInterval til å hente data hvert 10. sekund. refetchInterval vil hente ved gitt intervall, mens staleTime vil hente ved neste mulighet, som når brukeren går ut og inn av en side.

[click] Også er det også tilfeller vi ikke bryr oss om at andre endrer dataene i bakgrunn. Med mindre vi har et dashboard som vi ønsker live-updates fra eller har en maks brukergrense, så er det ikke så farlig om antall brukere ikke er oppdatert. Da kan vi sette staleTime til Infinity, som sier at dataene aldri kommer til å bli gamle, så ny henting vil ikke skje.


-->