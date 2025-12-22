automatic type inference if I pass in the key, typescript would know the output is of certain type
# Utilized State
```ts
type GlobalState {
    user: { id: number; name: string };
    darkMode: boolean;
    counter: number;
}

declare const state: GlobalState; // Assume 'state' is declared globally
```

# Generic Function
#### The Type-Safe Function
Now, define the function using two generics `<>`:
1. **`StateT`**: The type of the object we are accessing (here, `GlobalState`).
2. **`KeyT`**: The type of the key being passed in.
``` ts
function getStateValue<StateT, KeyT extends keyof StateT>(
    state: StateT,
    key: KeyT
): StateT[KeyT] {
    return state[key]; // The return type is inferred as StateT[KeyT]
}
```
- **`<StateT, KeyT extends keyof StateT>`:**
    - `StateT` is the generic for the state object's type (e.g., `GlobalState`).
    - `KeyT` is the generic for the key. 
	    - By using **`extends keyof StateT`**, we restrict `KeyT` to only be one of the literal string/symbol types of `StateT`'s properties (i.e., `'user'`, `'darkMode'`, or `'counter'`).
- **`key: KeyT`:** The argument must be a valid key.
- **`: StateT[KeyT]` (Return Type):** This is the magic. 
	- It's a #LookupType** (indexed access type) that tells TypeScript: 
		- "The return type is the type of the property on `StateT` indexed by the type `KeyT`."
# Example
I don't need to specify the type within the `<>` as typescript can automatically infer this
```ts
const userValue = getStateValue(state, 'user');
// 💡 TypeScript infers 'userValue' as { id: number; name: string }

const darkModeValue = getStateValue(state, 'darkMode');
// 💡 TypeScript infers 'darkModeValue' as boolean

const counterValue = getStateValue(state, 'counter');
// 💡 TypeScript infers 'counterValue' as number
```
## Steps for tracing function call
#### Step A: Inferring the [[Generics]] ($StateT$ and $KeyT$)
When the function is called, the compiler looks at the arguments provided and fills in the generic placeholders:2
- Argument 1 (state): The value state has the type GlobalState. $$\text{Therefore, } \mathbf{StateT} \text{ is inferred as } \mathbf{GlobalState}.$$
- Argument 2 ('user'): The value 'user' is a string literal type.$$\text{Therefore, } \mathbf{KeyT} \text{ is inferred as the literal type } \mathbf{'user'}.$$
The constraint ($KeyT \text{ extends keyof } StateT$) is satisfied because `'user'` is indeed a key of `GlobalState`.

#### Step B: Calculating the Lookup Type ($StateT[KeyT]$)
The TypeScript compiler now plugs these inferred types into the function's specified return type: $\mathbf{StateT[KeyT]}$.
$$\text{Return Type} = \text{GlobalState}[\text{'user'}]$$
This is known as a **Lookup Type** (or Indexed Access Type). It tells the compiler to literally look up the property type on the `GlobalState` interface using the key `'user'`.
#### Step C: Final Result
The property `'user'` on `GlobalState` has the type:
$$\text{\{ id: number; name: string \}}$$
The compiler assigns this resulting type to the `userValue` constant.
$$\text{Therefore, } \mathbf{userValue} \text{ is precisely typed as } \mathbf{\{ id: number; name: string \}}$$
## Simplify
```ts
type GetStateValue = <KeyT extends keyof GlobalState>(
    key: KeyT
) => GlobalState[KeyT];

// Example usage (where 'get' is an implementation of GetStateValue):
// const user = get('user'); // Type: { id: number; name: string }
```

### The Role of Generics
1. **Capturing the Literal Type:** When you call the function `getStateValue(state, 'user')`, the generic $KeyT$ **captures the exact literal type** `'user'` (not just the broader type `string` or `keyof GlobalState`).
2. **Creating the Relationship:** The function signature uses the captured literal type to calculate the return type: `GlobalState['user']`.
3. **Without Generics:** If you tried to define the function without generics:
    TypeScript]
    ```ts
    // This would NOT work for inference
    function getStateValue(state: GlobalState, key: keyof GlobalState): ??? {
        return state[key];
    }
    ```
	- In this case, the `key` argument is simply typed as the union of keys (`'user' | 'darkMode' | 'counter'`). -> no type-safety
	- The return type would be the union of all possible value types: `GlobalState['user'] | GlobalState['darkMode'] | GlobalState['counter']`, which is `{ id: number; name: string } | boolean | number`. 
	- The compiler has no way to narrow it down to the specific type.
	! This may cause runtime errors

## Where Automatic Type Inference IS Used Without Generics
While the key-value lookup _requires_ generics, automatic type inference is one of TypeScript's core features and is used **everywhere** in simpler contexts, even without explicitly defined generics.

| **Context**              | **Example Code**                                       | **Type Inferred**                                                             |
| ------------------------ | ------------------------------------------------------ | ----------------------------------------------------------------------------- |
| **Variable Declaration** | `const count = 10;`                                    | `number`                                                                      |
| **Function Return Type** | `function add(a: number, b: number) { return a + b; }` | `(a: number, b: number) => number`                                            |
| **Array/Object Literal** | `const data = [1, 'two', true];`                       | `(number                                                                      |
| **Destructuring**        | `const { a, b } = { a: 10, b: 'hello' };`              | `a: number`, `b: string`                                                      |
| **Contextual Typing**    | `[1, 2, 3].map((item) => item * 2);`                   | `item` is inferred as `number` because `map` is called on a `number[]` array. |
# Summary
This is done through the use of **[[Generics]]** (The Placeholder), the **[[`keyof` operator]]** (The Constraint), and **[[Lookup Types (or Indexed Access Types)]]** (Mapping) .
# Links
[Lookup Types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-1.html): 