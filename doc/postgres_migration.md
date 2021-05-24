## Migrating Postgres for update

We are looking to update to a newer postgres container. The current container data is stored in a disk called giant.

1. Create new disk called in google cloud called fast. This will store data for the new postgres.
2. Create data container (docker create -v /fast/pgdata:/var/lib/postgresql/data --name fastdata busybox)
3. Create postgres container (docker run --name fastpostgres -p 5432:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from fastdata postgis/postgis:13)
4. Import backed up data into new data container (start with just dola)
5. Test that the data can be reached and used
6. Once good to go, shut down both containers and restart fast with 5433:5432

Check mounting fastdata
