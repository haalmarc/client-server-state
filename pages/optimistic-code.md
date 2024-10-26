---
transition: fade
layout: two-cols
layoutClass: gap-16
---

# Optimistisk oppdatering

````md magic-move {lines: true}

```ts {0}
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

```ts {2,9|10-12|14-15|17-21,24}
export function ProfileForm() {
  const mutation = useMutation({
    mutationFn: createUser,
    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: ["userCount"]
      });
    },
    onMutate: async (newEmail: string) => {
      await queryClient.cancelQueries({ 
        queryKey: ["userCount"] 
      });

      const previousUserCount = queryClient
        .getQueryData<number>(["userCount"]);

      // 👇 Steg 1
      queryClient.setQueryData<number>(["userCount"], 
        (previousState) =>
          previousState + 1
      );

      return { previousUserCount };
    }, // 👈 Steg 2
  });

  return (

  );
}
```

```ts {16,18-24}
export function ProfileForm() {
  const mutation = useMutation({
    onMutate: async (newEmail: string) => {
      await queryClient.cancelQueries({ 
        queryKey: ["userCount"] 
      });

      const previousUserCount = queryClient
        .getQueryData<number>(["userCount"]);

      queryClient.setQueryData<number>(["userCount"], 
        (previousState) =>
          previousState + 1
      );

      return { previousUserCount };
    },
    // 👇 Steg 3b
    onError: (err, newEmail, context) => {
      queryClient.setQueryData<number>(
        ["userCount"],
        context?.previousUserCount
      );
    },
  });

  return (

  );
}
```

```ts {10-15}
export function ProfileForm() {
  const mutation = useMutation({
    ...
    onError: (err, newEmail, context) => {
      queryClient.setQueryData<number>(
        ["userCount"],
        context?.previousUserCount
      );
    },
    // 👇 Steg 3
    onSettled: () => {
      queryClient.invalidateQueries({
        queryKey: ["userCount"] 
      });
    },
  });

  return (

  );
}
```

````

::right::

<ol>
  <li>Vi endrer server-tilstanden med en gang</li>
  <li>Vi sender en forespørsel til serveren</li>
  <li>Etter forespørselen er fullført: 
    <ul>
      <li>a) hvis suksess: oppdater server-tilstanden med de faktiske dataene</li>
      <li>b) hvis kallet feiler: rull tilbake</li>
    </ul>
  </li>
</ol>

<!--
Nå har vi sett på mønsteret hvordan implementerer vi det i kode?

[click] Det er litt forberedelser før vi får oppdatert servertilstanden. Inni useMutation, er det onMutate-callbacken vi endrer på, for å definere hva som skjer når forespørselen skjer.

[click] Først stopper vi alle pågående forespørsel på userCount, for å unngå race conditions.

[click] Så tar vi vare forrige tilstand, tilfelle vi skal rulle tilbake.

[click] **SÅ** kan vi oppdatere tilstanden i React Query til å ha gammel tilstand + 1, siden vi legger til en bruker.

Så vil forespørselen bli sendt. 

[click] Om forespørselen feiler, ruller vi tilbake til gammel tilstand umiddelbart.

[click] Uansett om forespørselen feiler eller ikke, invaliderer vi cachen, så vi syncer klientens servertilstand med serverens faktiske data.

-->
