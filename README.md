## Setting up on dev-cookbook

*This section loosely follows the [heroku guide](https://github.com/discourse/discourse/blob/master/docs/install-HEROKU.md)*

### Download and Configure

Clone the project within your dev environment under `~/workspace/`:

    git clone git@github.com:nitrous-io/nitrous-discuss.git

Copy over the sample `.env` file and make any necessary changes:

    cp .env.sample .env
    export $(cat .env)

>Additional configurations can be found at `config/site_settings.yml`.

### Superuser Access

Next, disable password prompts for postgres user 'postgres'. This is the only superuser within the PostgreSQL database. Edit the following file with sudo:

    action@dev-box:~/workspace/nitrous-discuss$ sudo vim /etc/postgresql/9.2/main/pg_hba.conf

Make line 12 in the code below match your `pg_hba.conf` file. The method 'trust' will prevent a password prompt.

    7 # documentation for a complete description of this file.
    8
    9 # TYPE  DATABASE        USER            ADDRESS                 METHOD
    10
    11 # "local" is for Unix domain socket connections only
    12 local   all             postgres                                trust

Now it's time to give user action superuser access:

    action@dev-box:~/workspace/nitrous-discuss$ psql -U postgres
    psql (9.2.8)
    Type "help" for help.

    postgres=# alter user action with superuser;

### Running Locally with Foreman

### Foreman commands:


##### Create the database

    bundle exec foreman run rake db:create

##### Migrate and seed the database

    bundle exec foreman run rake db:migrate db:seed_fu

##### Start the application using Foreman

    bundle exec foreman run rails server

##### Use Rails console, with pry

    bundle exec foreman run rails console

##### Prepare the test database

    bundle exec foreman run rake db:test:prepare

##### Run tests

    bundle exec foreman run rake autospec

