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
postgres://greenlight:postgreadmin4090@localhost/greenlight

//nano ~/.bashrc
export GREENLIGHT_DB_DSN