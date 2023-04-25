# Scaling up database writes

UURPS

1. Unnecessary
    1. writes? (Duplicate API calls?)
    2. indexes?
2. upgrade your machine
3. Primary/secondary replication 4. reads are handled by another machine 5. the main machine only deals with writes 6. introduces replication lag
4. Horizontal partitioning 5. will have multiple machines you can write to 6. example: US database, Australia database 7. split tables into separate machines 8. join will be tough 9. put users tweets into specific machines
5. Sharding????

## Sharding vs horizontal partitioning

????
