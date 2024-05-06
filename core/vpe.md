---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-03"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.mon_full_notm}}
{: #vpe-connection}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables you to connect to {{site.data.keyword.mon_full_notm}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

## Before you begin
{: #prereq-service-endpoint}

Before you target a virtual private endpoint for {{site.data.keyword.mon_full_notm}} you must complete the following tasks.

* Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
* Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
* Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways) are set for your virtual private endpoint.
* Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
* Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

### Configuring an endpoint gateway
{: #endpoint-gateway-servicename}

To configure a virtual private endpoint gateway, follow these steps:

1. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.mon_full_notm}} that you want to be privately available to the VPC.
2. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
3. View the created VPE gateways associated with the {{site.data.keyword.mon_full_notm}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.mon_full_notm}} instance privately through it.

## Limitations
{: #vpe-limitations}

The following limitations exist when using {{site.data.keyword.mon_full_notm}} with VPEs.

* Only agent metrics are available through VPEs. Prometheus clients and REST APIs are not supported.
