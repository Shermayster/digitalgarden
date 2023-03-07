---
{"dg-publish":true,"dg-permalink":"software-design/ddd","permalink":"/software-design/ddd/"}
---

# Domain Driven Design

DDD is a way to design software program. It most useful then you have to deal with complex domain so it helps to reduce complexity of the system. If domain is not complex, you should consider to use another software architecture technic.

## Three most important concepts in DDD
- Bounded context
- Ubiquitous language
- Focus on Domain model

Domain centric architecture

Why Use Domain-centric Architecture?

Pros

- Focus on domain
- Less coupling
- Allows for DDD

Cons

- Change is difficult
- Requires more thought
- Initial higher cost

![Image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/007B074C-2A4A-4CD6-86DB-17BFB78635FC/EB505290-6607-446B-A6F3-ED10DB53C2B3_2/vNGQRPnTmBsPBDHS6CoYCl6orqxYjDr9sUzzZdppv0Yz/Image.png)

Domain is most important part of application. You start working from domain and not tools

![Image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/007B074C-2A4A-4CD6-86DB-17BFB78635FC/293547D8-A89A-442B-A57A-A3D8D819C35D_2/AGsBWwbibBBEFW9ncri7gTYSifXjTIhsGwZH2dTHGJ8z/Image.png)

1. Collaborative - business people and developers are working together
2. Modeling - Structure of you code should model structure of the domain. Changes happens in domain easily can be found in a code.
3. Incremental - Don't do big architecture upfront. Code involves as your understanding of a domain grows.

![image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/007B074C-2A4A-4CD6-86DB-17BFB78635FC/1DB35D79-0366-45EF-BAFF-D1C9C2E32CCD_2/A0oQ5KM0rWHNTVkd5fbuDAjuhkIvyBZypOqBoxSiSvoz/image.png)

Domain defines code, but code also can affect on domain. You release your app and it can change domain.

DDD is based on Agile principles.

Agile is base on Inspect and Adapt.

1. Make a small change
2. Assess(feedback)
3. Inspect and adapt
4. Improve

**The most important part is release small changes and adapt according to feedback.**

**Stories in Agile**

- A short narrative
- A couple of sentence
- Describes end user performing a domain-driven, result-oriented task
- Describes your user's work

**Micro-services and Monoliths**

problems with Monolith

- Tends to access data only
- Hard to update
- Hard to deploy
- Hard to maintain
- Agility imposable

Advantages of Microservices

- Autonomous

**Bounded Contexts and Entities**

What are context?

What are the responsibilities of people working within that context?

**Entity vs Aggregate**

bounded context:

![image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/007B074C-2A4A-4CD6-86DB-17BFB78635FC/18C6C778-4321-472A-9578-699941ECB985_2/djx4OEGLkxFpz0Bc1nEsXOOwcudyMSp8xsDuO114lnsz/image.png)

You need to think about responsibilities of people working in context. People in warehouse have different context rather than in book store.

![image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/007B074C-2A4A-4CD6-86DB-17BFB78635FC/5EB07021-DB1C-4BBD-9921-41A5E5DBBDAE_2/SJxG7Cz4Mamy61J3jtdMxtiOJFkfvymQj84C4Sxnj14z/image.png)

One way to solve a problem with different context. It should a role| one person that should communicate with different context. Usually it happens in real life.

Context is entity. It has one job and doing only one thing and doing it only in specific context.

**An aggregate is a collection of entities you talk to through a single portal.**

Line between entity and aggregate can be fuzzy:

- Portal into aggregate my look like an entity, but when you drill down you'll see that portal uses other entities to accomplish tasks.

**Ubiquitous language**

In different context language may change. In warehouse book will have different properties than in shop. The language itself will be reflected within the code. Developer and architect should use this language with describing features.

Names

- Distinguish between actor(people) and roles (tasks)
- Actors may accomplish tasks in different roles
- Entities named after roles, not actor
