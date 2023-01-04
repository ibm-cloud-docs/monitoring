---

copyright:
  years:  2018, 2023
lastupdated: "2022-08-22"

keywords: IBM Cloud, monitoring, iam, trusted profile

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Trusted profiles
{: #trusted_profiles}

{{site.data.keyword.mon_full}} supports {{site.data.keyword.iamlong}} (IAM) trusted profiles to grant  federated users access to your account with conditions based on SAML attributes from your corporate directory. Trusted profiles can also be used to set up fine-grained authorization for applications that are running in compute resources. This way, you aren't required to create service IDs or API keys for the compute resources.
{: shortdesc}

If you are using a trusted profile, the email address associated with the trusted profile cannot be used when configuring [notifications.](/docs/monitoring?topic=monitoring-notifications)
{: note}

See [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile) for information on setting up trusted profiles that can be used with {{site.data.keyword.mon_full_notm}}.
