---

copyright:
  years:  2018, 2023
lastupdated: "2021-03-28"

keywords: IBM Cloud, secure, getting started

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with Secure
{: #getting-started-secure}

In architectures that are focused on container and microservices, you can use *Secure* to protect, monitor, and enhance forensic analysis of your pipeline and runtime components.
{: shortdesc}


## Before you begin
{: #getting-started-secure-prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

Check the regions where the service is available. [Learn more](/docs/monitoring?topic=monitoring-endpoints#endpoints_regions).

You can complete the getting started steps in any of the supported regions.


## Step 1. Manage user access
{: #getting-started-secure-step1}

See [Manage user access](/docs/monitoring?topic=monitoring-getting-started#getting-started-step1).

## Step2. Provision an instance of the {{site.data.keyword.mon_full_notm}} service
{: #getting-started-secure-step2}

See [Provision an instance of the IBM Cloud Monitoring service](/docs/monitoring?topic=monitoring-provision).

## Step3. Connect a data source by configuring a monitoring agent
{: #getting-started-secure-step3}

Complete the following steps:
1. [Configure a monitoring agent](/docs/monitoring?topic=monitoring-config_agent).
2. [Optional] [Enable Kubernetes Audit Logging](https://docs.sysdig.com/en/kubernetes-audit-logging.html){: external} to track kubectl exec and other Kubernetes commands.

## Step 4. Launch the web UI
{: #getting-started-secure-step4}

See [Launch the web UI](/docs/monitoring?topic=monitoring-launch).


## Step 5. Secure your environment
{: #getting-started-secure-step5}

See the following table for tasks that you can run to secure your environment:

| Action                              | Descripion                  |
|-------------------------------------|------------------------------|
| `Integrate scanning into your CI/CD Pipeline` | You can integrate scanning into your CI/CD Pipeline to analyze images that are available on the CI/CD worker nodes. |
| `Configure a notification channel` | You can configure a notification channel to get notified about events, anomalies, or security incidents that require attention. |
| `Scan container images`             | You can scan container images for vulnerabilities, and other violations.  |
| `Configure an image scanning alert` | You can set up a runtime `Scanning Alert` to detect if an image is impacted by newly discovered vulnerabilities. You can scan a repository that hosts container images for vulnerabilities, secrets, and license violations. Then, you can configure an alert on the repository to receive notifications on issues that need your attention.  |
| `Configure a rule`                  | You can create a `Detection Rule` to detect and respond to anomalous runtime activity.  </br>You can create a rule to specify which image versions can be used. |
| `Define policy`                     | You can configure a policy on a resource and define what to do when 1 or more rules that are included in the policy are non-compliant.  </br>Secure includes a number of pre-defined policies that you can use. |
| `Configure a benchmark task`        | You can use `Compliance dashboards and metrics` to monitor the status of your sources based on the benchmark task that you configure.|
