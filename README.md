# Docker Course on KodeKloud

```bash
docker run -d --name=redis redis
docker run -d --name=db postgres:9.4
docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
docker run -d --name=result -p 5001:80 --link db:db result-app
docker run -d --name=worker --link db:db --link redis:redis worker
```

```bash
docker-compose up
```

### Example voting app 

```bash
nano ~/.docker/config.json
```
- change credsStore to credStore

```bash
docker build . -t voting-app
docker run -p 5000:80 voting-app
docker run -d --name=redis redis
docker run -p 5000:80 --link redis:redis voting-app
docker run --name=db postgres:9.4
docker logs 35ba45d2b09e
```

```bash
Error: Database is uninitialized and superuser password is not specified.
       You must specify POSTGRES_PASSWORD for the superuser. Use
       "-e POSTGRES_PASSWORD=password" to set it in "docker run".

       You may also use POSTGRES_HOST_AUTH_METHOD=trust to allow all connections
       without a password. This is *not* recommended. See PostgreSQL
       documentation about "trust":
       https://www.postgresql.org/docs/current/auth-trust.html

```

```bash
docker run -d --name=db -e POSTGRES_PASSWORD=my_password postgres:9.4
docker ps
```

```bash
cd worker
docker build . -t worker-app
```