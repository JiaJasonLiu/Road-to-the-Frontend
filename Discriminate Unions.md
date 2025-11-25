https://dev.to/darkmavis1980/what-are-typescript-discriminated-unions-5hbb
```
type Vehicle = {
	name: string,
} & (Car | Bike);

type Car = {
	doors: number;
}
```



Handle this data use [[Type Guard]]