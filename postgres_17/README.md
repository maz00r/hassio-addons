## &#9888; Open Issue : [🐛 [Postgres 17] Error with Teslamate en HomeAssistant (opened 2025-07-09)](https://github.com/alexbelgium/hassio-addons/issues/1944) by [@cortesmario](https://github.com/cortesmario)
# Home assistant add-on: Postgres maz00r

[![Donate][donation-badge]](https://www.buymeacoffee.com/alexbelgium)
[![Donate][paypal-badge]](https://www.paypal.com/donate/?hosted_button_id=DZFULJZTP3UQA)

![Version](https://img.shields.io/badge/dynamic/json?label=Version&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fpostgres%2Fconfig.json)
![Ingress](https://img.shields.io/badge/dynamic/json?label=Ingress&query=%24.ingress&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fpostgres%2Fconfig.json)
![Arch](https://img.shields.io/badge/dynamic/json?color=success&label=Arch&query=%24.arch&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fpostgres%2Fconfig.json)

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/9c6cf10bdbba45ecb202d7f579b5be0e)](https://www.codacy.com/gh/alexbelgium/hassio-addons/dashboard?utm_source=github.com&utm_medium=referral&utm_content=alexbelgium/hassio-addons&utm_campaign=Badge_Grade)
[![GitHub Super-Linter](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/weekly-supelinter.yaml?label=Lint%20code%20base)](https://github.com/alexbelgium/hassio-addons/actions/workflows/weekly-supelinter.yaml)
[![Builder](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/onpush_builder.yaml?label=Builder)](https://github.com/alexbelgium/hassio-addons/actions/workflows/onpush_builder.yaml)

[donation-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20(no%20paypal)-%23d32f2f?logo=buy-me-a-coffee&style=flat&logoColor=white
[paypal-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20with%20Paypal-0070BA?logo=paypal&style=flat&logoColor=white

_Thanks to everyone having starred my repo! To star it click on the image below, then it will be on top right. Thanks!_

[![Stargazers repo roster for @alexbelgium/hassio-addons](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/.github/stars2.svg)](https://github.com/alexbelgium/hassio-addons/stargazers)

![downloads evolution](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/postgres/stats.png)

## About

PostgreSQL, often simply "Postgres", is an object-relational database management system (ORDBMS) with an emphasis on extensibility and standards-compliance. As a database server, its primary function is to store data, securely and supporting best practices, and retrieve it later, as requested by other software applications, be it those on the same computer or those running on another computer across a network (including the Internet). It can handle workloads ranging from small single-machine applications to large Internet-facing applications with many concurrent users. Recent versions also provide replication of the database itself for security and scalability.

This addon is based on the official image : https://hub.docker.com/_/postgres

## Configuration

Postgres port is by default 5432 and is exposed to the host network.

default user: `postgres`
password: `set by POSTGRES_PASSWORD`

You can configure this options:

```yaml
POSTGRES_PASSWORD
POSTGRES_USER
POSTGRES_DB
POSTGRES_INITDB_ARGS
POSTGRES_HOST_AUTH_METHOD
```

For more info check [base image docs](https://hub.docker.com/_/postgres).

By default `postgresql.conf` is stored in volume accessible by other addons and Home Assistant, so you can conviniently modify it by e.g. File Editor addon. If you prefer better security change `CONFIG_LOCATION` to e.g. `/data/orig/postgresql.conf`, so it will be acessible only to this addon, but you will have to modify it by the [Hassio SSH](https://developers.home-assistant.io/docs/operating-system/debugging/).

## Installation

The installation of this add-on is pretty straightforward and not different in comparison to installing any other add-on.

1. Add my add-ons repository to your home assistant instance (in supervisor addons store at top right, or click button below if you have configured my HA)
   [![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Falexbelgium%2Fhassio-addons)
1. Install this add-on.
1. Click the `Save` button to store your configuration.
1. Set the add-on options to your preferences, at least POSTGRES_PASSWORD is required.
1. Start the add-on.
1. Check the logs of the add-on to see if everything went well.
1. Use any Postgres client to connect, e.g. to `homeassistant.local:5432`

Migration from postgres 15 :

- stop the postgres 15 addon
- use the Filebrowser addon to copy the database folder from /addon_configs/xxx-postgres to /addon_configs/xxx-postgres_latest
- start the postgres 17 addon. Upgrade of the database should proceed. In case it doesn't, your data is anyway safe in the postgres 15 addon

## Security

By default, Postgres will be reachable on the local network of your host system. To improve security, you can disable this behavior and make Postgres available only to other Add-ons within Home Assistant.

1. Configure all Add-ons that use Postgres to connect via the internal DNS name: `db21ed7f-postgres-latest:5432`.
2. Go to **Settings → Add-ons → Postgres 17 → Configuration**, and under **Network**, remove port `5432` by clearing the text field.
3. Click **Save** and restart the Add-on.
4. Postgres is now only accessible from other Add-ons and no longer reachable from your local network (e.g., laptop, IoT devices, etc.).

## Support

Create an issue on github

[repository]: https://github.com/alexbelgium/hassio-addons
