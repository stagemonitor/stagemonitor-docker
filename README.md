# This project is deprecated
Use docker-compose as described in https://github.com/stagemonitor/stagemonitor/wiki/Step-2%3A-Request-Analysis-Dashboard#set-up-with-docker-compose

## Graphite + Carbon + Grafana + Elasticsearch + Kibana

An all-in-one image running graphite and carbon-cache and grafana.

This image contains a sensible default configuration of graphite and
carbon-cache.

### Getting started with DockerHub
 * Pull the container `docker pull stagemonitor/stagemonitor-docker`
 * Download and execute the [start](https://github.com/stagemonitor/stagemonitor-docker/blob/master/start) script: `curl -s https://raw.githubusercontent.com/stagemonitor/stagemonitor-docker/master/start | sh`
 * Open the Dashboards. 
   * http://[docker-ip]:8888/kibana/`*`
   * http://[docker-ip]:8888/grafana/`*`

### Start with custom build
 * Clone this repo: `git clone https://github.com/stagemonitor/stagemonitor-docker`
 * Optional: edit the settings
 * Build the docker container: execute `./build`
 * Optional: modify `start` to map to the ports and host directories you need
 * Start the container: execute `./start`
 * Open the Dashboards. 
   * http://[docker-ip]:8888/kibana/`*`
   * http://[docker-ip]:8888/grafana/`*`

`*` Replace [docker-ip] with `localhost` if you are using native docker or `192.168.59.103`, if you are using boot2docker. If the ip is not working, check `boot2docker ip` for the actual ip. The trailing slash is important.

### Ports
Starting this container with the `start` script will, by default, bind the the following
ports:

| Host/VM | Container | Description                                                     |
| ------- | --------- | --------------------------------------------------------------- |
| `8888`  | `80`      | the grafana (`/grafana/`) and kibnana (`/kibana/`) web interface  |
| `8181`  | `2003`    | the graphite web interface (`/`)                                |
| `2003`  | `2003`    | the carbon-cache line receiver (the standard graphite protocol) |
|         | `2004`    | the carbon-cache pickle receiver                                |
|         | `7002`    | the carbon-cache query port (used by the web interface)         |

You can log into the administrative interface of graphite-web (a Django application) with the username admin and password admin. These passwords can be changed through the web interface.

NB: Please be aware that by default docker will make the exposed ports accessible from anywhere if the host firewall is unconfigured.

### Mounted Volumes
The `start` script will, by default, mount the following directories:

| Host/VM                             | Container                     | Description                                |
| ----------------------------------- | ----------------------------- | ------------------------------------------ |
| /var/docker/stagemonitor/elastic    | /var/lib/elasticsearch        | elasticsearch index files                  |
| /var/docker/stagemonitor/graphite   | /opt/graphite/storage/whisper | whisper (timeseries) database files        |
| /var/docker/stagemonitor/supervisor | /var/log/supervisor           | logs for elasticsearch, graphite and nginx |

### Technical details
By default, this instance of carbon-cache uses the following retention periods
resulting in whisper files of approximately 290Kb.

    1m:7d,10m:31d,1h:120d,6h:5y

### Notice
Modified from https://github.com/grafana/grafana-docker-dev-env
