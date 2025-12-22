The `keyof` operator is used in the constraint ($\text{KeyT extends **keyof** StateT}$) to enforce type safety. It generates a union type of all the public property keys of an object.
- Example: `keyof GlobalState` evaluates (returns) to `'user' | 'darkMode' | 'counter'`.
	- a union of string or numeric literal types
- This ensures that if you try to call `getStateValue(state, 'nonExistentKey')`, the compiler throws a direct error because `'nonExistentKey'` does not extend the union type.