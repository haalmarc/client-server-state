---
layout: two-cols
layoutClass: gap-16
---

# Sync ved mutering

<FormLoading />

::right::

````md magic-move {lines: true}


```ts {9-12}
export function ProfileForm() {
  const [email, setEmail] = useState("");

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
  });

  const handleSubmit = (e: FormEvent) => {
    e.preventDefault();
    createUser(email);
  };

  return (

  );
}
```

```ts {11-12,20-23|7,13-17}
export function ProfileForm() {
  const queryClient = useQueryClient();

  const [email, setEmail] = useState("");

  const { data, error, isLoading } = useQuery({
    queryKey: ["userCount"],
    queryFn: fetchUserCount,
  });

  const mutation = useMutation({
    mutationFn: createUser,
    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: ["userCount"]
      });
    },
  });

  const handleSubmit = (e: FormEvent) => {
    e.preventDefault();
    mutation.mutate(email);
  };

  return (

  );
}
```

````

<!--
Men hva med når vi selv gjør endringer?

Akkurat nå lager vi en ny bruker, men det er ingenting her som sier at vi skal hente antall brukere på nytt.

[click] For å få til det, kan vi mate createUser-funksjonen vår inn i useMutate. Det er en hook fra TanStack Query, som tar seg av oppdateringer. Lignende det useQuery gjør for henting av data.

[click] Så kan vi om funksjonen vellykkes, invalidere cachen for antall brukere, så vi får nye data. Da vil vi få nytt tall med en gang vi oppretter en bruker. 

(demonstrer: skriv inn epost test@test.no og trykk opprett)

Dette er jo fremgang! Vi får synca servertilstanden idet brukeren gjør en handling. Men syns ikke dere det tok litt lang tid?

-->
