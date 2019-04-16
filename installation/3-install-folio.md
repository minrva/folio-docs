# Install FOLIO Platform

After the requirements are installed, you can download and install the FOLIO platform from source code and pre-packaged docker containers.

## Create Workspace

```bash
mkdir ~/Desktop/folio
mkdir ~/Desktop/folio/bl
mkdir ~/Desktop/folio/db
mkdir ~/Desktop/folio/docs
mkdir ~/Desktop/folio/ui
mkdir ~/Desktop/folio/vms
```

## Install Stripes Demo Platform

1. Download the platform.
    ```bash
    cd ~/Desktop/folio/ui
    git clone --recursive https://github.com/folio-org/platform-complete
    cd platform-complete
    git fetch
    git checkout 5a3b6896f2886ffd67d18cdca1ea65bbd559997c
    ```
1. Add folio repository.
    ```bash
    yarn config set @folio:registry https://repository.folio.org/repository/npm-folio/
    ```
1. *Optional*: [Yarn Troubleshooting Step](https://github.com/yarnpkg/yarn/issues/3507)
    ```bash
    yarn global add node-gyp
    ```
1. *Optional*: Install eslint.
    ```bash
    yarn global add eslint
    ```
1. *Recommended*: Install stripes-cli
    ```bash
    yarn global add @folio/stripes-cli
    ```
1. Install the platform.
    ```bash
    yarn install
    ```

## Install Okapi

```bash
cd ~/Desktop/folio/bl
git clone --recursive https://github.com/folio-org/okapi -b v2.18.0
cd okapi && mvn clean install
```

## Install Okapi Modules

1. Download the configuration files (i.e. `descriptors`).
    ```bash
    cd ~/Desktop/folio/bl
    git clone https://github.com/minrva/folio-config.git
    mv folio-config/ dev-ops
    ```
1. **Start Docker** and then download the pre-packaged Okapi module images.
    ```bash
    open -a Docker
    docker pull folioci/mod-finance-storage:1.0.1-SNAPSHOT.4
    docker pull folioci/mod-inventory:10.1.0-SNAPSHOT.110
    docker pull folioci/mod-authtoken:2.0.2-SNAPSHOT.34
    docker pull folioci/mod-circulation-storage:6.1.2-SNAPSHOT.120
    docker pull folioci/mod-circulation:12.1.0-SNAPSHOT.176
    docker pull folioci/mod-password-validator:1.0.1-SNAPSHOT.11
    docker pull folioci/mod-login:4.5.1-SNAPSHOT.27
    docker pull folioci/mod-inventory-storage:13.1.0-SNAPSHOT.184
    docker pull folioci/mod-orders:1.0.0-SNAPSHOT.23
    docker pull folioci/mod-feesfines:15.0.2-SNAPSHOT.17
    docker pull folioci/mod-users-bl:4.0.4-SNAPSHOT.36
    docker pull folioci/mod-codex-inventory:1.4.0-SNAPSHOT.64
    docker pull folioci/mod-tags:0.2.0-SNAPSHOT.28
    docker pull folioci/mod-notify:1.2.0-SNAPSHOT.56
    docker pull folioci/mod-login-saml:1.2.2-SNAPSHOT.31
    docker pull folioci/mod-users:15.3.0-SNAPSHOT.54
    docker pull folioci/mod-codex-mux:2.2.3-SNAPSHOT.60
    docker pull folioci/mod-codex-ekb:1.0.1-SNAPSHOT.73
    docker pull folioci/mod-permissions:5.4.0-SNAPSHOT.33
    docker pull folioci/mod-rtac:1.2.0-SNAPSHOT.18
    docker pull folioci/mod-configuration:5.0.2-SNAPSHOT.49
    docker pull folioci/mod-kb-ebsco:1.0.2-SNAPSHOT.155
    docker pull folioci/mod-notes:2.2.0-SNAPSHOT.64
    docker pull folioci/mod-vendors:1.0.2-SNAPSHOT.26
    docker pull folioci/mod-orders-storage:1.0.1-SNAPSHOT.14
    docker images
    ```

## Install Demo Database

1. Download [folio-db-fa18.tar](https://uofi.box.com/s/dncj1cx7xv47lmb67qpebrqbs5v1m4vm) into `~/Desktop`.
1. Replace the default database with the FOLIO demo platform database.
    ```bash
    cd ~/Desktop
    tar xopf folio-db-fa18.tar
    mv /usr/local/var/postgresql@9.6 ~/postgres.9.6.bak
    mv var/lib/postgresql/9.6/main /usr/local/var/postgresql@9.6
    rm folio-db-fa18.tar
    rm -rf var/
    rm -rf __MACOSX/
    ```
1. Copy configuration files to the newly migrated database.
    ```bash
    cp ~/postgres.9.6.bak/pg_ident.conf /usr/local/var/postgresql@9.6/
    cp ~/postgres.9.6.bak/postgresql.conf /usr/local/var/postgresql@9.6/
    cp ~/postgres.9.6.bak/pg_hba.conf /usr/local/var/postgresql@9.6/
    ```

## Disclaimer

The Okapi [descriptors](https://code.library.illinois.edu/scm/fol/dev-ops.git) and [demo data](https://uofi.box.com/s/dncj1cx7xv47lmb67qpebrqbs5v1m4vm) were extracted from [folio/snapshot](https://app.vagrantup.com/folio/boxes/snapshot). The descriptors and data would typically be generated during the build, deploy, and test process and/or created from the system administrator.
