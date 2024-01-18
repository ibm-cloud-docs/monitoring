---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-09"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Deploying Workload Protection features on a host
{: #deploy-secure-features}

{{site.data.keyword.mon_full_notm}} can be configured to integrate {{site.data.keyword.sysdigsecure_short}} features.
{: shortdesc}

For more information about {{site.data.keyword.sysdigsecure_short}}, see the [{{site.data.keyword.sysdigsecure_full}} documentation.](/docs/workload-protection).
{: note}

## Step 1. Check the service plan of your {{site.data.keyword.mon_short}} instance
{: #check_plan}

If you have the {{site.data.keyword.mon_short}} service deployed in your account with the `Graduated tier` service plan, you must upgrade to the `Graduated Tier - Sysdig Secure + Monitor` plan.

If you provision a {{site.data.keyword.mon_short}} instance, choose the `Graduated Tier - Sysdig Secure + Monitor` plan.

{{site.data.content.combined-plan-deprecated}}

## Step 2. Deploy the agent for orchestrated environments by using Helm
{: #deploy_with_helm}

For orchestrated environments, deploy the {{site.data.keyword.mon_short}} agent by using Helm:
- [Deploying an agent on a Kubernetes cluster by using helm](/docs/monitoring?topic=monitoring-agent-deploy-kube-helm).
- [Deploying an agent on a {{site.data.keyword.redhat_openshift_notm}} cluster by using helm](/docs/monitoring?topic=monitoring-agent-deploy-openshift-helm).


You can only deploy the agent by using Helm if you want to use the {{site.data.keyword.sysdigsecure_short}} features on an orchestarted environment. If you deployed your agent by using the script, you must manually remove the agent and redeploy it by using Helm.
{: important}
