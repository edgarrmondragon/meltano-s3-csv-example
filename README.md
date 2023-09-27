# Example Meltano project to extract data from files in S3

## Prerequisites

* [Docker][install-docker]
* [Meltano][install-meltano]

## Setup

1. Clone this repository
2. Run `meltano install` to install the project's dependencies
3. Run `docker compose up -d` to start the project's services (MinIO)
4. Run `meltano run tap-spreadsheets-anywhere target-duckdb` to run the pipeline

You should now be be able to query the data in the `output/warehouse.duckdb` file:

```console
$ duckdb output/warehouse.duckdb -c 'select id, email from tap_spreadsheets_anywhere.customers limit 5;'
┌────────┬───────────────────────────┐
│   id   │           email           │
│ int128 │          varchar          │
├────────┼───────────────────────────┤
│      1 │ ebook0@twitter.com        │
│      2 │ mtire1@vkontakte.ru       │
│      3 │ rdorian2@twitpic.com      │
│      4 │ ssuddock3@ycombinator.com │
│      5 │ sdaws4@usgs.gov           │
└────────┴───────────────────────────┘
```

[install-docker]: https://docs.docker.com/engine/install/
[install-meltano]: https://docs.meltano.com/getting-started/installation/