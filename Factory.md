a function or method that creates and returns objects
- Instead of using `new ClassName()`, you use a factory function to **encapsulate the creation logic**, which can include configuration, defaults, or conditional logic.
``` ts
function createUserWithDefaults(
  name: string,
  age: number = 18
): User {
  return new User(name, age);
}

const bob = createUserWithDefaults("Bob"); // age defaults to 18

```
