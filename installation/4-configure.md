# Configure

The following configuraiton changes help fascilitate development environment portability.

## FOLIO IP Address

An external IP address is needed for the modules to communicate with the Okapi gateway and the Postgres database. One solution is to use the public IP address of the current workstation. Another solution is to create a temporary [loopback alias](https://aaron.blog/2011/02/04/mac-os-x-adding-a-loopback-alias/).

## Edit Postgresql Config

Postgresql needs to be configured in order to work with the loopback alias.

1. Add to or modify `postgresql.conf`.
    ```bash
    code /usr/local/var/postgresql@9.6/postgresql.conf
    listen_addresses = 'localhost, 10.0.2.15'
    ```
1. Add to `pg_hba.conf`,
    ```bash
    code /usr/local/var/postgresql@9.6/pg_hba.conf
    host    all             all             10.0.2.15/32            trust
    ```

## Test Loopback Alias

```bash
sudo ifconfig lo0 alias 10.0.2.15
brew services restart postgresql@9.6
psql -h 10.0.2.15 -U postgres
\q
brew services stop postgresql@9.6
sudo ifconfig lo0 -alias 10.0.2.15
```

## Docker RAM

To be on the safe side, give Docker a lot of RAM to work with, if possible 4-6GB. The extra RAM may help mitigate some current known issues: [FOLIO-968](https://issues.folio.org/browse/FOLIO-968), [FOLIO-868](https://issues.folio.org/browse/FOLIO-868), [MODPERMS-19](https://issues.folio.org/browse/MODPERMS-19).
