[Home](index) > [Developer](Developer) > [DevOps](DevOps) > **Database Troubleshooting**
***

CHEFS uses the PostgreSQL database with high availability provided by Patroni. As CHEFS users increase the database grows both in size and the number of queries that it has to process. The queries must be very efficient, otherwise they will become a bottleneck, the load on the database will grow until it reaches the CPU limit, and then API calls will begin to fail.

## Basic Monitoring (TODO)

## Using `pg_stat_statements`

Using the primary database pod, check if the `pg_stat_statements` extension is installed:

```sql
SELECT * FROM pg_extension WHERE extname = 'pg_stat_statements';
```

If not then check that it's available:

```sql
SELECT * FROM pg_available_extensions WHERE name = 'pg_stat_statements';
```

It should be there! If it isn't then you're on your own. To install the extension:

```sql
CREATE EXTENSION pg_stat_statements;
```

Now re-check that the extension is installed:

```sql
SELECT * FROM pg_extension WHERE extname = 'pg_stat_statements';
```

Doing a `SELECT` for the view should fail:

```sql
SELECT * FROM pg_stat_statements;
```
> SQL Error [55000]: ERROR: pg_stat_statements must be loaded via shared_preload_libraries

You need to edit the Patroni configuration, which is fun because Patroni uses a minimalist container that doesn't have an editor like `ed` or `vi`.

1. Open a terminal for one of the database pods.
1. Temporarily install `busybox` to use it as an editor:
    1. ```sh
       export EDITOR=/tmp/vi
       ```
    1. ```sh
       curl https://busybox.net/downloads/binaries/1.35.0-x86_64-linux-musl/busybox --output $EDITOR
       ```
    1. ```sh
       chmod 700 $EDITOR
       ```
1. Now's the time to use the fancy Patroni editing:
   ```sh
   patronictl edit-config
   ```
1. Add `shared_preload_libraries: pg_stat_statements` under `parameters` (keep them in order - we love alphabetizing things!). Save the file and choose `Y` to apply the changes. This will update `/home/postgres/pgdata/pgroot/data/patroni.dynamic.json`, and then updates `/home/postgres/pgdata/pgroot/data/postgresql.conf`
1. Delete the editor:
   ```sh
   rm $EDITOR
   ```
1. Restart Patroni - this does not restart the pods, there is no outage:
   ```sh
   patronictl restart master
   ``` 

Done! `pg_stat_statements` can now be used to find long-running queries.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)