Your team has decided that the data for Prometheus will be exposed via the tool Node Exporter. Your jobs is to get Node Exporter up and running on your server.

Install Node Exporter.

Verify Node Exporter is running and exposing port 9100.

<br>

### Solution
<details>
<summary>Solution</summary>
Create the directory where we will install Node Exporter.

```plain
mkdir /opt/node_exporter
```

`cd` into that directory to set up the server.

```plain
cd /opt/node_exporter
```

Download and unpackage a current version of Node Exporter and move to the extracted folder.

```plain
wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
tar xvfz node_exporter-*.*-amd64.tar.gz
cd node_exporter-*.*-amd64
```

Download the example systemd setup from their github repository into a new directory named `config_files`

```
git clone https://github.com/prometheus/node_exporter.git config_files
```

Copy over the `node_exporter.service` and `node_exporter.socket` file to the systemd directory

```plain
cp /opt/node_exporter/node_exporter-*.*-amd64/config_files/examples/systemd/node_exporter.service /etc/systemd/system/node_exporter.service

cp /opt/node_exporter/node_exporter-*.*-amd64/config_files/examples/systemd/node_exporter.socket /etc/systemd/system/node_exporter.socket
```

Copy the sysconfig settings from config_files and the binary for node_explorer as indicated in node_exporter.service

```
cp node_exporter /usr/sbin/
cp /opt/node_exporter/node_exporter-*.*-amd64/config_files/examples/systemd/sysconfig.node_exporter /etc/sysconfig/node_exporter
```

Create a directory named /var/lib/node_exporter/textfile_collector

```
mkdir -p /var/lib/node_exporter/textfile_collector
```

Create a user for node_exporter and apply ownerships to files needed

```
useradd -s /sbin/nologin node_exporter
chown -R node_exporter:node_exporter /var/lib/node_exporter/textfile_collector
chown -R node_exporter:node_exporter /etc/sysconfig/node_exporter
```

Review the service file so that you are confident it is going to properly start Node Exporter.

```plain
cat /etc/systemd/system/node_exporter.service
```

Now that you've checked everything reload the systemd configuration manager and start Node Exporter daemon.

```plain
systemctl daemon-reload
systemctl enable node_exporter.service --now
```

Verify that Node Exporter is running and exposing the proper port.

```plain
systemctl status node_exporter --no-pager
sleep 2
curl http://localhost:9100/metrics
```

What data can you see exposed? Don't worry if it's not well formatted for you to process, it's in the correct configuration for Prometheus to scrape.

</details>