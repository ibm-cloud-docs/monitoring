---

copyright:
  years: 2018
lastupdated: "2018-09-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Configuring a Sysdig agent
{: #sysdig_config_agent}

After you provision an instance of the Sysdig service in the {{site.data.keyword.Bluemix}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}


## Installing a Sysdig agent
{: #install_agent}

To configure a Sysdig agent, 

1. Install the agent
2. Configure metrics file


You can install a Sysdig agent on any of the following 

Sysdig agents are available as a container or as a service.

You can deploy the agent with an orchestrator such as Kubernetes or Mesos, or without it.
The Sysdig agent in an orchestrated infrastructure such as Kubernetes, Mesos/Marathon, use the respective Installation Guides: 

    Agent Install: Kubernetes | GKE | OpenShift
    Agent Install: Mesos | Marathon | DCOS

install the Sysdig agent directly on a Linux host, without using an orchestrator such as Kubernetes or Mesos.

The agent can be installed two ways: 

    As a standard Docker container 
    As a non-containerized service  

## Configuring a Sysdig agent
{: #config_agent}

## Configuring a Sysdig agent on Linux
{: #config_agent_linux}


 Run this single command to install the agent automatically:

curl -s https://us-south.monitoring.test.cloud.ibm.com/stable/install-agent | sudo bash -s -- --access_key d9512a44-6451-41b3-a5e8-b630bb6cf830 --collector 172.31.19.232 --collector_port 6666 -e SECURE=false --check_certificate false --tags example_tag:example_value

curl -s https://us-south.monitoring.test.cloud.ibm.com/install-agent | sudo bash -s --access_key d9512a44-6451-41b3-a5e8-b630bb6cf830 --collector 172.31.19.232 --collector_port 6666 -e SECURE=false --check_certificate false

Tagging your machines is highly recommended!
Replace example_tag:example_value in the commands with a comma-separated list of tags (eg. role:webserver,location:europe). 


## Uninstalling a Sysdig agent
{: #uninstall_agent}

Sysdig agent when it was installed as a service. If the agent was installed as a container, remove it using standard Docker commands.


## Installing Sysdig agent on Kubernetes
{: #kube}


 install a Sysdig agent container in a Kubernetes environment. This document assumes you will run the agent container as a Kubernetes pod, which then enables the Sysdig agent automatically to detect and monitor your Kubernetes environment. 



Create the first agent using the Sysdig Wizard

1. Watch the video
2. Choose an installatiomn method:
 -non-orchestrated: Docker
 - non-orchestrated: Native linux
 - Kubernetes |iks| Openshift
 - <esos | Marathin | DCOS

 3. Setup the environment

  Waiting for first node to connect... Go ahead and follow the instructions below!

The Sysdig Monitor agent is available to run inside a single Docker container to report on the entire host.

    First, install kernel headers on the host:
    Debian-like distributions:

    apt-get -y install linux-headers-$(uname -r)

RHEL-like distributions:

yum -y install kernel-devel-$(uname -r)

Now install the Sysdig Monitor container on the host:

    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=eccbc556-63cc-48ef-b404-feb0e93f0219 -e COLLECTOR=172.31.19.232 -e COLLECTOR_PORT=6443 -e CHECK_CERTIFICATE=false -e TAGS=example_tag:example_value -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent

    Note, this will run the container in detached mode. To see the container's output, remove the "-d".

Tagging your machines is highly recommended!
Replace example_tag:example_value in the commands with a comma-separated list of tags (eg. role:webserver,location:europe).
Note: tags will also be created automatically from your infrastructure's metadata, including AWS, Docker, Mesos, Kubernetes, etc

If you have any issues, please refer to the full installation instructions.
And do not hesitate to contact us at support@sysdig.com!
