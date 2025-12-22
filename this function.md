
With a class
```javascript
class CustomerAPI {
construct(api, {
	super(api)
})
 public update(payload) {
	 this.api.proxy(
		 ...
	 )
 }
}
```
If I do this
`const CustomerAPI = new CustomerAPI(api)`
then if I use this method and pass it to a new component  
```
	mutationFn: CustomerAPI.update 
```
- It will loss `this.api` as it loses its context when this function is called

`this` is determined by how a function is called (not whether its pass-by-reference)
- Passing method directly losses the context -> wrapping it in a call on the object keeps it
Solution (Using ReactQuery mutation)
```
	mutationFn: (payload) => CustomerAPI.update(payload) 
```