
Abbreviations:
* MB: Metabase
* DB: database

# Installing New Java Version

Normally, the `metabase.jar` file will require Java 11+ (as of 2023), so follow these steps, especially if you're planning on [migrating](#Migrating%20from%20H2%20DB%20of%20Metabase%20to%20PostgreSQL) or [upgrading](#To%20Upgrade%20Metabase%20on%20Docker) Metabase:


1. Download Java 11 from [here](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html#:~:text=Windows%20x64%20Installer,141.41%20MB) and install it.
2. Open Java configuration:
   
   ![](Media-Temp/Pasted%20image%2020240205172503.png)
   
3. Add new Java path:
   
   ![](Media-Temp/Pasted%20image%2020240205172726.png)
   
If you don't do this, then in the [migrating](#Migrating%20from%20H2%20DB%20of%20Metabase%20to%20PostgreSQL) section, you may get this error:

`Exception in thread "main" java.lang.UnsupportedClassVersionError: jakarta/servlet/http/HttpServletRequest has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0`

# Migrating from H2 DB of Metabase to PostgreSQL

#docker   #metabase   #postgresql

Most of the steps are taken from [here](https://www.metabase.com/docs/latest/installation-and-operation/migrating-from-h2#docker-how-to-migrate-from-h2-to-your-production-application-database) to migrate. Environment variables [page](https://www.metabase.com/docs/latest/configuring-metabase/environment-variables) might also be useful.

1. In the project's root directory (I'll refer to it as `PROJ` from now on), create `metabase_h2_backup` directory.
2. Copy `metabase.db` directory from MB's docker container to `metabase_h2_backup`:
   
   ![](Media-Temp/Pasted%20image%2020240205140932.png)
   
3. Extract the `.db` files inside the `metabase.db` directory to the outside and delete `metabase.db` directory such that the `metabase_h2_backup` directory looks like this:
   
   ![](Media-Temp/Pasted%20image%2020240205141136.png)
   
4. In `metabase_h2_backup` directory, install the [version of](https://www.metabase.com/docs/latest/releases) `metabase.jar` file that is the same as the version of your production metabase at the time of installation, which can be seen here:
   
   ![](Media-Temp/Pasted%20image%2020240205143151.png)
   
5. Make sure the PostgreSQL container is running (I don't know if it is ok to run the production Metabase container as well, but I remember running it while doing this and no problems happened).
6. Run the following commands in command prompt (cmd):

```cmd
set MB_DB_TYPE=postgres
set MB_DB_DBNAME=postgres
set MB_DB_PORT=5432
set MB_DB_USER=<username of MB_DB_USER_FILE in docker-compose.yml file>
set MB_DB_PASS=<username of MB_DB_PASS_FILE in docker-compose.yml file>
set MB_DB_HOST=localhost
java -jar metabase.jar load-from-h2 "<ABSOLUTE_PATH_OF_metabase_h2_backup_DIR>"
```

Look at the YAML example section below to visualize the `MB_DB_USER_FILE`

# To Upgrade Metabase on Docker

#docker   #metabase   #postgresql


Check [this](https://www.metabase.com/docs/v0.48/installation-and-operation/upgrading-metabase).



# Example of Docker Compose YAML File for Metabase
   
#docker   #metabase   #postgresql

```yaml
# base code is from metabase documentation:
# https://www.metabase.com/docs/latest/installation-and-operation/running-metabase-on-docker#use-docker-secrets-to-hide-sensitive-parameters

# "version" here refers to the version of the docker-compose file (.yml), not the version of the docker engine
# source: https://stackoverflow.com/questions/76156527/what-does-the-first-line-in-the-docker-compose-yml-file-that-specifies-the-ve
version: '3.9'
# "name" will change the compose's name. This is optional
# source: https://stackoverflow.com/questions/68357205/docker-compose-change-name-of-main-container
name: metabase-postgresql-mssql-compose
services:

  #
  # configuring metabase service
  #

  metabase:
    image: metabase/metabase:latest
    container_name: metabase
    hostname: localhost
    volumes:
      - type: bind # so if we delete the container, the data will still be there in the `source` (i.e., in the host machine)
        source: ./metabase_data
        target: /metabase.db # should be empty, since we're using Postgres for MB's system files instead of H2
      # # side note: run the command below instead of type/source/target above if you want to use named volumes
      # - metabase_data:/var/lib/metabase/data/
    ports: 
      - 3000:3000
    environment:
      MB_DB_TYPE: postgres # same as POSTGRES_DB in `postgres` service below
      # even though you specify the name of the DB here,
      # you'll still probably need to use 'master' as the DB name when connecting to Metabase
      MB_DB_DBNAME: postgres
      MB_DB_PORT: 5432
      # the 
      MB_DB_USER_FILE: /run/secrets/db_user
      MB_DB_PASS_FILE: /run/secrets/db_password
      MB_DB_HOST: postgres # same as host of `postgres` service below

    networks:
      metabase_postgres_mssql_network:
        aliases:
          - metabase_nsa # network-scoped alias
    secrets:
      - db_password
      - db_user
    healthcheck:
      test: curl --fail -I http://localhost:3000/api/health || exit 1
      interval: 15s
      timeout: 5s
      retries: 5

  #
  # configuring Postgres DB 
  # for storing Metabase's system files, as we can't use MSSQL for this, details:
  # https://www.metabase.com/docs/latest/installation-and-operation/migrating-from-h2#supported-databases-for-storing-your-metabase-application-data
  # 

  postgres:
    image: postgres:latest
    container_name: postgres-for-metabase
    hostname: localhost
    volumes:
      - type: bind
        source: ./postgres_data_for_metabase
        target: /var/lib/postgresql/data 
      # # side note: run the command below instead of type/source/target lines above if you want to use named volumes
      # - postgres_data_for_metabase:/var/lib/postgresql/data/
    ports:
      - 5432:5432
    environment:
      # for some reason, when naming the db anything else, it doesn't get created
      # so we're currently resorting to the default DB name: "postgres"
      POSTGRES_DB: postgres # same as METABASE_DBNAME in metabase service above
      # the postgres DB will now have the same username/pass. as MSSQL DB, since they both use the same secrets
      POSTGRES_USER_FILE: /run/secrets/db_user
      POSTGRES_PASSWORD_FILE: /run/secrets/db_password
    networks:
      metabase_postgres_mssql_network:
        aliases:
          - postgres_sys_files_nsa # network-scoped alias
    secrets:
      - db_password
      - db_user

  #
  # configuring MSSQL DB 
  # for storing business-related data
  #

  mssql:
    image: mcr.microsoft.com/mssql/server:2019-CU23-ubuntu-20.04
    container_name: mssql-for-metabase
    hostname: localhost
    volumes:
      - type: bind
        source: ./mssql_data_for_metabase
        # side note (optional): to manually backup `target` to place other than `source`, follow these steps:
        # using docker desktop -> containers left tab -> mssql-for-metabase -> Files top tab, 
        # you can also backup ("save") /var/opt/mssql/.system/ and /var/opt/mssql/log/ folders as well for backup purposes.
        target: /var/opt/mssql/data 
      # # side note: run the command below instead of type/source/target lines above if you want to use named volumes
      # - mssql_data_for_metabase:/var/lib/mssql/data/
    ports:
      - 1433:1433
    environment:
      # Details about possible environment variables can be found here:
      # https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-configure-environment-variables?view=sql-server-ver16#environment-variables 
      # But apparently, the following environment variable will not work with mssql env_file: ./mssql.env,
      # that's why we had to strong type the password below along with extra details in ./mssql.env
      # However, if you want to circumvent this issue, follow this resource:
      # https://www.dbi-services.com/blog/managing-sql-server-sa-credentials-with-docker-secrets-on-swarm/
      ACCEPT_EULA: Y
      MSSQL_SA_PASSWORD: YOUR_PASS
      MSSQL_PID: Developer
      MSSQL_TCP_PORT: 1433
    networks:
      metabase_postgres_mssql_network:
        aliases:
          # alias refers to the DNS (host name) of the container. This is optional.
          # If not specified, the container name "mssql-for-metabase" will be used as DNS
          # source: https://stackoverflow.com/questions/49913355/domain-configuration-in-docker-compose
          # alternatively, you can use the IP address of the mssql container, which can be found by running
          # docker inspect mssql-for-metabase | grep IPAddress
          # details of this command can be found here:
          # https://www.tutorialworks.com/container-networking/
          # details of how to get DNS and IP address of containers: 
          # https://stackoverflow.com/questions/62872963/docker-network-show-dns-entries#:~:text=Run%20docker%20network%20ls%20to,key%20is%20the%20DNS%20name

          # use this alias on "host" field in metabase to connect to mssql
          - mssql_nsa # network-scoped alias

#
# general configurations based on what was mentioned in metabase and mssql services above
#

# # side note: uncomment the following lines if you want to avoid using bind mounts, and use named volumes instead 
# # consequently, you should also comment type/source/target lines above
# volumes:
#   # named volumes are added here to map to the containers
#   # source: https://stackoverflow.com/questions/74315648/service-volumes-must-be-mapping-in-docker
#   metabase_data:
#     name: metabase_data
#   mssql_data:
#     name: mssql_data_for_metabase

networks:
  metabase_postgres_mssql_network:
    driver: bridge
secrets:
   db_password:
     file: db_password.txt
   db_user:
     file: db_user.txt

```
 