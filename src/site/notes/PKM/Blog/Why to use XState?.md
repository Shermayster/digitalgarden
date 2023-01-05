---
{"dg-publish":true,"dg-permalink":"state-management/why-to-use-xstate","permalink":"/state-management/why-to-use-xstate/"}
---

- Direct changing of the state will spread  logic across UI component. UI and logic will be mixed. Will be hard to decouple/break down in the future. Is harder to understand. Components should be pure. 
- It's battle tested. The library has a lot of extension is quite popular.
- It's base on State machines. State machines are used mostly in hardware, it was much hard patch software inside hardware. Many developers used state machines to reduce possible bugs. 

Use cases:
- Multi step form with complex flow

### Pros
 - It has almost all benefits of Redux. 
	 - Logic reuse 
	 - robust dev tools
- It's readable. Logic and flow is easy to understand.
- It's much harder to make a bug with Xtate. 

### Cons
- TypeScript and Xstate is hard to get work together. They trying to solve it, but it's very challenging.
- In most cases you don't need Xstate. You can use same principles with enum state, but if component logic gets complex Xstate can a good option.
- Learning curve. It's a powerful library, but it takes time to learn. There are good courses on Frontend Masters. 

### Resources:
- https://kentcdodds.com/blog/implementing-a-simple-state-machine-library-in-javascript
