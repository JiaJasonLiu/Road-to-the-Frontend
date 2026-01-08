```ts

function func<T extends string = string>(
)
```

The `extends` keyword acts as a **gatekeeper**. It tells TypeScript: "You can use any type you want for `T`, as long as it is a `string` or a subtype of `string` (like a specific string literal)."`