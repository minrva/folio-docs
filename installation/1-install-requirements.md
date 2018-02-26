# Install Requirements

Install the following software for developing on the macOS system.

## Tools

- [git](https://git-scm.com/downloads)
- [sourcetree](https://www.sourcetreeapp.com/)
- [vscode](https://code.visualstudio.com/docs/setup/mac)
- [brew](https://brew.sh/)
- [pgAdmin 4](https://www.pgadmin.org/download/pgadmin-4-macos/)

## Java

- [java 8 jre/jdk](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

## Dependencies Available in Brew

- [maven 3.3.9 or higher](https://maven.apache.org/install.html)
- [node 6.x or higher](https://nodejs.org/en/download/)
- [yarn v0.20.3 or higher](https://yarnpkg.com/en/)

```bash
brew install maven
brew install node
brew install yarn
```

Note: Make sure that you completely remove old [npm installs](https://stackoverflow.com/questions/11177954/how-do-i-completely-uninstall-node-js-and-reinstall-from-beginning-mac-os-x) and [yarn installs](https://stackoverflow.com/questions/42334978/how-do-i-uninstall-yarn).

## Postgres in Brew

- [postgres 9.6](https://www.postgresql.org/)

```bash
rm -rf rm -rf /usr/local/var/postgres
rm -rf .psql_history .psqlrc .psql.local .pgpass .psqlrc.local
brew install postgresql@9.6
echo 'export PATH="/usr/local/opt/postgresql@9.6/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
brew services start postgresql@9.6
psql postgres
\q
brew services stop postgresql@9.6
```

## Docker

- [Docker for Mac CE](https://www.docker.com/community-edition)

## Python

To help with the deploy process, Python can be useful.

1. Install Conda to manage Python environments.
    ```bash
    cd ~/Desktop
    curl "https://repo.continuum.io/miniconda/Miniconda2-latest-MacOSX-x86_64.sh" -o "Miniconda2-latest-MacOSX-x86_64.sh"
    bash Miniconda2-latest-MacOSX-x86_64.sh
    source ~/.bash_profile
    ```
1. Restart the terminal and then remove the shell file.
    ```bash
    rm ~/Desktop/Miniconda2-latest-MacOSX-x86_64.sh
    ```
1. Create and activate a Python environment.
    ```bash
    conda create --name folio python=3.6
    source activate folio
    python --version
    source deactivate folio
    python --version
    ```
1. Install `requests` library from source.
    ```bash
    cd ~/Desktop
    git clone git://github.com/requests/requests.git
    cd requests
    source activate folio
    pip install .
    cd ..
    rm -rf requests
    source deactivate folio
    ```
1. Install data manipulation libraries.
    ```bash
    source activate folio
    pip install dataset
    pip install autopep8
    conda install psycopg2
    source deactivate folio
    ```

## Optional Firefox Quantum

Firefox Quantum is a great browser.

- [firefox](https://www.mozilla.org/en-US/firefox/)

## Optional Virtual Machine

The pre-bundled demo system can be quickly run and explored using vagrant and virtualbox:

- [virtualbox](https://www.virtualbox.org/wiki/Downloads)
- [vagrant 1.9.2 or higher](https://www.vagrantup.com/)
- [ansible 2.2 or higher](http://docs.ansible.com/ansible/latest/intro_installation.html)

## Optional Chrome Plugins

Web development tools are available in Chrome:

- [react developer tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [redux developer tools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)

## Optional Windows Specific

Okapi seems to have some Windows specific incompatibilities, but some development was possible using these tools:

- [cygwin](http://www.cygwin.com/)
- [vscode + cygwin](https://github.com/Microsoft/vscode/issues/14977)
