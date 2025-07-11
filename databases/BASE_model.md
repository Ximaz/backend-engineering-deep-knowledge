# BASE Model

This document covers what I learnt about the BASE database model.

## BA stands for Basically Available

Basically Available means that concurrent access to the database is available.
There is no need for a user to wait for a transaction to end before updating
the same record with another one.

## S stands for Soft State

Soft State implies that data may have a temporary state taht may vary in time
even without trigger or external source. The Soft State represents the record's
transaction state whilst different entities update it concurrently. The record
is then saved once all transactions are ended.

## E stands for Eventual Consistency

Eventual Consistency implies that records achieve consistency once all
concurrent transactions are completed. There is no such thing as intermediate
reading. If transactions are executed to transalte record 1 to record 2, the
queries will return record 1 until all transactions are done, where as in the
ACID model, each query would return the result of the previously executed
transaction, meaning we could have intermediate up-to-date records.
