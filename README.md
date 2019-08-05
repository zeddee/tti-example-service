# TTI experimental service

Using:

- mysql:8.0.17
- nginx:1.16-alpine

## Quirks

### Make sure `dbdata/` dir exists

Before running `docker-compose up`, make sure that a non-root `dbdata/` directory exists in service root.

We're mounting `/var/lib/mysql` as a local directory so that the data directory is as obvious as possible,
and therefore easy to mount.

Relying on Docker and Unix permissions to keep data dir secure.

### ENV var values unquoted

Putting the values of env variables in double quotes, while a good practice to ensure proper expansion of expressions,
causes MYSQL to read in the quotes as part of the literal values, and therefore misconfigures the `MYSQL_*` entries when
standing up a `docker-compose` cluster that uses that `.env` file.
