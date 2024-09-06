# Install Postgres server

Below commands install, posibly old version (14.x) of postgres. If you need newest version, follow the next instructions.
```sh
sudo apt-get update
sudo apt install postgresql postgresql-contrib
psql --version 
```

### Install latest Postgres Version
To install latest postgres version, add PostgreSQL repository and repository signing key and then update the system.

```sh
# Postgres repository
sudo sh -c 'echo "deb https://apt.PostgreSQL.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Postgres repository signing key
wget --quiet -O - https://www.PostgreSQL.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update
sudo apt update
```

Now, Install latest version of Postgres
```sh
sudo apt install postgresql-16 -y

# Check version
psql --version
```

The installation of PostgreSQL creates a user account called `postgres`, which is a `standard UNIX account`.

#### Other Usefull commands
```sh
sudo systemctl start postgresql
sudo systemctl stop postgresql
sudo systemctl restart postgresql
sudo systemctl reload postgresql
sudo systemctl status  postgresql
```

#### Login to Postgres

```sh
sudo -i -u postgres psql
```

#### Set Passowrd
Postgresql is installed without any password to the account `postgres`. Now set the password to the account. There are two way to do this.

##### Method: 1

Login to the postgres
```sh
sudo -u postgres psql
```

After login to the psql console,
type `\password` and follow the instructions to set the password.
type `\q` and `exit` to quit the postgres console.

##### Method: 2
In this mothod, Password is created using postgres `Alter` command.
```sh
# Login to the postgres console
sudo -u postgres psql

# change password
ALTER USER postgres PASSWORD '<new-password>';
```







