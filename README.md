# TIG Stack

This TIG Stack is done for monitoring a host using Docker containers of Telegraf, InfluxDB and Grafana.


## Usage

1. Clone repo
 ```bash
 git clone https://github.com/igorrecioh/tig-docker-host.git
 cd tig-docker-host
 ```
2. Generate folder infraestructure
```bash
mkdir -p confs/{telegraf,telegraf/telegraf.d}
```

3. Generate configuration files
```bash
docker run --rm telegraf telegraf config > ./confs/telegraf/telegraf.conf
```

4. Set up Telegraf configuration as commented before

You can modify these settings as desired. Here you have an example of the simplest ones:

```log
[[outputs.influxdb]]
  urls = ["http://influxdb:8086"]
  database = "telegraf" 
  retention_policy = ""
  write_consistency = "any"
  timeout = "5s"
  username = "telegraf"
  password = "password"
```

5. Start the containers (-d option can be added for detached mode)
```bash
docker-compose up
```

6. Setup grafana

- First go to http://localhost:3000
- The default value for user and password is **admin/admin**
- Once you login, you can change it
- Finally, go to **Configuration** --> **Data Sources** to set up the connection with InfluxDB
- Done! Now start creating your own Dashboards!

## URLs

### Grafana URL
```
http://localhost:3000
```

### InfluxDB URL
```
http://influxdb:8086
```

### Based on (Kudos for them)
- `https://github.com/ichasco/tick`
- `https://github.com/nicolargo/docker-influxdb-grafana/`
- `https://tsql.tech/a-self-deployable-tick-stack-for-ingesting-data-monitoring-and-alerting-for-any-service-including-sql-server/` 
