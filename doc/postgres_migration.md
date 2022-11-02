## Migrating Postgres for update

We are looking to update to a newer postgres container. The current container data is stored in a disk called giant.

#disregard for now
1. Create new disk called in google cloud called fast. This will store data for the new postgres.
2. Create data container (docker create -v /fast/pgdata:/var/lib/postgresql/data --name fastdata busybox)
## Steps
1. Create postgres container (docker run --restart unless-stopped --name postgres -p 5433:5432 -e POSTGRES_PASSWORD="egcdcatbhcab" -d --volumes-from fastdata -itd --shm-size=1g postgis/postgis:14-3.2)
2. sudo -i
3. mount /dev/sdb /fast/      (same as giant but should be able to remove giant eventually)
4. Import backed up data into new data container (start with just dola and newest acs)
5. Test that the data can be reached and used
6. Once good to go, load other acs databases
7. Once everything is tested and working, reconnect old postgres at 5432:5432 and delete the old databases.



