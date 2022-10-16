## Setup

1. Create metastore schema

    ```bash
    docker compose run --entrypoint bash hive-metastore /opt/apache-hive-metastore/bin/schematool -initSchema -dbType derby
    ```

2. Change permission

    ```
    sudo chown -R 10000.root jupyter_workspace
    ```


## start

```bash
docker compose up -d
```

## Access

* Notebook

```
http://localhost:8888
```

* trino

```
docker compose exec -it trino trino
```

* minio

```
http://localhost:9001
```
