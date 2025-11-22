commands to start postgresql in arch

Install PostgreSQL
sudo pacman -Syu
sudo pacman -S postgresql

Initialize the Database Cluster
sudo -u postgres initdb -D /var/lib/postgres/data

Start and Enable the PostgreSQL Service
sudo systemctl start postgresql
sudo systemctl enable postgresql

Access the PostgreSQL Shell
sudo -u postgres psql

Command to create new database and setup database

CREATE DATABASE greenlight;

Command to create user to use api
CREATE ROLE greenlight WITH LOGIN PASSWORD 'postgreadmin4090';

Command to add "citext" extensions for case-insensitive character string type

CREATE EXTENSION IF NOT EXISTS citext;

DNS to connect 
postgres://greenlight:password@localhost/greenlight

//nano ~/.bashrc
export GREENLIGHT_DB_DSN

golang migration tool version 4.14.1 install if not installed

MacOs
brew install golang-migrate

Windows/Linux
curl -L https://github.com/golang-migrate/migrate/releases/download/v4.14.1/migrate.linux-amd64.tar.gz | tar xvz
mv migrate.linux-amd64 $GOPATH/bin/migrate

command to check version
migrate -version

migrate -path=./migrations -database=$GREENLIGHT_DB_DSN up
migrate -path ./migrations -database $GREENLIGHT_DB_DSN up
migrate -path=./migrations -database=$GREENLIGHT_DB_DSN up
migrate -path=./migrations -database=$GREENLIGHT_DB_DSN up

if not working this command run commands below

psql -U postgres -d greenlight -W

-- Grant schema permissions
GRANT ALL ON SCHEMA public TO greenlight;

-- Grant permissions on existing tables and sequences
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO greenlight;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO greenlight;

-- Grant default privileges for future tables and sequences
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL ON TABLES TO greenlight;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL ON SEQUENCES TO greenlight;

-- Make greenlight the owner of the public schema (optional but recommended)
ALTER SCHEMA public OWNER TO greenlight;