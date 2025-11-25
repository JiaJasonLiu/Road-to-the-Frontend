https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types

```
SomeType extends OtherType ? TrueType : FalseType;
```

This works when you are making a generic type like

```
interface Animal {
	live: boolean;
}

interface Dog extends Animal {
	bark(): void;
}

type Puppy = Dog extends Animal ? Animal : undefined
%% Puppy is type Animal %%

%% or %%

type Bob = Random extends Animal ? Animal : undefined 
%% Bob is type undefined %%
```
Explanation: If its true that the type (e.g. `Dog`) extends `Animal`, we get the type `Animal`
- This is a simple functionality, but to fully utilize it we can use generics
