## Migrating Postgres for update

We are looking to update to a newer postgres container. The current container data is stored in a disk called Giant.

1. Create new disk called in google cloud called Huge. This will store data for the new postgres.
2. Create data container (docker create -v /huge/pgdata:/var/lib/postgresql/data --name hugedata busybox)
3. Create postgres container (docker run --name hugepostgres -p 5432:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from hugedata postgis/postgis:13)
4. Import backed up data into new data container (start with just dola)
5. Test that the data can be reached and used
6. Once good to go, shut down both containers and restart huge with 5433:5432
