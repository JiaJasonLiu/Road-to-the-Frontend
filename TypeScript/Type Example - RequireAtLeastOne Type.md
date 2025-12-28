``` ts
type RequireAtLeastOne<T> = {
  [K in keyof T]-?: Required<Pick<T, K>> & Partial<Pick<T, Exclude<keyof T, K>>>
}[keyof T]
```
- `[K in keyof T]-?` this property (K) is valid only if it has the same name as any property of T.
- `Required<Pick<T, K>>` makes a new type from T with just the current property in the iteration, and marks it as required
	- Constructs a type by picking the set of properties `Keys` (string literal or union of string literals) from `Type`.
		- e.g `Pick<Todo, "title" | "completed">`;
- `Partial<Pick<T, Exclude<keyof T, K>>>` makes a new type with all the properties of T, except from the property K.
- `&` is what unites the type with only one required property from `Required<...>` with all the optional properties from `Partial<...>`.
- `[keyof T]` ensures that only properties of T are allowed.

Works using Typescript [[TODO - Utility Types]]