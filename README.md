## Graphite + Carbon + Grafana + Elasticsearch + Kibana

An all-in-one image running graphite and carbon-cache and grafana.

This image contains a sensible default configuration of graphite and
carbon-cache. Starting this container will, by default, bind the the following
host ports:

- `80`: the grafana (`/grafana`) and kibnana (`/kibana`) web interface
- `81`: the graphite web interface (`/`)
- `2003`: the carbon-cache line receiver (the standard graphite protocol)
- `2004`: the carbon-cache pickle receiver
- `7002`: the carbon-cache query port (used by the web interface)

You can log into the administrative interface of graphite-web (a Django application) with the username admin and password admin. These passwords can be changed through the web interface.

NB: Please be aware that by default docker will make the exposed ports accessible from anywhere if the host firewall is unconfigured.

### Getting started
 * Clone this repo: `git clone https://github.com/stagemonitor/stagemonitor-docker`
 * Optional: edit the settings
 * Build the docker container: execute `./build`
 * Optional: modify `start` to map to the ports and host directories you need
 * Start the container: execute `./start`

### Technical details
By default, this instance of carbon-cache uses the following retention periods
resulting in whisper files of approximately 290Kb.

    1m:7d,10m:31d,1h:120d,6h:5y

### Notice
Modified from https://github.com/grafana/grafana-docker-dev-env
