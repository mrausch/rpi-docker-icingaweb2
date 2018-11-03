# Icingaweb2 Container for Docker on a Raspberry Pi (raspbian)

Fork of [docker-icingaweb2](https://github.com/psi-4ward/docker-icingaweb2) that supports the raspberry pi as target platform.

* Icingaweb2 v2.5.3
  * Director v1.4.3
  * Cube v1.0.1
  * Businessprocess v2.1.0
  * Grafana v1.2.1
* Alpine based
* Automated Database and Director initialization and update
* Waits at least 60 seconds for database to come up
* Requires MySQL/MariaDB
* Docker-Healthcheck support

**Exposed Volume: `/etc/icingaweb2`**: Icingaweb2 Config Files  
**Exposed Port: `80`**: Icingaweb2 HTTP Port

### Supported tags

* Exact: i.e. `2.4.2-r1`: Icingaweb2 Version 2.4.2, image build 1
* `2.4`: Icingaweb2 Version 2.4.x, latest image build
* `2`: Icingaweb2 Version 2.x.x, latest image build

### Example

See [docker-compose.yml](): Icinga2 stack with UI and Graphing **(TODO)**  

**Initialization creates admin:admin user, don't forget to change the password!**

```bash
sudo docker run \
  --rm -t \
  --name icingaweb2 \
  --link mysql \
  --link icinga2 \
  -p 8080:80 \
  -e TIMEZONE=Europe/Berlin \
  -e ICINGA_API_PASS=damn-secret \
  -e WEB_DB_PASS=top-secret \
  -v $PWD/conf:/etc/icingaweb2 \
  psitrax/icingaweb2
```


### Configuration via ENV Vars:

* `TIMEZONE=UTC`: Timezone
* `ICINGAWEB_AUTOCONFIG=true`: Set to false to disable auto configuration
* `DIRECTOR_INSERT_DEFAULTS=true`: Insert some defaults for Icinga Director
* `ICINGA_API_PASS`: Password Icinga2 API user `icingaweb2` 

#### MySQL for Icingaweb
* `WEB_DB_HOST=mysql`: Database Host
* `WEB_DB_PORT=3306`: Database Port
* `WEB_DB_USER=root`: Database User
* `WEB_DB_PASS=root`: Database Password
* `WEB_DB=icingaweb`: Database Name
* `DIRECTOR_DB`: Database Name for Director

#### MySQL for Icinga IDO
* Uses Icingaweb connection if not specified
* `IDO_DB_HOST=mysql`: Database Host
* `IDO_DB_PORT=3306`: Database Port
* `IDO_DB_USER=root`: Database User
* `IDO_DB_PASS=root`: Database Password
* `IDO_DB=icinga2`: Database Name


## Maintainer
* Michael Rausch <it@emair.de>
* Forked from  Christoph Wiechert <wio@psitrax.de>
