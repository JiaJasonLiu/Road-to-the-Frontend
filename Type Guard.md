feature to narrow down the type of the variable using conditional blocks (`switch cases`)
```
const handler = (test: Object) => {
	switch (test.type) {
		case 'one':
			console.log(test.name1)
		case 'two':
			console.log(test.name2)
	}
}
```

- helps with autocomplete