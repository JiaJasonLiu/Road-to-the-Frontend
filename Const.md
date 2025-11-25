
# Type Assertion
```
export const new_data = {
	one: 'test1',
	two: 'test2',
} as const
```
the `as const` tells typescript that the new_data variable is readonly and the key-values are `literal types`, and not just `strings`.

So instead of it being something like `one: string` it is `readonly one: 'test1'`

### Benefits
- Can be used in type-safe [[unions]]
- makes keys/values immutable
-  preserves literal types (not widened strings)
- enables strong typing for derived unions