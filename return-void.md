In TypeScript type of `void` is interesting. It implies it doesn't have any type at all. So it is commonly used as the return type of functions that do not have return value.
But what if it is used with type of `any`? The first below code is technically valid in terms of TypeScript syntax.

```
var returnVoidFn = (): void => {
	let x: any = 1; // note type of `any`
	
	return x;
}

var returnVoidFn = (): void => {
	let x: number = 1;
	
	return x; // error because x is number type and the return type of the function is void
}
```

Although you the function `returnVoidFn` has `void` type as the return value, it can return type `any`. Probably we won't use that way intentionally.
But I had a chance to use it in Observables in Angular 2. When I tried to implement chaining of observables I used `do` operator. 
Its call-signature is like below.

```
do: (next?: (x: T) => void, error?: (e: any) => void, complete?: () => void) => Observable<T>;
```

As you see the `next` method has `void` type as the return value. But I wanted to return a observable to chain it like Promises. Although it is a right way or not, when I tried to do like below it worked fine without any compile error.

```
do(
 (): void => {
   return <any>httpService.get();
 }
)
```

There will be a better way to chain observables. But my interesting was that a type of `any` can be returned from a function with `void` as return value.
Although we won't use like that way it would be good to know about TypeScript.

