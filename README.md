# Project
Grafana enables querying logs.  
Loki is a server to store logs.  
Promtail is an agent which sends logs to Loki.  

# Description
In this project, Promtail is configured to send all logs from all docker containers to Loki.
- loki-simple-var-log: A basic configuration to use /var/log/*log
- loki-docker-socket: A full configuration with docker sockets and /var/log/*log
- loki-icm-lustre: A configuration using files in ICM /network/lustre/ directories

# Usage
```bash
cd ~/Dev/loki-docker-compose/loki-simple-var-log
docker-compose up
# Go to http://localhost:3000/login with admin/admin and skip password change.
# Go to http://localhost:3000/plugins/loki and add a datasource : IP http://loki:3100 -> Save and test -> Explore.
# On top of Explore, select Loki -> Labels filename -> Top right blue arrow run query.

cd ~/Dev/loki-docker-compose/loki-docker-socket # https://grafana.com/docs/loki/latest/getting-started/
docker-compose up
# Go to http://localhost:3000/login with admin/admin and skip password change.
# Go to http://localhost:3000/explore and select Loki as datasource.
# Select Label -> container -> flog -> Live query.
# Filter queries : top right click code and enter this :
# {container="loki-docker-socket_flog_1"} |= "POST"
# {container="loki-docker-socket_flog_1"} | json | status="401"
# {container="loki-docker-socket_flog_1"} != "401"

cd ~/Dev/loki-docker-compose/loki-icm-lustre # https://gitlab.com/icm-institute/iconics/xnat/xnat-docker-compose-icm-fork/-/tree/develop
docker-compose up
# Ensure user is specified in the docker-compose file
#    user: "${DOCKER_UID}:${DOCKER_GID}"
# See xnat staging at http://xnat-staging.icm-institute.org:44970/
```

# Source
https://grafana.com/docs/loki/latest/getting-started/
