---

copyright:
  years: 2018, 2025
lastupdated: "2025-03-03"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.mon_full_notm}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for {{site.data.keyword.mon_full_notm}}, see [Understanding your responsibilities when using {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-shared-responsibilities).

## Dependent services
{: #data-portability-dependencies}

{{site.data.keyword.mon_full_notm}} interacts with the following {{site.data.keyword.cloud_notm}} services. See the documentation for these services for data portability related to these services.

* [{{site.data.keyword.iamlong}}](/docs/account) for access control.

* [{{site.data.keyword.en_full_notm}}](/docs/event-notifications) as a notification channel for triggered alerts.

* [{{site.data.keyword.messagehub_full_notm}}](/docs/EventStreams) for extracted {{site.data.keyword.mon_full_notm}} notifications to be sent using the {{site.data.keyword.messagehub}} API.

## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.mon_full_notm}} has two types of data:

* Metrics data
* Configuration data

### Metrics data
{: #data-portability-metrics}



{{site.data.keyword.mon_full_notm}} metrics data cannot be exported.

### Configuration data
{: #data-portability-config}

{{site.data.keyword.mon_full_notm}} provides mechanisms to export settings and configurations that are used to process the customer's content.

| Configuration data | Export using |
|--------------------|--------------|
| Custom dashboards | [List API](/apidocs/monitor#listlightusingget-2)  \n [Get API](/apidocs/monitor#getusingget-4) |
| Alerts | [List API](/apidocs/monitor#getactiveprometheusalertusingget)  \n [Get API](/apidocs/monitor#getprometheusrulebyalertidsusingget) |
| Teams configurations | [List API](/apidocs/monitor#getprometheusrulebyalertidsusingget)  \n [Get API](/apidocs/monitor#getusingget-12) |
{: caption="Configuration export methods" caption-side="bottom"}

## Exported data formats
{: #data-portability-data-formats}



{{site.data.keyword.mon_full_notm}} configuration data is exported in JSON format.

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS&cc=us&lc=en){: external}.
