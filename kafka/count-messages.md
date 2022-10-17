# Count of messages on a stream or topic.

Using ksqldb, it's easy to get a count of messages on a stream using:
```sql
select 'x' as x, count(*) as record_count from stream_name group by 'x' emit changes;
```

Be sure to have run this first:
```sql
set 'auto.offset.reset'='earliest';
```

If a stream does not already exist, one can be easily created for this purpose upon an existing topic.
```sql
create stream stream_name (KEY varchar KEY) with (KAFKA_TOPIC='topic_name', VALUE_FORMAT='JSON');
```

(Specify the `VALUE_FORMAT` as needed.)