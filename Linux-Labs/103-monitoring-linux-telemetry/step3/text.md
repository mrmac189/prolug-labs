In your reseach you find that the Prometheus can read telemetry data from Node Exporter. Your tasks will be to deploy and configure Prometheus to poll telemetry data from Node Exporter.

Install Prometheus.

Configure Prometheus to gather telemetry data.

Ensure that Prometheus is running correctly.

<br>

### Solution



Setup your server for Prometheus install

```plain
useradd prometheus
```

```plain
mkdir /var/lib/prometheus
```

Download and extract Prometheus and required tools.

```plain
wget https://github.com/prometheus/prometheus/releases/download/v2.42.0-rc.0/prometheus-2.42.0-rc.0.linux-amd64.tar.gz  -P /tmp
tar xvfz /tmp/prometheus-2.42.0-rc.0.linux-amd64.tar.gz -C /var/lib/prometheus/ --strip-components=1
cp /var/lib/prometheus/prometheus /usr/bin/prometheus
```

Change ownership of /var/lib/prometheus so that prometheus user can start the service

```plain
chown -R prometheus:prometheus /var/lib/prometheus/
```

Create a directory and copy over the configuration for prometheus

```plain
mkdir /etc/prometheus
cp /answers/prometheus.yml /etc/prometheus/prometheus.yml
```

View the file and look at the configuration

```plain
cat /etc/prometheus/prometheus.yml
```

Copy over the prometheus.service file so that systemd can control and start prometheus

```plain
cp /answers/prometheus.service /etc/systemd/system/prometheus.service
```

View the file and look at the configuration

```plain
cat /etc/systemd/system/prometheus.service
```

Start the Prometheus Service

```plain
systemctl daemon-reload
systemctl start prometheus
```

Verify that Prometheus is working

```plain
systemctl status prometheus.service --no-pager
ps -ef | grep [p]rometheus
```

You can also access prometheus via this link:

{{TRAFFIC_HOST1_9090}}

