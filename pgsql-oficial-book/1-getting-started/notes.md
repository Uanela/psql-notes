# 1 Chapter. Getting Started

## 1.1 Installation

- This is just my personal example with docker

```bash
docker run --name mypgsql \
-e POSTGRES_USER=admin \
-e POSTGRES_PASSWORD=Password123 \
-e POSTGRES_DB=maindb \
-p 5432:5432 \
-v pgdata:/var/lib/postgresql/data \
-d postgres:[version]
```

### Understanding above command

- `-e` -> stands from `--env` (environment)
- `-p` -> port (HOST:CONTAINER)
- `-d` -> means detached mode, to run it inside docker in background
- `\` -> this is just to mean it is a single line
- `[version]` -> is optional

- You may need to run `su postgres` to get into root mode maybe
- Get into the server process

```bash
docker exec -it mypgsql bash
psql -U admin -d maindb
```

### Understanding

It is `docker exec -it <CONTAINER> <COMMAND>`, means exec command into container, `-i` is interactive mode and `t` is for `TTY` to give you a terminal

## 1.2 Architectural Fundamentals

- You gotta understand some artchitures from pgsql.
- A pgsql session consists of 2 things:
    - a server process, that manages files, accepts connections and performs db actions. (postgres)
    - user client (frontend) that consumes the server process

## 1.3 Creating a Database

```bash
createdb mydb
drop mydb
```

## 1.4 Accessing Data

```sql
SELECT version();
SELECT current_date;
SELECT 2 + 2;
\h -- For help
\q -- To quit psql
```
