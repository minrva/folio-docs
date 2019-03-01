# Install FOLIO virtual machine

These instructions are optional. These instructions were used to get information from FOLIO's VM `snapshot` to setup a singler server installation. 

You can skip this document if:

1. You follow the official FOLIO [Single Server Installation](https://github.com/folio-org/folio-install/blob/master/single-server.md#install-and-configure-required-packages) guide.
2. You want to use the information collected below.

## Create Workspace

```bash
mkdir ~/Desktop/folio
mkdir ~/Desktop/folio/bl
mkdir ~/Desktop/folio/db
mkdir ~/Desktop/folio/docs
mkdir ~/Desktop/folio/ui
mkdir ~/Desktop/folio/vms
```

## Install a snapshot

```bash
mkdir ~/Desktop/folio/vms/snapshot
cd ~/Desktop/folio/vms/snapshot
vagrant init --minimal folio/snapshot
```

## Login to snapshot

```bash
cd ~/Desktop/folio/vms/snapshot
vagrant up
vagrant ssh
```

## Collect Stripes dependency versions

```bash
node -v
# v10.13.0

yarn --version
# yarn version v1.12.1
```

## Collect Stripes git information

```bash
cd /etc/folio/stripes

git remote show origin
# https://github.com/folio-org/platform-complete

git rev-parse HEAD
# 5a3b6896f2886ffd67d18cdca1ea65bbd559997c
```

## Collect Okapi version

```bash
apt list okapi
# okapi/FOLIO,now 2.18.0-1 all [installed]
```

## Migrate Database

```bash
sudo su
cd /vagrant
systemctl stop postgresql
tar -cf folio-db-fa18.tar /var/lib/postgresql/9.6/main
systemctl start postgresql
exit
logout
```

## Collect Docker images information

```bash
docker images
# stripes                           latest                c0fda44e57ef        39 hours ago        44.5MB
# folioci/mod-finance-storage       1.0.1-SNAPSHOT.4      1ff396617e84        3 days ago          516MB
# folioci/mod-inventory             10.1.0-SNAPSHOT.110   2ecfddab354e        3 days ago          458MB
# folioci/mod-authtoken             2.0.2-SNAPSHOT.34     19d576407b53        3 days ago          115MB
# folioci/mod-circulation-storage   6.1.2-SNAPSHOT.120    60b0da8830f2        4 days ago          516MB
# folioci/mod-circulation           12.1.0-SNAPSHOT.176   e63381c70dd9        4 days ago          474MB
# folioci/mod-password-validator    1.0.1-SNAPSHOT.11     9d180faa6d73        4 days ago          516MB
# folioci/mod-login                 4.5.1-SNAPSHOT.27     ec46699473f0        4 days ago          521MB
# folioci/mod-inventory-storage     13.1.0-SNAPSHOT.184   2036195badd7        4 days ago          520MB
# folioci/mod-orders                1.0.0-SNAPSHOT.23     e81b5b2f5187        7 days ago          516MB
# folioci/mod-feesfines             15.0.2-SNAPSHOT.17    b02c52aac825        8 days ago          520MB
# folioci/mod-users-bl              4.0.4-SNAPSHOT.36     02f7a55884f9        9 days ago          522MB
# folioci/mod-codex-inventory       1.4.0-SNAPSHOT.64     4bd4748dae68        10 days ago         522MB
# folioci/mod-tags                  0.2.0-SNAPSHOT.28     db0619044ed4        10 days ago         521MB
# folioci/mod-notify                1.2.0-SNAPSHOT.56     da3a8d5294fc        10 days ago         521MB
# folioci/mod-login-saml            1.2.2-SNAPSHOT.31     a624b68886ef        2 weeks ago         536MB
# folioci/mod-users                 15.3.0-SNAPSHOT.54    af01fdf44ee6        2 weeks ago         521MB
# folioci/mod-codex-mux             2.2.3-SNAPSHOT.60     b53e372a3b4e        2 weeks ago         522MB
# folioci/mod-codex-ekb             1.0.1-SNAPSHOT.73     c447858d6d80        3 weeks ago         521MB
# folioci/mod-permissions           5.4.0-SNAPSHOT.33     e1f4dcfaab7a        3 weeks ago         521MB
# folioci/mod-rtac                  1.2.0-SNAPSHOT.18     c63619985d8b        4 weeks ago         517MB
# folioci/mod-configuration         5.0.2-SNAPSHOT.49     2243b5e3b431        4 weeks ago         520MB
# folioci/mod-kb-ebsco              1.0.2-SNAPSHOT.155    45ed10db1d61        4 weeks ago         848MB
# folioci/mod-notes                 2.2.0-SNAPSHOT.64     669fed2e1c99        4 weeks ago         522MB
# folioci/mod-vendors               1.0.2-SNAPSHOT.26     63d1b52d2a0d        5 weeks ago         517MB
# folioci/mod-orders-storage        1.0.1-SNAPSHOT.14     47b6b19dce01        5 weeks ago         517MB
# nginx                             stable-alpine         14d4a58e0d2e        7 weeks ago         17.4MB
```

## Collect Okapi command line

```bash
xargs -0 < /proc/2199/cmdline
# /usr/bin/java
#    -Djava.awt.headless=true
#    -Dstorage=postgres
#    -Dpostgres_host=localhost
#    -Dpostgres_port=5432
#    -Dpostgres_user=okapi
#    -Dpostgres_password=okapi25
#    -Dpostgres_database=okapi
#    -Dhazelcast.logging.type=slf4j
#    -Dlog4j.configuration=file:///etc/folio/okapi/log4j.properties
#    -Dhost=10.0.2.15
#    -Dport=9130
#    -Dport_start=9131
#    -Dport_end=9661
#    -DdockerURL=http://localhost:4243
#    -Dokapiurl=http://10.0.2.15:9130
#    -jar /usr/share/folio/okapi/lib/okapi-core-fat.jar dev
```

## Copy Deployment Descriptors

```bash
sudo su
cd /etc/folio
cp -R deployment-descriptors /vagrant/deployment-descriptors
cp -R okapi /vagrant/okapi
cp install.json /vagrant/install.json
cp okapi-deploy.conf /vagrant/okapi-deploy.json
exit
```

## VM directory reference

### Okapi

```bash
/usr/share/folio/okapi
/etc/folio/okapi
/var/log/folio/okapi
```

### Modules and Stripes

```bash
/etc/folio
/usr/share/folio
```
