odules:
  http_2xx:
    prober: http
    timeout: 3s

    http:
      valid_http_versions: ["HTTP/1.1", "HTTP/2.0"]
      valid_status_codes: []  # Defaults to 2xx
      method: GET
      no_follow_redirects: false

scrape_configs:
  - job_name: 'blackbox'
    metrics_path: /probe
    params:
      module: [http_2xx]  # Look for a HTTP 200 response.
    static_configs:
      - targets:
        - https://www.ibm.com/software/passportadvantage/pao_customer.html   # Target to probe with https.
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 52.117.190.199:9115  # The blackbox exporter's real hostname:port.
~                                                                                                                                                        
~                                                                                                                                                        
~                                                                                                                                                        
~                                                                                                                                                        
~                                                                                                      

The Blackbox exporter provides metrics about HTTP latencies, DNS lookups latencies as well as statistics about SSL certificates expiration.

The Blackbox exporter is mainly used to measure response times. 
Blackbox exporter is going to expose a HTTP endpoint that can be used in order to monitor targets over the network. By default, the Blackbox exporter exposes the /probe endpoint that is used to retrieve those metrics.

http://localhost:9115/probe?target=https://google.com&module=https_2xx

You are going to define ‘targets’ in a dedicated Blackbox configuration section, and Prometheus will issue requests to the probe endpoint we saw earlier.

Prometheus is acting as a way to automate requests and as a way to store them for long-term storage.

The Blackbox exporter configuration file is made of modules.

A module can be seen as one probing configuration for the Blackbox exporter.

As a consequence, if you choose to have a HTTP prober checking for successful HTTPS responses (2xx HTTP codes for example), the configuration will be summarized within the same module.

As a consequence, the Blackbox exporter will report if it successfully probed the targets it was assigned (0 for a failure and 1 for a success).

the Blackbox exporter only focuses on availability 

https://prometheus.io/download/

wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.17.0/blackbox_exporter-0.17.0.linux-amd64.tar.gz

tar xvzf blackbox_exporter-0.17.0.linux-amd64.tar.gz

you are going to define service files and define start and restart policies for it.

First, make your executables accessible for your user local account.

$ sudo mv blackbox_exporter /usr/local/bin

    Note : by moving files to the /usr/local/bin path, all users may have access to the blackbox exporter binary. For binaries to be restricted to your own user account, you need to add the path to your own PATH environment variable.

Next, create configuration folders for your blackbox exporter.

`/etc/blackbox`

$ sudo mkdir -p /etc/blackbox
$ sudo mv blackbox.yml /etc/blackbox

For safety purposes, the Blackbox exporter is going to be run by its own user account (named blackbox here)

As a consequence, we need to create a user account for the Blackbox exporter.

$ sudo useradd -rs /bin/false blackbox

Then, make sure that the blackbox binary can be run by your newly created user.

$ sudo chown blackbox:blackbox /usr/local/bin/blackbox_exporter

Give the correct permissions to your configuration folders recursively.

$ sudo chown -R blackbox:blackbox /etc/blackbox/*

 create your service file.

To create the Blackbox exporter service, head over to the /lib/systemd/system folder and create a service named blackbox.service

$ cd /lib/systemd/system
$ sudo touch blackbox.service


$ sudo nano blackbox.service

[Unit]
Description=Blackbox Exporter Service
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=blackbox
Group=blackbox
ExecStart=/usr/local/bin/blackbox_exporter \
  --config.file=/etc/blackbox/blackbox.yml \
  --web.listen-address=":9115"

Restart=always

[Install]
WantedBy=multi-user.target


Save your service file, and make sure that your service is enabled at boot time.

$ sudo systemctl enable blackbox.service
$ sudo systemctl start blackbox.service


For now the Blackbox exporter is not configured to scrape any targets, but we are going to add a few ones in the next section.

If your service is correctly running, you can check the metrics gathered by issuing a request to the HTTP API.

$ curl http://localhost:9115/metrics


Binding the Blackbox exporter with Prometheus

    Important note: in this section, Prometheus is going to scrape the Blackbox Exporter to gather metrics about the exporter itself.

    To configure Prometheus to scrape HTTP targets, head over to the next sections.


    To bind the Blackbox exporter with Prometheus, you need to add it as a scrape target in Prometheus configuration file.

If you follow the Prometheus setup tutorial, your configuration file is stored at /etc/prometheus/prometheus.yml

Edit this configuration file, and amend the following change

--------

Prometheus is a time series database, created in 2012 and part of the Cloud Native Computing Foundation, that exposes dozens of exporters for you to monitor anything.

On the other hand, Grafana is probably one of the most popular monitoring tools.

In Grafana, you create dashboards that bind to datasources (such as Prometheus) in order to visualize your metrics in near real-time.

Grafana & Prometheus natively bind together, so today we are going to see how you can setup Prometheus and Grafana on your Linux system.

Download Prometheus

prometheus-2.20.1.linux-amd64.tar.gz    https://prometheus.io/download/

wget https://github.com/prometheus/prometheus/releases/download/v2.20.1/prometheus-2.20.1.linux-amd64.tar.gz

Untar it to extract the files in the archive.

$ tar xvzf prometheus-2.21.1.linux-amd64.tar.gz

The archive contains many important files, but here is the main ones you need to know.

    prometheus.yml: the configuration file for Prometheus. This is the file that you are going to modify in order to tweak your Prometheus server, for example to change the scraping interval or to configure custom alerts;
    prometheus: the binary for your Prometheus server. This is the command that you are going to execute to launch a Prometheus instance on your Linux box;
    promtool: this is a command that you can run to verify your Prometheus configuration.

We are not going to execute directly the Prometheus, instead we are going to configure it as a service

First of all, for security purposes, you are going to create a Prometheus user with a Prometheus group.

$ sudo useradd -rs /bin/false prometheus

Make sure to move the binaries to your local bin directory.

I stored my binaries in a Prometheus folder, located on my home directory.

Here’s the command to move them to the bin directory.

$ cd Prometheus/prometheus-2.11.2.linux-amd64/ 
$ sudo cp prometheus promtool /usr/local/bin

Give permissions to the Prometheus user for the prometheus binary.

$ sudo chown prometheus:prometheus /usr/local/bin/prometheus

Create a folder in the /etc folder for Prometheus and move the console files, console libraries and the prometheus configuration file to this newly created folder.

$ sudo mkdir /etc/prometheus
$ sudo cp -R consoles/ console_libraries/ prometheus.yml /etc/prometheus

Create a data folder at the root directory, with a prometheus folder inside.

$ sudo mkdir -p /usr/prometheus/data

Give the correct permissions to those folders recursively.

$ sudo chown -R prometheus:prometheus /usr/prometheus/data /etc/prometheus/*

Head over to the /lib/systemd/system folder and create a new file named prometheus.service

$ cd /lib/systemd/system
$ sudo touch prometheus.service



[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=prometheus
Group=prometheus
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path="/data/prometheus" \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  --web.enable-admin-api

Restart=always

[Install]
WantedBy=multi-user.target


Save your file, enable your service at startup, and start your service.

$ sudo systemctl enable prometheus
$ sudo systemctl start prometheus


# sudo systemctl status prometheus
* prometheus.service - Prometheus
   Loaded: loaded (/lib/systemd/system/prometheus.service; enabled; vendor preset: enabled)
   Active: failed (Result: exit-code) since Tue 2020-09-08 04:31:29 CDT; 1min 21s ago
  Process: 31963 ExecStart=/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/data/prometheus --web.console.temp
 Main PID: 31963 (code=exited, status=2)

Sep 08 04:31:29 baremetal01 systemd[1]: prometheus.service: Service hold-off time over, scheduling restart.
Sep 08 04:31:29 baremetal01 systemd[1]: prometheus.service: Scheduled restart job, restart counter is at 5.
Sep 08 04:31:29 baremetal01 systemd[1]: Stopped Prometheus.
Sep 08 04:31:29 baremetal01 systemd[1]: prometheus.service: Start request repeated too quickly.
Sep 08 04:31:29 baremetal01 systemd[1]: prometheus.service: Failed with result 'exit-code'.
Sep 08 04:31:29 baremetal01 systemd[1]: Failed to start Prometheus.



he problem is the permissions on /data/prometheus should be set to prometheus user and group.

so the sollution is: sudo chown -R prometheus:prometheus /data/prometheus/


If you follow the Prometheus setup tutorial, your configuration file is stored at /etc/prometheus/prometheus.yml

Edit this configuration file, and amend the following changes

`/etc/prometheus/`

$ sudo nano /etc/prometheus/prometheus.yml

global:
  scrape_interval:     15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
    - targets: ['localhost:9090', 'localhost:9115']

With Prometheus, you don’t need to restart the systemd service for Prometheus to update.

You can also send a signal to the process for it to restart.

In order to send a SIGHUP signal to your Prometheus process, identify the PID of your Prometheus server.

$ ps aux | grep prometheus
schkn  4431  0.0  0.0  14856  1136 pts/0    S+   09:34   0:00 /bin/prometheus --config.file=...

The PID of my Prometheus process is 4431. Send a SIGHUP signal to this process for the configuration to restart.

$ sudo kill -HUP 4431

Head over to your Prometheus target configuration (http://localhost:9090/targets), and check that you are correctly scrapping your Blackbox exporter.
Binding the Blackbox Exporter to Prometheus


root@baremetal01:/etc/prometheus# sudo systemctl stop prometheus
root@baremetal01:/etc/prometheus# sudo systemctl start prometheus



`/opt/draios/etc/`

root@baremetal01:/etc/prometheus# cd /opt/draios/etc/
root@baremetal01:/opt/draios/etc# nano dragent.yaml 



customerid: 7ac04746-1104-4f82-8445-f71427dd2a1d
collector: ingest.us-south.monitoring.cloud.ibm.com
collector_port: 6443
ssl: true
sysdig_capture_enabled: false
tags: resourceType:baremetal,region:dallas
prometheus:
     enabled: true
     interval: 30
     log_errors: true
     max_metrics: 3000
     max_metrics_per_process: 3000
     max_tags_per_metric: 20
prometheus:
        enabled: true
        interval: 30
        log_errors: true
        max_metrics: 3000
        max_metrics_per_process: 3000
        max_tags_per_metric: 20
        remote_services:
            - blackbox_bm01:
                always:
                conf:
                url: "http://localhost:9115/probe?target=https://www.ibm.com/software/passportadvantage/pao_customer.html&module=https_2xx"
                tags:
                    service: passport-advantage-dallas-uptime
                    hostname: baremetal01





sudo sysdig-probe-loader
* Unloading sysdig-probe, if present
* Running dkms install for sysdig
Module sysdig/0.27.0 already installed on kernel 4.15.0-99-generic/x86_64
* Trying to load a dkms sysdig-probe, if present
sysdig-probe found and loaded in dkms



remote_services:
         - blackbox_bm_01:
             always:
             conf:
             url: "http://localhost:9115/probe?module=http_2xx&target=https://www.ibm.com/software/passportadvantage/pao_customer.html"
             tags:
                 service: passport_advantage_uptime
                 service_hostname: baremetal01
                 service_region: us-south


