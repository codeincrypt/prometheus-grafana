# Install Prometheus

Installing Prometheus in Ubuntu Server

[Prometheus Official Link](https://prometheus.io/docs/prometheus/latest/getting_started)

## Download and install

[Download Prometheus](https://prometheus.io/download/)

Download the latest release of Prometheus for your platform, then extract and run it:

or, download prometheus-2.45.0 through CLI
```
wget https://github.com/prometheus/prometheus/releases/download/v2.45.0/prometheus-2.45.0.linux-amd64.tar.gz
```

or, download prometheus-2.45.0 through CLI
```
tar -xvfz prometheus-*.tar.gz
cd prometheus-*
```

Note : If you already setup the `systemctl` for prometheus in linux system, then no need to use the below commands / steps, then go to `systemctl` part.


## Start Prometheus

By default, Prometheus stores its database in ./data (flag --storage.tsdb.path).
```
./prometheus --config.file=prometheus.yml
```
or,
To run in background
```
nohup ./prometheus --config.file=prometheus.yml &
```

## Configuring Prometheus to monitor itself

Prometheus collects metrics from targets by scraping metrics HTTP endpoints. Since Prometheus exposes data in the same manner about itself, it can also scrape and monitor its own health.

While a Prometheus server that collects only data about itself is not very useful, it is a good starting example. Save the following basic Prometheus configuration as a file named `prometheus.yml`

```
global:
  scrape_interval:     15s # By default, scrape targets every 15 seconds.

  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'codelab-monitor'

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'

    # Override the global default and scrape targets from this job every 5 seconds.
    scrape_interval: 5s

    static_configs:
      - targets: ['localhost:9090']
```

## Start Prometheus using systemctl

It is time to configure Prometheus as a service inside the systemd. Create a file prometheus.service.

```
sudo nano /etc/systemd/system/prometheus.service
```
And put the lines mentioned below in the file and save it
```
[Unit]
Description=Prometheus Server
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart= /home/centos/prometheus-2.18.1.linux-amd64/prometheus \
--config.file= /home/centos/prometheus-2.18.1.linux-amd64/prometheus.yml \
--storage.tsdb.path=/home/centos/prometheus-2.18.1.linux-amd64/ \
--web.console.templates= /home/centos/prometheus-2.18.1.linux-amd64/consoles \
--web.console.libraries= /home/centos/prometheus-2.18.1.linux-amd64/console_libraries

[Install]
WantedBy=multi-user.target
```


Using systemctl, reload the systemd system, and start the Prometheus service. Its status should show the service is running if you have followed all the steps correctly.

To Start Prometheus with systemd
```
sudo systemctl daemon-reload
sudo systemctl start prometheus
```
To check Prometheus status with systemd

```
sudo systemctl status prometheus
```


Configure the Prometheus server to start at boot:

```
sudo systemctl enable prometheus.service
```


Restart the server with systemd, 
To restart the service and verify that the service has started, run the following commands:

```
sudo systemctl restart prometheus
sudo systemctl status prometheus
```

After that you can check that Prometheus is running on PORT 9090
```
sudo netstat -tulpn
```
or,
```
sudo netstat -tulpn | grep 9090
```
Open Prometheus UI
```
http://{HOSTNAME}:9090
```

## Prometheus Web UI
Open the browser and access to server’s IP with port 9090 to access the web interface of Prometheus.

[Prometheus Dashboard](http://localhost:9090/)
