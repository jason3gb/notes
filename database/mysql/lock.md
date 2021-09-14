# Lock Types

## Basic Lock Types

- Shared & Exclusive Locks (reduce read & write operation lock contention)
- Intention Locks (multiple granularity locks)
- Record Lock
    - lock a record (select for update)
    - always lock the clustered index

## Advanced Lock Types

### Gap Lock

Locks that lock the gap between the first indexed value and the last indexed value, usually occurs in a select statement with a range where condition.

### Next-key Lock

The next-key lock is a conbination of index-record lock + gap lock with a range from the previous indexed value to the current record's value. 

The default repeatable-read isolation level enables the next-key lock which prevents the phantom row problem.

<br></br>


# Transaction Model

### Isolation Level

#### Repeatable Read

- Mysql Default isolation level, MVCC for consistent non-blocking reads, which means all reads in same transaction sees the same snapshot of the database state
- For locking reads, the lock uses next-key locking as the default when scanning the clustered index of the table, except for the column with unique index.
- Locks acquired on rows do not satisfy the condition is released after the lock read statement, which is slightly different from the read-committed isolation level. (this is truely confusing, since the locks on record satisfy the condition would be retained until the end of the transaction, we should build up an intuitive understanding on how all the things should work)

### Read Committed

- No next-key lock for locked read, only record lock
- Lock release after scanned, retained only when the where condition satisfied

### Others

Read Uncommitted and Serialization would probably never be encountered in your career, just save some space for your memory. :)

## Locking Reads

- Select for update set an exclusive next-key lock / record lock on the elements scanned, depending on the isolation level
- Select lock in share mode set a shared next-key lock / record lock ...
- For lock reads, all the locks acquired is retained until the end of the transaction.

<br></br>

# Lock set criteria

Must read the whole Reference: https://dev.mysql.com/doc/refman/5.7/en/innodb-locks-set.html

The reference basically introduce all the scenarios about how specifiy sql statements work with the lock system.

