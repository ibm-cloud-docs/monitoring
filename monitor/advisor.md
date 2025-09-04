---
copyright:
  years:  2018, 2025
lastupdated: "2025-09-04"

keywords:

subcollection: monitoring
---

{{site.data.keyword.attribute-definition-list}}

# Monitoring Advisors
{: #advisors}

{{site.data.keyword.mon_full}} features Monitoring Advisors to provide deep insights into your infrastructure, from high-level performance overviews to actionable data for troubleshooting specific issues. Advisors are available for Kubernetes and IBM Virtual Server for VPC instances (VSIs).
{: shortdesc}

## VSI for VPC Advisor
{: #vsi-advisor}

This advisor offers a single pane of glass, simplifying visibility across your entire infrastructure down to specific VSI instances, accelerating problem identification, and ensuring operational health.

To access the Advisor, Click **Advisor** > **VSI for VPC**.

Beyond typical monitoring insights (CPU, memory, disk, network, and so on), this tool "advises" you about common problems that your hosts might have such as elevated CPU or memory utilization. When these issues arise, immediate insights are crucial. The system delivers critical details, including:

- Resource usage: From a troubleshooting point of view, the Advisor shows when issues occur, how often, and for how long, so teams see not just a CPU or memory spike, but its timing and frequency.

- Advisories: Information on common issues that affect VMs—like CPU throttling, out‑of‑memory errors, or host‑not‑present events.

- Detailed resource usage by process: You can correlate the resource usage with the processes involved, to identify the root cause at a process level.

- Alert suggestions: Suggests alert rules that teams can enable with one click, so teams are notified the next time the issue occurs.

Proactive monitoring keeps your VSI hosts healthy and your users unaffected. This solution allows for easy configuration of alerts for these common problems. Instant notifications are triggered the moment a critical event occurs — such as  a sudden spike in CPU or memory. These alerts ensure continuous awareness of potential issues, enabling remediation before services or users are impacted.

## Kubernetes Advisor
{: #kubernetes-advisor}

The Kubernetes Advisor is a robust Kubernetes troubleshooting tool integrated within {{site.data.keyword.mon_full_notm}} that significantly accelerates the resolution process by up to ten times. It offers a prioritized list of issues along with relevant data, enabling you to quickly pinpoint and address critical problems.

To access the Advisor, Click **Advisor** > **Kubernetes**.


### Scope Tree
{: #scope-tree}

In the Scope Tree, you can navigate through your Kubernetes infrastructure from all the resources (where you will be able to check all your Kubernetes, IKS, ROKS, and so on, clusters) to one specific container running in a namespace. When you click on any level in the scope tree (a cluster name, a namespace, a container, and so on) the information presented  will change to show information related to that part of your infrastructure.

### Advisories
{: #advisories}

Along with the detailed information about the current level of the Scope Tree, {{site.data.keyword.mon_full_notm}} will also show some issues presented in your infrastructure in an opinionated way. These pieces of troubleshooting content are the *Advisories*. They will tell you not only what the issue is, but also where it is happening, when it started, what specific resources are affected, and how you can remediate the issue. Each of these Advisories have a different level of urgency: Low, Medium or High. These are the Advisories you can find in the Kubernetes Advisor:

- Pods in CrashloopBackOff
- Image Pull Error
- CPU Throttling
- Out-of-memory kill
- Replicas Unavailable
- Cluster CPU Overcommitment
- Cluster Memory Overcommitment
- Container Error
- Cluster Pod Capacity issues

Also, each one of these Advisories will allow you to enable an alert, in a very quick and easy way, to be notified next time there is a similar issue.
