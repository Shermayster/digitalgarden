---
{"dg-publish":true,"dg-permalink":"web/indexeddb","permalink":"/web/indexeddb/"}
---

---
# IndexedDB (Browser Storage Workshop summary from FrontendMasters)

IndexedDB allows to store a large amounts of data in a browser.

![Image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/809B60F9-12FD-498E-A917-9A781915FACD/8C7ED055-DB9D-4188-95CD-1D7CD9FDEEB4_2/ns9R2jc0rZvgwU4E2yhuwiTyk7IWlxP4Elt9FHBrt3kz/Image.png)

`const q = await navigator.storage.estimate() ;`

+ ### IndexedDB characteristics

It's a NoSQL data store

It stores JavaScript objects or bytes

Every entry has a key

The API is asynchronous

No permission needed from user

It's available on Windows, Workers and Service Workers

When storing objects, IDB clones them, and **cloning** happens **synchronously -** *can be solved with web workers*

The API is event-based

With a thin wrapper we can convert it in a Promise-based API

It supports transactions - can combine several actions

It supports DB versioning - every time we change schema we can change the storage and migrate data

### Open a IndexedDB database with name and version

![Image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/809B60F9-12FD-498E-A917-9A781915FACD/3A6046A4-8FB3-4B7D-815A-F1F5BAC52C30_2/xKXoe3aUk4W1tTm9gPYTEAI5PYw0GGoJg6Nyt3JxAkAz/Image.png)

DB doesn’t exist: the browser checks for name -> not finding it -> fires **upgrade even**t and creates new DB with version

DB exist with smaller version: the browser checks name and version -> fires **upgrade** **event**. We need to decide what should be done with the data. It can be migrated, or deleted. -> opens db

DB exist with greater version: The browser will throw an error.

BD exist with same version: Will open the db **without upgrade event**.

### Updating IndexedDB store

Cloning an object is more expensive than the action itself. Bigger objects take longer to process. Moving functionality into a web worker or splitting large objects into smaller ones can improve performance.

![Image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/809B60F9-12FD-498E-A917-9A781915FACD/11C6CCCE-C8F3-427E-B8C5-5D1E511201B8_2/HkTI0POyxnexyqWj8fZsPfzEvQiShK1ZTU70hxxha90z/Image.png)

Index is like schema. It also enforces object in db to have a property. When creating an Index, you make your db large (without adding actual data). Adding an index will make you db slower.

**It’s possible to search by index**

![Image.png](https://res.craft.do/user/full/73194c2a-8262-dbc2-9d25-65597808e888/doc/809B60F9-12FD-498E-A917-9A781915FACD/D5D530F3-C7E2-45A8-BB55-11204680A901_2/D02RViwhnndgYe83Fuj7c1ZgVyvyPyOyo4UmGAJ3cpoz/Image.png)

It’s not possible to run complex scenarios (like join in SQA). There’s few libraries that allows to use SQL with Indexeddb

**Cursors**

Instead of loading all data in-memory storage, you can pull data one by one with cursors. Useful when you work with large amount of data.

