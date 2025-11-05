# Modern Data Stack (proof of concept)

## Command

1. Data Warehouse and View layer. 

Run Postgres and Metabase. Note: Postgrs serves as both Metabase's config db and analytic db.
```
docker-compose up -d db metabase
```

2. Run EL

;; Not using Docker seems to make this job easier
```
pipx install meltano
cd ./meltano
meltano install
meltano el tap-smoke-test target-postgres
```

3. Run Transformation Layer

```
# run all models
dbt run

# run tests
dbt test

# run single model
dbt run --select my_new_model
```

## connect to the Warehouse

```
psql "postgresql://${USER}:${PASS}@127.0.0.1:5432/${DB}"
```
