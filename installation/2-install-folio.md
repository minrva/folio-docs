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
    git clone --recursive https://github.com/folio-org/stripes-demo-platform
    cd stripes-demo-platform
    git checkout 178976520471a17fa8816db884c6859f2ed3c67b .
    ```
1. *Optional*: [Yarn Troubleshooting Step](https://github.com/yarnpkg/yarn/issues/3507)
    ```bash
    yarn global add node-gyp
    ```
1. *Optional*: Install eslint.
    ```bash
    yarn global add eslint
    ```
1. Replace `config` in `stripes.config.js`.
    ```bash
    code stripes.config.js
    config: {
        hasAllPerms: true,
        reduxLog: true
    }
    ```
1. Fix `yarn.lock` file.
    ```bash
    code yarn.lock
    # replace 6e336e55b41f628e98c63e3c83d65a3b6cc2d7d9
    # with 639b3104e6954d30cd64d2ce6790dd9394b2c0cb
    ```
1. Install the platform.
    ```bash
    yarn config set @folio:registry https://repository.folio.org/repository/npm-folio/
    yarn install
    ```

## Install Okapi

```bash
cd ~/Desktop/folio/bl
git clone --recursive https://github.com/folio-org/okapi -b v1.10.0
cd okapi && mvn clean install
```

## Install Okapi Modules

1. Download the configuration files (i.e. `descriptors`).
    ```bash
    cd ~/Desktop/folio/bl
    git clone https://code.library.illinois.edu/scm/fol/dev-ops.git
    ```
1. **Start Docker** and then download the pre-packaged Okapi module images.
    ```bash
    docker pull folioorg/mod-authtoken:v0.6.1
    docker pull folioorg/mod-circulation-storage:v3.2.0
    docker pull folioorg/mod-circulation:v4.4.0
    docker pull folioorg/mod-configuration:v2.0.0
    docker pull folioorg/mod-inventory-storage:v5.1.0
    docker pull folioorg/mod-inventory:v5.1.1
    docker pull folioorg/mod-login:v3.1.0
    docker pull folioorg/mod-notes:v0.2.0
    docker pull folioorg/mod-notify:v0.1.1
    docker pull folioorg/mod-permissions:v4.0.4
    docker pull folioorg/mod-users-bl:v2.0.2
    docker pull folioorg/mod-users:v14.2.0
    docker images
    ```

## Install Demo Database

1. Download [folio-db.zip](https://uofi.app.box.com/s/atlz23qsmrl5hxnf2hjxgrtl9dq04k1p) into `~/Desktop`.
1. Replace the default database with the FOLIO demo platform database.
    ```bash
    cd ~/Desktop
    unzip folio-db.zip
    mv /usr/local/var/postgresql@9.6 ~/postgres.9.6.bak
    mv var/lib/postgresql/9.6/main /usr/local/var/postgresql@9.6
    rm folio-db.zip
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

The Okapi [descriptors](https://code.library.illinois.edu/scm/fol/dev-ops.git) and [demo data](https://uofi.box.com/s/atlz23qsmrl5hxnf2hjxgrtl9dq04k1p) were extracted from [folio/stable](https://app.vagrantup.com/folio/boxes/stable). The descriptors and data would typically be generated during the build, deploy, and test process and/or created from the system administrator.
