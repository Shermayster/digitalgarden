---
{"dg-publish":true,"permalink":"/notes/blog/notes-on-type-script/"}
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