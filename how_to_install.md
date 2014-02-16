source: http://suite.opengeo.org/opengeo-docs/installation/ubuntu/install.html

__1. Change to the root user:__

    sudo su -
    
Import the OpenGeo GPG key:

    wget -qO- http://apt.opengeo.org/gpg.key | apt-key add -

    Add the OpenGeo repository. If installing for Precise:

    echo "deb http://apt.opengeo.org/suite/v4/ubuntu/ precise main" > /etc/apt/sources.list.d/opengeo.list

    apt-get update

    apt-get install opengeo

    apt-get update

    exit

__2. After successful installation. The opengeo installation does not create a postgis_template database..here's how.__

source: http://gis.stackexchange.com/questions/80563/how-to-install-postgis-correctly-with-opengeo-suite-4-0-community-edition-on-ubu

    sudo su postgres -c psql

    CREATE ROLE [new user name] PASSWORD ['new password'] SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;

    \q

__3. Open pg_hba.conf in text editor__

    leafpad /etc/postgresql/9.3/main/pg_hba.conf

Change:
local all all peer

to:
local all all md5

or:
local all all trust

Save file changes

    sudo service postgresql restart

    createdb -U [new username] -W -E UTF8 [new postgis template name]

    psql -U [new username] -W -d [new postgis template name]

    create extension postgis;
    
__To change the User postgres' password

    psql -U [new username] -d postgis_template -W
    
    ALTER ROLE postgres WITH PASSWORD ['new password'];
    
