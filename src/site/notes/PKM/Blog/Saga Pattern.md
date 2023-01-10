---
{"dg-publish":true,"dg-permalink":"pattern/saga-pattern","permalink":"/pattern/saga-pattern/"}
---

https://www.youtube.com/watch?v=xDuwrtwYHu8
http://www.cs.cornell.edu/andru/cs711/2002fa/reading/sagas.pdf
Originally come for databases. Sagas is a Long Lived Transactions

> A Saga is a **Long Lived Transaction** that can be written as a sequence of transactions that can be interleaved.
   All transactions in the sequence complete successfully or compensating transactions are ran to amend a partial execution.

We can describe Saga as a collection of sub-transactions. The first step towards Saga is breaking down a transaction into small sub-transactions. It should **not** be possible for them to rely on each other or receive input from one another. Each sub-transaction has its own compensation transaction, and they shouldn't depend on each other as well. 
In some cases, there is no way to return to the previous state in case of failure.

> Trade-Off: Atomicity for Availability

Sub-transactions will be fired without particular order and will be finished before main transaction will be finished.

Sagas gives a robust Failure Management System. Most used mechanism is `Backwards Recovery`, taking required steps to return to previous state `req -> failed -> cancel other request in saga`
