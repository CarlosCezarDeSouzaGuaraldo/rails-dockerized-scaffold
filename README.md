# Rails Dockerized Scaffold

This repository provides a Dockerized scaffold to help you construct a Ruby on Rails application with a PostgreSQL database from scratch.

## Requirements

Make sure you have the following dependencies installed on your system:

- Docker
- Docker Compose

## Getting Started

To use this scaffold, follow the steps below:

1. Clone this repository to your local machine:

```bash
git clone https://github.com/CarlosCezarDeSouzaGuaraldo/rails-dockerized-scaffold.git
cd rails-dockerized-scaffold
```

2. Copy the following files from this repository to your application's repository:

- Dockerfile
- entrypoint.sh
- Gemfile
- Gemfile.lock
- docker-compose.yml

3. Once the files are copied, execute the following command in the current directory:

```bash
docker compose run --no-deps web rails new . --force --database=postgresql
```

4. After the Rails application is generated, and if you are using Linux, execute the following command to ensure that the files and directories are owned by the current user:

```bash
sudo chown -R $USER:$USER .
```

5. Next, build the Docker images for your application:

```bash
docker compose build
```

6. Now, you need to change the contents of the config/database.yml file to the following:

```yaml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test
```

7. It's time to bring up your Rails application and PostgreSQL database:

```bash
docker compose up
```

8. Finally, in a new terminal, run the following command to create the development database:

```bash
docker compose run web rake db:create
```

9. Go to `http://localhost:3000` on a web browser to see the Rails Welcome.

![rails-welcome-page](https://github.com/CarlosCezarDeSouzaGuaraldo/rails-dockerized-scaffold/assets/66181262/752776f4-6a62-4ca6-8a2c-a93d2f0535a4)

Your Ruby on Rails application with a PostgreSQL database is now up and running within Docker containers. Happy coding!