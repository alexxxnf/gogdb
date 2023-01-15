# GOG Database

Website that collects data on GOG games.

## Configuration

The project can be configured via environment variables.

| Parameter                   | Default value | Required | Description |
|-----------------------------|---------------|----------|-------------|
| `GOGDB_STORAGE_PATH`        |               | y        |             |
| `GOGDB_NUM_PRODUCT_TASKS`   | `1`           |          |             |
| `GOGDB_UPDATER_LOGLEVEL`    | `NOTSET`      |          |             |
| `GOGDB_DEBUG`               |               |          |             |
| `GOGDB_JINJA_LSTRIP_BLOCKS` | `False`       |          |             |
| `GOGDB_JINJA_TRIM_BLOCKS`   | `False`       |          |             |

## Database

This project uses [SQLite](https://www.sqlite.org/) as a relational database for search index.

## Scripts
* `gogdb-token`
* `gogdb-updater`
* `gogdb-cleanup`

## Local development

Target platform for this project is [Python 3.10](https://python.org/)
running on [Ubuntu](https://ubuntu.com/).
It may work with higher or lower versions of Python and Ubuntu but compatibility is not guaranteed.

### Dependencies

The project uses [Poetry](https://python-poetry.org/) as a package manager. Consider installing it globally.

It is recommended to use a virtual environment.

To install python dependencies run `poetry install` in the root directory.

If you prefer to use `requirements.txt`, run `poetry export -o /requirements.txt`.
It will convert poetry-style list of requirements to pip's one.

### Development server

Adjust [configuration](#configuration).

Run `hypercorn gogdb.application:app` for a dev server.

## Production deployment

TBD

# License

AGPLv3 or later
