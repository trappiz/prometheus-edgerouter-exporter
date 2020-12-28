# prometheus-edgerouter-exporter
This project contains files to export metrics from an ubiquiti edgerouter using docker with prometheus already running on it.

## Start
To get the exporter up and running there are a few manual steps you'll need to perform:
- Make sure SNMP is enabled on your Edgerouter and the community string is set.
- Modify `.edgerouter.auth.community` in `snmp.yml` to match your community
  string
- Modify `.scrape_configs.0.static_configs.0.targets.0` in `prometheus.yml` to
  match the IP address of your Edgerouter

Now have your raspberry setup with docker.
Install docker:
```
curl -sSL https://get.docker.com | sh
```

Add user to docker group (requires logout to apply new priviliges).
```
sudo usermod -aG docker pi
```

Install necessary packages.
```
sudo apt-get install -y libffi-dev libssl-dev python3 python3-pip
```

Install pip3 docker-compose.
```
sudo pip3 -v install docker-compose 
```

Once these steps are complete, you can use `docker-compose up` to spin up the
environment. To test the exporter directly without using Prometheus Server,
use the following command (replace with your egerouter ip):
```
curl "http://localhost:9116/snmp?target=192.168.1.1&module=edgerouter"
```
