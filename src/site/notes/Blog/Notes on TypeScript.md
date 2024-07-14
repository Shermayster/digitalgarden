---
{"dg-publish":true,"permalink":"/blog/notes-on-type-script/"}
---

# Notes on TypeScript
Recommended courses:
- [Type-Level TypeScript](https://type-level-typescript.com/)
>2023-09-25
- **TypeScript** manages types with `Sets`,  `any` breaks it because `any` can include everythig and can be single value. 
- Types system is hirarical. Type that belongs to some parent is  **subtype**. For example `type Name = ‘John’ | ‘Frank’`, is this case `’John’ | ‘Frank` will be subtype of `string`
- Every type is subtype of `unknown`. 
- `A | unknown` will be type of `unknown` because unknown includes `A`, if it’s `A` it’s also unknown.`A & unknown` will be `A`, because **inersecting means extracting** the part of A that belogns to B(unknown). Unknown is set that contains everything else.
- The result of intersection with two not overlapping types is `never`. For example `string & number` is equal to `never`. Never is empty set
- `A | never` is `A`
- `A & never` is `never`
- `A | any` or `A & any` will be `any`

## Objects
When you add type for an object, you **have no guarantee** that an **object** of some type **does not contain extra props**.
==**keyof**== - retrives the union of all keys in an object type
```typescript
type User {
	name: string;
	age: number;
	isAdmin: boolean;
}

type Keys = keyof User; // "name"| "age" | "isAdmin"
// you can write it like this
type UserValues = User[keyof User]

```
You can define optional properites with `?` key
```typescript
type User {
	name: string;
	age: number;
	isAdmin: boolean;
	tags?: string[];
}

```
### Merging object with intersections
```typescript
type Obj1 = {a: string};
type Obj2 = {b: number};

type Obj3 = Obj1 & Obj2; // { a: string; b: number; }
```
```typescript
type A = { a: string };
type KeyOfA = keyof A; // => 'a'

type B = { b: number };
type KeyOfB = keyof B; // => 'b'

type C = A & B;
type KeyOfC = keyof C; // => 'a' | 'b'
```

Here is the general rule:
```typescript
keyof (A & B) = (keyof A) | (keyof B)

keyof (A | B) = (keyof A) & (keyof B)
```

### Caveats of intersections of objects
1. Don’t merge objects with overlapping properting with diffrent type 
```typescript
type WithName = { name: string; id: string };
type WithAge = { age: number; id: number };
type User = WithName & WithAge;

type Id = User[“id”]; // => string & number <=> never
```

2. Interface have better performance: [Performance · microsoft/TypeScript Wiki · GitHub](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections
## Records
Just like Object types, Records also represent sets of objects. The difference is that **all keys of a record must share the same type**
`type InputState = Record<“valid” | “edited” | “focused”, boolean>;`

Or without using Record:
`type InputState = { [Key in “valid” | “edited” | “focused”]: boolean };`
The **Partial** generic takes an object type and returns another one that’s identical except that all of its properties are optional:
```typescript
type Props = { value: string; focused: boolean; edited: boolean };

type PartialProps = Partial<Props>;
// is equivalent to:
type PartialProps = { value?: string; focused?: boolean; edited?: boolean };
```
The **Required** generic does the opposite of Partial. It takes an object and returns another one that’s identical except that all of its properties are required:
```typescript
type Props = { value?: string; focused?: boolean; edited?: boolean };
type RequiredProps = Required<Props>;
// is equivalent to:
type RequiredProps = { value: string; focused: boolean; edited: boolean
```

The **Pick** generic removes all keys that aren’t assignable to the type of key given as second argument:
```typescript
type Props = { value: string; focused: boolean; edited: boolean };

type ValueProps = Pick<Props, “value”>;
// is equivalent to:
type ValueProps = { value: string };

type SomeProps = Pick<Props, “value” | “focused”>;
// is equivalent to:
type SomeProps = { value: string; focused: boolean };
```

The **Omit** generic removes all object properties that are assignable to the type given as second argument. It does the **opposite of Pick!**
```typescript
type Props = { value: string; focused: boolean; edited: boolean };

type ValueProps = Omit<Props, “value”>;
// is equivalent to:
type ValueProps = { edited: boolean; focused: boolean };

type OtherProps = Omit<Props, “value” | “focused”>;
// is equivalent to:
type OtherProps = { edited: boolean };
```