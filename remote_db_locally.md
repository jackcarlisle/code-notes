### Run locally but connect to remote DB:


##### Experimentally running local env whilst connecting to review app db

```bash
echo "export REVIEW_APP_DATABASE_URL=$(heroku config:get DATABASE_URL -a [app_name]-pr-xxxx)" >> .env
source .env
```

Now run server and should be connected to review app db.

____ 

### Copy remote DB locally:

If there is an error being triggered in a review app, we can look to clone the review app database and trigger the error locally - allowing for easier debugging.

```bash
REVIEW_APP=[app_name]
DEBUG_REVIEW_DB=[target_db_name]

# create the database
createdb $DEBUG_REVIEW_DB

# get db url
REVIEW_APP_DB_URL=$(heroku config:get DATABASE_URL -a $REVIEW_APP)

# Dump the review app database
pg_dump -xO $REVIEW_APP_DB_URL | tr -d '\r' | psql $DEBUG_REVIEW_DB 1> /dev/null

# update our `config/dev.exs` with our new db
sed -i '' -e "s/ev2_dev/$DEBUG_REVIEW_DB/" config/dev.exs

# update all user password hashes for this review app
MY_PASSWORD_HASH=$(psql -t -d [local_db_name_that_has_user_id_1] -c 'SELECT password_hash FROM users WHERE id = 1' | xargs)
psql -d $DEBUG_REVIEW_DB -c "UPDATE users SET password_hash = '$MY_PASSWORD_HASH'" 1> /dev/null

# We can now run our dev server with the review app data
mix phx.server
```

-----------


##### Debugging a Heroku Build
```sh
heroku config:get -a [app_name] -s > .env.PROD
heroku local:start web -e .env.PROD -p 4000
```

