
# Connecting to a DB on Heroku via JDBC

Assumptions:
* DB IDE: [DBeaver](https://dbeaver.io/)
* Cloud platform: [Heroku](https://www.heroku.com/)
* Database: [PostgreSQL](https://www.postgresql.org/)
* You have access to an app on Heroku (which has the DB).

First, install Heroku CLI to your machine by following this guide: [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#install-with-an-installer:~:text=Download%20the%20appropriate%20installer).

Then, login to Heroku by running the following:

```bash
heroku login
```

Then, get the name of the app (where the DB is hosted) by running the following:

```bash
heroku apps
```

If you see `You have no apps.` as the output, then you probably aren't the person who created the app (i.e., the app's owner gave you access). In that case, run this command:

```bash
heroku apps --all
```

Which should give you an output like this:

```bash
=== Collaborated Apps

 <app-name> <app-related-string>@herokumanager.com
```

So now you can run the following command to get the database URL:

```bash
heroku pg:credentials:url --app <app-name>
```

Which will give you an output like this:

```bash
Connection information for default credential.
Connection info string:
  "dbname=<DB_NAME> host=<HOST> port=<PORT> user=<USERNAME> password=<PASS> sslmode=<require, etc>"
Connection URL:
  postgres://<USERNAME>:<PASS>@ec2<dash-separated-integers>.compute-1.amazonaws.com:<PORT>/<DB_NAME>
```

Now, open DBeaver and follow these steps:

1. Click on the `Database` menu.
2. Click on `New Database Connection`.
3. Select `PostgreSQL` as the database type.
4. In the `Connect by` field, click `URL`.
5. Then, write `jdbc:` followed by the `Connection URL` you got from the Heroku CLI.
6. Then, in `Authentication`, select `Database Native`.
7. Then, write the `Username` and `Password` you got from the Heroku CLI.
8. Click `Test Connection`.
	1. If everything is correct, you should see `Connection is successful`.
9. Click `OK`.


# Associating SQL Scripts with ...


## Connections

Assumptions:
* DB IDE: [DBeaver](https://dbeaver.io/)
* Connection name: `localhost`
* SQL file name: `convert_to_biginteger.sql`

Then:

![](Attachments%20-%20DB%20IDEs/Pasted%20image%2020250304095757.png)

## Schema

Source: [Perplexity chat](https://www.perplexity.ai/search/suppose-i-have-dbeaver-opened-HHETtzSXQGWZZl20aFh6Hg).

Assumptions:
* DB IDE: [DBeaver](https://dbeaver.io/)
* Schema name: `multi_sql_files`
* SQL file name: `convert_to_biginteger.sql`

Then:

![](Attachments%20-%20DB%20IDEs/Pasted%20image%2020250304100149.png)

Note 1: the step at `<- *` does ***NOT*** solve the issue, so you don't have to do it.

Note 2: Check [this](https://stackoverflow.com/a/76829577/13626137) to quickly understand the usage of `search_path` and [this](https://www.youtube.com/watch?v=4VlRmw4V1hg) for a video explanation.


