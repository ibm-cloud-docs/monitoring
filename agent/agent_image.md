---

copyright:
  years:  2021
lastupdated: "2021-11-29"

keywords: IBM Cloud, monitoring, monitoring, agent image, container registry, icr

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Getting information about Kubernetes monitoring agent images 
{: #monitoring_agent_image}

Kubernetes monitoring agent images are public images that are available in {{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started) service.
{: shortdesc}

You can access the images that are provided by {{site.data.keyword.IBM}} by using the command line.

Complete the following steps to get information about the monitoring agent images:

## Before you begin
{: #monitoring_agent_image_prereqs}

Before you begin, complete the following tasks:

1. Ensure that the {{site.data.keyword.registrylong_notm}} CLI is installed, see [Installing the `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#cli_namespace_registry_cli_install).

2. Log in to [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login):

    ```text
    ibmcloud login
    ```
    {: pre}


## Step 1. Target the global registry
{: #monitoring_agent_image_step1}

Run the following command:

```text
ibmcloud cr region-set global
```
{: pre}



## Step 2. List the monitoring agent images that are hosted in the global registry
{: #monitoring_dna_agent_image_step2}

Run the following command:

```text
ibmcloud cr images --restrict ext/sysdig
```
{: codeblock}

The output of this command is the list of monitoring agent images. It includes information about the repository, `icr.io/ext/sysdig`, the image tag, the image digest, the image namespace, when the image was created, the image size, and the images security status.

You can find the following images in the registry:

- `icr.io/ext/sysdig/agent`: You can use this image, that includes the kernel module, to deploy the full agent.
- `icr.io/ext/sysdig/agent-slim`: You can use this image to deploy the slim agent. This image also requires the initContainer agent-kmodule image `icr.io/ext/sysdig/agent-kmodule-thin` to pre-build the kernel module.
- `icr.io/ext/sysdig/agent-kmodule`: Image for the initContainer that is used for building the kernel module from the headers or by downloading a precompiled version.
- `icr.io/ext/sysdig/agent-kmodule-thin`: Image for the initContainer that is used for building the kernel module when you deploy the slim agent. It is a smaller version of the agent-kmodule image, it has less dependencies, and it removes unused packages.



