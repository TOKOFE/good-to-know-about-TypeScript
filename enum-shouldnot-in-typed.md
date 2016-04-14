## No Enums in Type Definition file

As we work with TypeScript, we need to create typing files to define shapes of our classes. It will be defined with `interface` and the file should be `.d.ts`.
We can define something like below. 

`type-sample.d.ts` file
```
export interface OutPutEventData {
  event: any;
  data: any;
}
```

The definition files are needed only during compile time. So they are not generated in JavaScript file. When you checked with compiled files you will notice there is no such interface files.
It means you shouldn't define any objects to be used in run time. One of the objects is `enums`. Some people might be confused `enums` can be defined in the type definition files.
But `enums` are a collection of related values and used at run time. So if you define it in the typing file errors will be occured during run time.

For example, let's say you define `enum` like below.

```
enum Tristate {
    False,
    True,
    Unknown
}
```

The above code will be translated like below

```
var Tristate;
(function (Tristate) {
    Tristate[Tristate["False"] = 0] = "False";
    Tristate[Tristate["True"] = 1] = "True";
    Tristate[Tristate["Unknown"] = 2] = "Unknown";
})(Tristate || (Tristate = {}));
```

To sum up, `enum` shouldn't be defined in the typing files. You can define it in the same class files or other separate configurations.

### Reference

[Enums](https://basarat.gitbooks.io/typescript/content/docs/enums.html)
