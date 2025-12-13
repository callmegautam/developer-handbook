```ts
type User = {
  id: number;
  name: string;
};

type UpdateUser = Partial<User>;

```


```ts

type UserPreview = Pick<User, "id" | "name">;


```


```ts

type UserWithoutId = Omit<User, "id">;


```

```ts

type Status = "idle" | "loading" | "success";

type ActiveStatus = Exclude<Status, "idle">;
// "loading" | "success"



```


