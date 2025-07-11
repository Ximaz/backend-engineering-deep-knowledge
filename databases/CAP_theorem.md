# CAP theorem

This document covers what I learnt about the CAP theorem.

## C stands for Consistency

Consistency means that each Read operation returns the most recent Write data
or an error

## A stands for Availability

Availability means each request received by a non-failing node must result in a
response.

## P stands for Partition tolerance

Partition tolerance means that the system continues to operate even if some
message are dropped or delayed by the network between nodes.

### Network failure management

When a network issue occures, the system has two ways to handle the operation :
- cancel : less availability, more consistency;
- proceed : more available (not High Availability though), less consistent.
