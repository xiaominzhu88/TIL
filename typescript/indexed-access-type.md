# Indexed access type

Look up a specific property on another type

```jsx
type Person = { age: number, name: string, alive: boolean };
```

```jsx
type Age = Person['age'];
const age = (arg: Age) => `Age: ${arg}`;
age(10); // Age: 10
age('10'); // Argument of type 'string' is not assignable to parameter of type 'number'.
```

```jsx
// keyof: union, the indexing type is itself a type
type Person1 = Person[keyof Person];
const person1 = (arg: Person1) => arg;
person1("Lola"); // Lola
person1(13); // 13
person1(["lola"]); // Argument of type 'string[]' is not assignable to parameter of type 'Person1'.
```

```jsx
// Using number: get the type of an array’s elements
// Combine with typeof to conveniently capture the element type of an array literal
const MyPets = [
	{ name: 'Lola', age: 13 },
	{ name: 'Mimi', age: 10 },
	{ name: 'Flo', age: 5 },
];
type Pets = (typeof MyPets)[number];
const pets = (arg: Pets) => `${arg.name}: ${arg.age}`;
pets({ name: 'Not a pet', age: 0 }); // Not a pet: 0
```
