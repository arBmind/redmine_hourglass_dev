# Redmine Hourglass Development setup

A development setup based on Docker

## Initial setup

For the first run docker-compose itself is not enough.
Rails won't start correctly until some steps are taken care of.

```
docker-compose run --rm app bash
````

Run:
```
rake db:migrate
rake redmine:plugins:migrate
rake redmine:plugins
exit
```

Notes:
* Starting rails would not expose the port
* Start regularly and proceed with the web setup

## Run Redmine with hourglass

```
docker-compose up
```

## Debugging Rails process

Rubymine works great for that.
You can also use VsCode but I have not tried it.

## Database Backups

Create:
```ps
docker run --rm --volume redmine_db:/dbdata --volume $(pwd):/backup ubuntu tar cvf /backup/redmine_db.tgz /dbdata
```

Restore:
```ps
docker run --rm --volume redmine_db:/dbdata --volume $(pwd):/backup ubuntu tar xvf /backup/redmine_db.tgz -C /dbdata --strip 1
```
