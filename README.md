# radius_voip
Accounting service for VoIP Gateways
Docker image name **vkushnir/radius:voip**

## Environment variables for container


    DB_DRIVER=oracle
>Set the database driver to one of:
>- **oracle**
>- **mysql** *not implemented yet*
>- **mssql** *not implemented*
>- **postgresql** *not implemented*


    DB_SERVER=localhost
    DB_USER=username
    DB_PASSWORD=password
    DB_NAME=database
    DB_PORT=1521
>*connection info*


    RAD_ACCT1=radacct
    RAD_ACCT2=radacct
>*If you want both stop and start records logged to the same SQL table, leave this as is.  If you want them in different tables, put the start table in acct_table1 and stop table in acct_table2*


    RAD_POSTAUTH=radpostauth
>*Allow for storing data after authentication*


    RAD_CHECK=radcheck
    RAD_REPLY=radreply

    RAD_GROUPCHECK=radgroupcheck
    RAD_GROUPREPLY=radgroupreply

    RAD_USERGROUP=radusergroup
>*Table to keep group info*


    READ_GROUPS=yes
>*If set to 'yes' (default) we read the group tables*
>*If set to 'no' the user MUST have Fall-Through = Yes in the **radreply** table*


    DELETE_STALE=yes
>*Remove stale session if **checkrad** does not see a double login*


    SQL_TRACE=yes
>*Print all SQL statements when in debug mode (-x) to ${logdir}/sql*race.sql*


    SQL_SOCKS=20
>*Number of sql connections to make to server*
>*Setting this to LESS than the number of threads means that some threads may starve, and you will see errors like "No connections available and at max connection limit"*
>*Setting this to MORE than the number of threads means that there are more connections than necessary.*


    SQL_DELAY=120
>*Number of seconds to dely retrying on a failed database connection (per_socket)*


    SQL_LIFETIME=0
>*Lifetime of an SQL socket.  If you are having network issues such as TCP sessions expiring, you may need to set the socket lifetime.  If set to non-zero, any open connections will be closed "lifetime" seconds after they were first opened.*


    SQL_QUERIES=0
>*Maximum number of queries used by an SQL socket.  If you are having issues with SQL sockets lasting "too long", you can limit the number of queries performed over one socket.  After "max_qeuries", the socket will be closed.*
>*Use **0** for "no limit".*


    READ_CLIENTS=no
>*Set to 'yes' to read radius clients from the database ('nas' table)*
>*Clients will ONLY be read on server startup.  For performance and security reasons, finding clients via SQL queries CANNOT be done "live" while the server is running.*


    NAS=nas
>*Table to keep radius client info*

Environment variables from **vkushnir/freeradius:2-oracle**

    ENV RADIUS_USER="freerad"
    ENV RADIUS_GROUP="freerad"
>*Username and group used to run FreeRADIUS server*


    ENV RADIUS_UID="105"
    ENV RADIUS_GID="107"
>*UID and GID set according to host system*
