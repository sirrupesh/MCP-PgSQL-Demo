# DVD Rental Database Setup Guide

This guide explains how to set up a PostgreSQL database with the DVD rental sample database using Docker.

## Prerequisites
- Docker and Docker Compose installed
- Basic understanding of PostgreSQL
- Terminal/Command Line access

## Setup Steps

### 1. Start the PostgreSQL Container
# Start the PostgreSQL container in detached mode
docker compose up -d

### 2. Download and Extract Sample Database
# Download the DVD rental sample database
curl -o ./dvdrental.zip https://neon.tech/postgresqltutorial/dvdrental.zip

# Extract the downloaded zip file
unzip ./dvdrental.zip -d ./

### 3. Restore the Database
# Note: Choose one of the following methods to restore the database

#### Method 1: Direct PostgreSQL Connection (Commented out examples)
# Connect to database directly
#psql -h localhost -U postgres -W mydatabase

# Restore database directly
#pg_restore -h localhost -U postgres -W -d mydatabase ./dvdrental.tar

#### Method 2: Using Docker Container (Commented out example)
# Connect to database through Docker
#docker run -it --rm --network my-nw postgres:latest psql -h demo_postgres_container -U postgres -W mydatabase

#### Method 3: Restore Using Docker (Recommended)
# Restore the database using Docker with volume mounting
docker run -it --rm -v .:/opt --network my-nw postgres:latest pg_restore -h demo_postgres_container -U postgres -W -d mydatabase /opt/dvdrental.tar

### 4. Cleanup
# Remove downloaded and extracted files
rm dvdrental.*

## Note
- The database will be restored to the PostgreSQL instance running in Docker
- Default username is 'postgres'
- You will be prompted for the password when running the restore command
