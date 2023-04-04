
# Install Grafana

Installing Grafana in Ubuntu Server

## Download and install

You can install Grafana using APT repository, by downloading a `.deb` package, or by downloading a binary `.tar.gz` file.


[Grafana Download & Install Official Docs](https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/#1-download-and-install)

## Start the server

Start the server with systemd
To start the service and verify that the service has started:

To Start Grafana with systemd
```
sudo systemctl daemon-reload
sudo systemctl start grafana-server
```

To check Grafana status with systemd

```sudo systemctl status grafana-server```


Configure the Grafana server to start at boot:

```sudo systemctl enable grafana-server.service```


Restart the server with systemd, 
To restart the service and verify that the service has started, run the following commands:

```
sudo systemctl restart grafana-server
sudo systemctl status grafana-server
```