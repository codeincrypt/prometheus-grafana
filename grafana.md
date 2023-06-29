
# Install Grafana

Installing Grafana in Ubuntu Server

## Download and install

You can install Grafana using APT repository, by downloading a `.deb` package, or by downloading a binary `.tar.gz` file.


[Grafana Download](https://grafana.com/grafana/download)

Install generic font configuration library
```
sudo apt-get install -y adduser libfontconfig1
```

Download grafana deb file through this below command, or you can direct download from Grafana
```
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.0.1_amd64.deb
```

```
sudo dpkg -i grafana-enterprise_9.3.2_amd64.deb
```
## Start the server

Start the server with systemd
To start the service and verify that the service has started:

To Start Grafana with systemd
```
sudo systemctl daemon-reload
sudo systemctl start grafana-server
```
To check Grafana status with systemd

```
sudo systemctl status grafana-server
```


Configure the Grafana server to start at boot:

```
sudo systemctl enable grafana-server.service
```


Restart the server with systemd, 
To restart the service and verify that the service has started, run the following commands:

```
sudo systemctl restart grafana-server
sudo systemctl status grafana-server
```

After that you can check that Grafana is running on PORT 3000
```
sudo netstat -tulpn
```
or,
```
sudo netstat -tulpn | grep 3000
```


Open Grafana dashboard
```
http://{HOSTNAME}:3000
```

## Use dashboards
This topic provides an overview of dashboard features and shortcuts, and describes how to use dashboard search


[Grafana Dashboard](https://grafana.com/docs/grafana/latest/dashboards/use-dashboards/)

