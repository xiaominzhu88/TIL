# Generics: all about relating two or more values with the same type!

```jsx
// *Type* as a link between the input of the function (the array) and the output (the return value )
  function firstEl<Type>(arr: Type[]): Type | undefined {
    return arr[0];
  }
 firstEl(["Apple", "Orange", "Kiwi"]); // Apple
 firstEl([1, 2, 3]); //  1
 firstEl([]); // undefined!

  // Multiple type parameters e.g map()
  function map<Input, Output>(
    arr: Input[],
    fn: (arg: Input, idx: number) => Output
  ) {
    return arr.map(fn);
  }
map(["Apple", "Orange", "Kiwi"], (str, idx) => `${idx}: ${str}  `); // 0: Apple 1: Orange 2: Kiwi
map([1, 2, 3], (num, idx) => idx + num); // 135

// Constrains:  limit the kinds of types that a type parameter can accept.
  function longest<
    Type extends {
      length: number;
    }
  >(a: Type, b: Type) {
    if (a.length >= b.length) {
      return a;
    }
    return b;
  }

longest([1, 2], [1, 2, 3]); // 123
longest("Kiwi", "Orange"); // Orange
longest(4, 2); // Error: Argument of type 'number' is not assignable to parameter of type '{length: number;}',
              // because number type doesn’t have a .length property

  // Specifying Type Arguments
  function combineTwo<Type>(arr1: Type[], arr2: Type[]): Type[] {
    return [...arr1, ...arr2];
  }

// Type: string | number
combineTwo<string | number>([1, 2, 3], [", hello"]); // 123, hello
combineTwo([1, 2, 3], [", hello"]); // Error: Type 'string' is not assignable to type 'number'!
                                      // function is called with mismatched arrays!

  // Type parameters are for relating the types of multiple values.
  // If a type parameter is only used once in the function signature,
  // it’s not relating anything, then write in a simpler way 👇
  function sayHello(val: string) {
    return "Hello, " + val + " 🐶!";
  }

sayHello("Lola"); // Hello, Lola 🐶!
```
