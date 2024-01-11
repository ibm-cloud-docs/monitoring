---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-11"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Alerts library
{: #alert-library}

To help you get started, {{site.data.keyword.mon_full_notm}} provides a set of curated alert templates in the *Alerts Library*. {{site.data.keyword.mon_full_notm}} automatically detects the applications and services running in your environment and recommends alerts that you can enable.
{: shortdesc}

Two types of alert templates are included in the *Alerts Library*:

Recommended
:   Alert suggestions based on the services that are detected running in your infrastructure.

All templates
:   Templates for all services. For some templates, you might need to configure the integration for the service.

## Accessing the Alerts Library
{: #alert-library-access}

To access the Alerts Library from the *Alert* section of the UI, select **Library**.

## Configuring an alert for a service
{: #alert-library-config}

1. In the library you can enter a search term or scroll through the list of all templates, or recommended templates.

    For example, click `Kubernetes`. Template suggestions are displayed for Kubernetes services running on the environment.

2. From a list of template suggestions, click the desired template.

3. Click **Enable Alert** and configure the alert.

4. Click **Enable Alert**.

## Enabling multiple alerts using templates
{: #alert-library-config-mult}

You can enable multiple alerts by selecting multiple templates.

1. In the library you can enter a search term or scroll through the list of all templates, or recommended templates.

    For example, click `Kubernetes`. Template suggestions are displayed for Kubernetes services running on the environment.

2. From a list of template suggestions, select the check boxes next to the desired templates.

3. Click **Enable Alerts** and configure the alert.

4. Click **Enable Alerts**.

## Identifying templates that are in use
{: #alert-library-inuse}

Alerts that have been configured using templates will show `Alert in use` in the template library.
