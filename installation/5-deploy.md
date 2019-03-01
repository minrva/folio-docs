# Deploy

## Set-up

```bash
sudo ifconfig lo0 alias 10.0.2.15
brew services start postgresql@9.6
open -a Docker
# wait for Docker to start before running next cmd
docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p 127.0.0.1:4243:4243 bobrik/socat TCP-LISTEN:4243,fork UNIX-CONNECT:/var/run/docker.sock
```

## Deploy Okapi

```bash
cd ~/Desktop/folio
java \
      -Dstorage=postgres \
      -Dpostgres_host=localhost \
      -Dpostgres_port=5432 \
      -Dpostgres_user=okapi \
      -Dpostgres_password=okapi25 \
      -Dpostgres_database=okapi \
      -Dhost=10.0.2.15 \
      -Dport=9130 \
      -Dport_start=9131 \
      -Dport_end=9661 \
      -DdockerURL=http://localhost:4243 \
      -Dokapiurl=http://10.0.2.15:9130 \
      -jar bl/okapi/okapi-core/target/okapi-core-fat.jar dev
```

## Deploy Okapi Modules

Important! Only run the following code one time.

```bash
source activate folio
python ~/Desktop/folio/bl/dev-ops/deploy_modules.py
source deactivate folio
```

## Deploy Stripes Platform

```bash
cd ~/Desktop/folio/ui/platform-complete
yarn start
```

## Login to FOLIO Platform

- Visit <http://localhost:3000>
- Login with diku_admin/admin
- Checkout with `user: 313967897459701`, `item: 765475420716`
- Checkin with `item: 765475420716`

## Tear-down

1. `ctrl + c` out of okapi and stripes-demo-platform
1. `docker kill $(docker ps -q)`
1. `docker container prune`
1. `brew services stop postgresql@9.6`
1. `sudo ifconfig lo0 -alias 10.0.2.15`

## Status Checks

```bash
curl http://localhost:9130/_/proxy/tenants
curl http://localhost:9130/_/proxy/modules
curl http://localhost:9130/_/proxy/tenants/diku/modules
curl http://localhost:9130/_/discovery/modules
docker container ls
```
