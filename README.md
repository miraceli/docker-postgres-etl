# Usage

This README provides instructions for setting up and running the ETL (Extract, Transform, Load) process using Docker and PostgreSQL. Follow the steps below to initialize the databases and execute the ETL process.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/): Ensure Docker is installed on your system to control the ETL process environment.
- [Docker Compose](https://docs.docker.com/compose/): Required for managing multi-container Docker applications.

## Running PostgreSQL in Docker

1. **Pull PostgreSQL Image**: Pull the PostgreSQL Docker image from the Docker Hub.
    ```bash
    docker pull postgres
    ```

2. **Create a Directory for Data**: Create a directory to store PostgreSQL data.
    ```bash
    mkdir data-engineering-db
    cd data-engineering-db/
    ```

3. **Run PostgreSQL Container**: Run a PostgreSQL container named `data-engineering-postgres`.
    ```bash
    docker run --name data-engineering-postgres -e POSTGRES_PASSWORD=secret -d postgres
    ```

4. **Create a Database**: Create a database named `postgres-db`.
    ```bash
    docker exec -u postgres data-engineering-postgres createdb postgres-db
    ```

5. **Access PostgreSQL Shell**: Access the PostgreSQL shell to interact with the database.
    ```bash
    docker exec -it data-engineering-postgres psql -U postgres -d postgres-db
    ```

6. You are now connected to the PostgreSQL database and can execute SQL commands as needed. Press `Ctrl + D` to exit the PostgreSQL shell.

7. **Post-Installation Instructions**:
    After running `docker-compose up`, wait for the services to initialize. Then, execute the following commands to access the destination database and list tables:
    
    ```bash
    docker exec -it ws-data-engineer_destination_postgres_1 psql -U postgres
    ```

    You will be connected to the PostgreSQL shell. Once connected, switch to the `destination_db` database:

    ```sql
    \c destination_db
    ```

    You are now connected to the `destination_db` database as user `postgres`. You can list the tables using the following command:

    ```sql
    \dt
    ```

    This command will display a list of tables in the `destination_db` database.