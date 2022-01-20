# Cassandra

## Run in local

```
docker-compose up
```

## Basics

- keyspace

    ```
    CREATE KEYSPACE "test" WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : '1' };
    ```
- table
    ```
    CREATE TABLE test.foo (a int, b text, PRIMARY KEY(a)) WITH cdc=true;
    ```

    ```
    cassandra@cqlsh:test> desc table foo;

    CREATE TABLE test.foo (
        a int PRIMARY KEY,
        b text
    ) WITH bloom_filter_fp_chance = 0.01
        AND caching = {'keys': 'ALL', 'rows_per_partition': 'NONE'}
        AND comment = ''
        AND compaction = {'class': 'org.apache.cassandra.db.compaction.SizeTieredCompactionStrategy', 'max_threshold': '32', 'min_threshold': '4'}
        AND compression = {'chunk_length_in_kb': '64', 'class': 'org.apache.cassandra.io.compress.LZ4Compressor'}
        AND crc_check_chance = 1.0
        AND dclocal_read_repair_chance = 0.1
        AND default_time_to_live = 0
        AND gc_grace_seconds = 864000
        AND max_index_interval = 2048
        AND memtable_flush_period_in_ms = 0
        AND min_index_interval = 128
        AND read_repair_chance = 0.0
        AND speculative_retry = '99PERCENTILE';
    ```
- insert

    ```
    cassandra@cqlsh:test> insert into foo(a,b) values (1, 'test');
    cassandra@cqlsh:test> select * from foo;

    a | b
    ---+------
    1 | test

    (1 rows)
    ```

## Configurations

`cassandra.yaml`

- [Change Data Capture (CDC) logging](https://docs.datastax.com/en/cassandra-oss/3.x/cassandra/configuration/configCDCLogging.html)
    - [Change Data Capture](https://cassandra.apache.org/doc/3.11.3/operating/cdc.html)


## Reference

- https://github.com/docker-library/cassandra
- https://hub.docker.com/_/cassandra
