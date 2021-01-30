## Ownership issues

If any issue about ownership raise on Linux, run this command

```bash
sudo chown -R "$USER":"$USER" .
```

## Connecting the Database

You have to tell Rails where to find the database.
In your `config/database.yml` put this :

```bash
# config/database.yml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: <%= ENV['POSTGRES_USER'] %>
  password: <%= ENV['POSTGRES_PASSWORD'] %>
  pool: 5
development:
  <<: *default
  database: myapp_development
test:
  <<: *default
  database: myapp_test
```

## Booting the app
First run :

```bash
docker-compose up --build
```

And in another terminal :

```bash
docker-compose run -rm web rails db:create
docker-compose run -rm web rails db:migrate
```

## Browsing the app
Now you should be able to browse your app on `localhost:3000`

## Stopping the app
To stop the application, just hit CTLR+C in the terminal, or run this commande in another one :
```bash
docker-compose down
```

## Starting the app
If you don't need a rebuild, simply run :
```bash
docker-compose up
```

If you changed the `Gemfile` :
```bash
docker-compose run web bundle install
docker-compose up --build
```

If you didn't change the `Gemfile` but changed the `docker-compose.yml` :
```bash
docker-compose up --build
```