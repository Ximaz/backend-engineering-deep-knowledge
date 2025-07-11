# ACID model

This document covers what I learnt about the ACID database model.

## A stands for Atomicity

Atomicity means that when a transaction is executed, it must either fully
complete or cancel all operations, even the one that previously succeeded on
the same transaction.

Let us consider a banking system. If a user A sends money to user B, it would
create a transaction of two operations. The first one would decrease user A's
wallet value while the second one would increase user B's wallet value.
If the first operation fails, nothing changes. If the second operation fails,
meaning that the first one, which decreases user A's wallet value, succeeded,
then it rolls back to the initial state, cancelling the decrease opeartion, as
there was an issue while fulfilling the transaction.

## C stands for Consistency

Consistency means that all users pulling data from the database must receive
the same results.

Let us consider an e-commerce website, where only one article is on stock. If a
customer buys it, all other customers must not be able to buy it as there is no
more in stock.

## I stands for Isolation

Isolation means that if multiple transactions are executed concurrently, the
outcome would look similar to if the transactions were sequentially executed.

To illustrate this concept, here is an example extracted from [this article](https://en.wikipedia.org/wiki/Isolation_(database_systems)):

<table>
    <tr>
        <td>Transaction 1</td>
        <td>Transaction 2</td>
    </tr>
    <tr>
        <td><pre lang="sql">
BEGIN;
SELECT age FROM users WHERE id = 1;
-- retrieves 20
</pre></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td><pre lang="sql">
BEGIN;
UPDATE users SET age = 21 WHERE id = 1;
-- not commited yet
</pre></td>
    </tr>
    <tr>
        <td><pre lang="sql">
SELECT age FROM users WHERE id = 1;
-- READ UNCOMMITTED retrieves 21 (dirty read)
-- READ COMMITTED retrieves 20 (dirty read has been avoided)
-- REPEATABLE READ retrieves 20 (dirty read has been avoided)
-- SERIALIZABLE retrieves 20 (dirty read has been avoided)
</pre></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td><pre lang="sql">ROLLBACK;</pre></td>
    </tr>
</table>

In this example, and depending on the isolation level, `Transaction 1` would
always return `20` for the age query, because `Transaction 2` was not commited.
The data did not change because of that.

## D stands for Durability

Durability means that when a transaction is committed, it remains committed
even if a system failure occures.
