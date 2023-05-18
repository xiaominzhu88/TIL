# Object Types

```jsx
// readonly just means that Property itself ( 'resident' ) can’t be re-written to
interface Home {
  readonly resident: { name: string; age: number };
}


// Extending Types
// Interfaces can also extend from multiple types
interface Dog {
  age: number;
}
interface Cat {
  color: string;
}
interface Animal extends Dog, Cat {}


// Generic Object Types
// 'Box' as a template for a real type,
// where 'Type' is a placeholder that will get replaced with some other type
interface Box<Type> {
  contents: Type;
}
interface StringBox {
  contents: number;
}
interface ObjectBox {
  contents: { a: number; b: string };
}
```

Functions using types above 👇

```jsx
export function ObjectType() {
  function visitForBirthday(home: Home) {
    // We can read and update properties from 'home.resident'
    return `Happy birthday ${home.resident.name}! Age: ${
      home.resident.age + 1
    }`;
  }
 visitForBirthday({ resident: { name: "Lola", age: 12 } }); // Happy birthday Lola! Age: 13

  // We can't write to the 'resident' property itself on a 'Home'
  // because 'resident' is readonly!
  function evict(home: Home) {
    home.resident = {
      name: "Victor the Evictor",
      age: 42
    };
  }

  const getPets = (myPets: Animal) => {
    return `Lola is ${myPets.age} years old, i also want to have a ${myPets.color} cat.`;
  };
  getPets({ age: 13, color: "white" }) // Lola is 13 years old, she likes to have a white cat.


  let stringBox: Box<string> = { contents: "Hello" };
  console.log(stringBox.contents); // Hello

  let numberBox: StringBox = { contents: 4 };
  console.log(numberBox.contents); // 4

  let objectBox: ObjectBox = { contents: { a: 4, b: "Hello" } };
  console.log(`{${objectBox.contents.a} - ${objectBox.contents.b}`); // 4 - Hello
```
