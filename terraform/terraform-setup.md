---

copyright:
  years:  2018, 2025
lastupdated: "2025-03-03"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}



# Setting up Terraform for {{site.data.keyword.mon_full_notm}}
{: #terraform-setup}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitier cloud environments that follow Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.mon_full_notm}} instances by using HashiCorp Configuration Language (HCL). You can optionally connect an {{site.data.keyword.sysdigsecure_full_notm}} instance to your {{site.data.keyword.mon_full_notm}} instance.
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't need to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

Before you begin, ensure that you have the [required access](/docs/monitoring?topic=monitoring-iam) to create and work with {{site.data.keyword.mon_short}} resources.

## Step 1. Install the Terraform CLI
{: #terraform-install-cli}

Complete the following steps to install the Terraform CLI:

1. Create a terraform folder on your local machine, and navigate to your terraform folder.

    ```terraform
    mkdir terraform && cd terraform
    ```
    {: pre}

2. Download the Terraform version that you want.

    For more information about the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform supported versions, see [Installing the Terraform CLI](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli).

    For example, you can download `terraform_0.15.5_darwin_amd64.zip` for a MacOS.

3. Extract the Terraform zip file and copy the files to your terraform directory.

4. Set the environment PATH variable to your Terraform files.

    ```terraform
    export PATH=$PATH:<terraform-directory>/terraform
    ```
    {: codeblock}

5. Verify that the installation is successful by using a terraform command.

    ```terraform
    ./terraform
    ```
    {: pre}

For more information, see [Installing the Terraform CLI](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation).

## Step 2. Set up the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-setup-ibm-plugin}

After the Terraform CLI installation is complete, you must set up the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in IBM Cloud. For a list of supported versions, see the [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.

The setup of the {{site.data.keyword.cloud_notm}} Provider plug-in varies depending on the Terraform CLI version that you want to use. To run your Terraform configuration files with Terraform version 0.13.x or higher, installation of the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform is not required. For more information, see [Terraform v0.13.x and higher](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install-provider-v13).

For example, to run your Terraform configuration files with Terraform version 0.13.x or higher, complete the following steps:
1. Create a `versions.tf` file and specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter.

    ```terraform
    terraform {
        required_providers {
            ibm = {
                source = "IBM-Cloud/ibm"
                version = "<provider version>"
                }
        }
    }
    ```
    {: codeblock}

    For example:

    ```terraform
    terraform {
        required_version = ">= 0.15"
        required_providers {
            ibm = {
                source = "ibm-cloud/ibm"
                version = "~>1.33.0"
            }
        }
    }
    ```
    {: codeblock}

2. Store the `versions.tf` file in your Git repository or the folder where Terraform is set up.


If you are using Terraform on {{site.data.keyword.cloud_notm}} modules, you must add a `versions.tf` file to all the module folders. You can refer the Terraform provider block from the [provider registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest){: external}. You can use the [IBM Cloud Observability - Terraform Module](https://registry.terraform.io/modules/terraform-ibm-modules/observability/ibm/latest){: external} module to configure an instance.
{: note}



## Step 3. Configure the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-config-ibm-plugin}

After you complete the set up, you must [configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference).

Before you can start working with Terraform on {{site.data.keyword.cloud_notm}}, you must retrieve the credentials and parameters that are required for a Terraform resource or data source, and specify them in the `provider` configuration. This configuration is used by the {{site.data.keyword.cloud_notm}} Provider plug-in to authenticate with the {{site.data.keyword.cloud_notm}} platform and to view, create, update, or delete {{site.data.keyword.cloud_notm}} resources and services.

The following table lists input parameters that you can set in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file:

|Input parameter | Required / optional  | Description           |
|----------------|----------------------|-----------------------|
|`ibmcloud_api_key`| Required | The {{site.data.keyword.cloud_notm}} API key to authenticate with the {{site.data.keyword.cloud_notm}} platform. For more information, about how to create an API key, see [Creating an API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key). You can specify the API key in the `provider` block or retrieve the value from the `IC_API_KEY` or `IBMCLOUD_API_KEY` environment variables. If both environment variables are defined, `IC_API_KEY` takes precedence. |
|`ibmcloud_timeout`| Optional | The number of seconds that you want to wait until the {{site.data.keyword.cloud_notm}} API is considered unavailable. The default value is `60`. You can specify the timeout in the `provider` block or retrieve the value from the `IC_TIMEOUT` or `IBMCLOUD_TIMEOUT` environment variables. If both variables are specified, `IC_TIMEOUT` takes precedence. |
|`region`| Optional | The {{site.data.keyword.cloud_notm}} region where you want to create your resources. If this value is not specified, `us-south` is used by default. You can specify the region in the `provider` block or retrieve the value from the `IBMCLOUD_REGION` or `IC_REGION` environment variables. If both environment variables are specified, `IC_REGION` takes precedence. |
|`resource_group`| Optional | The ID of the resource group that you want to use for your {{site.data.keyword.cloud_notm}} resources. To retrieve the ID, run `ibmcloud resource groups`. You can specify the resource group in the `provider` block or retrieve the value from the `IC_RESOURCE_GROUP` or `IBMCLOUD_RESOURCE_GROUP` environment variables. If both environment variables are defined, `IC_RESOURCE_GROUP` takes precedence. |
|`workload_protection_connected_instance`| Optional | Connects an existing {{site.data.keyword.sysdigsecure_full_notm}} instance to the {{site.data.keyword.mon_full_notm}} instance being created. Specify the CRN of the {{site.data.keyword.sysdigsecure_full_notm}} instance to be connected. For more information on connecting instances, see [Can {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} be used together?](/docs/monitoring?topic=monitoring-faq#faq_4) |
{: caption="List of input parameters that you can set in the provider block of your Terraform" caption-side="top"}

For more information on how to use environment variables, see [Using environment variables](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars).

You can [add multiple provider configurations within the same Terraform on the {{site.data.keyword.cloud_notm}} configuration file](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#multiple-providers) to create your {{site.data.keyword.cloud_notm}} resources with different provider parameters. For example, you can multiple providers so that you can use different input parameters, such as different regions, zones, infrastructure generations, or accounts to create the {{site.data.keyword.cloud_notm}} resources in your Terraform on {{site.data.keyword.cloud_notm}} configuration file. For more information, see [Multiple Provider Instances](https://developer.hashicorp.com/terraform/language/providers/configuration){: external}.


### Option 1. Creating a static `provider.tf` file
{: #terraform-config-ibm-plugin-static}

You can declare the input parameters in the `provider` block directly.

Because the `provider` block includes sensitive information, do not commit this file into a public source repository. To add version control to your provider configuration, use a local [`terraform.tfvars` file](#terraform-vars-tf).
{: important}

Complete the following steps:

1. Create a `provider.tf` file and specify the input parameters that are required for your resource or data source.

    ```terraform
    provider "ibm" {
        ibmcloud_api_key = "<api_key>"
        region = "<region>"
    }
    ```
    {: codeblock}


### Option 2. Referencing credentials from a Terraform tfvars file
{: #terraform-config-ibm-plugin-tfvars}

You can store sensitive information, such as credentials, in a local `terraform.tfvars` file and reference these credentials in your `provider` block.

Do not commit the `terraform.tfvars` into a public source repository. This file is meant to be stored in your local machine only.
{: important}

1. Create a `terraform.tfvars` file on your local machine and add the input parameters that are required for your resource or data source.

    ```terraform
    ibmcloud_api_key = "<ibmcloud_api_key>"
    region = "region"
    ```
    {: codeblock}

2. Create a `provider.tf` file and use Terraform interpolation syntax to reference the variables from the `terraform.tfvars`.

    ```terraform
    variable "ibmcloud_api_key" {}
    variable "region" {}

    provider "ibm" {
        ibmcloud_api_key    = var.ibmcloud_api_key
        region = var.region
    }
    ```
    {: codeblock}


## Step 4. Initialize the Terraform CLI.
{: #terraform-init-tf-cli}

Next, initialize the Terraform CLI. Run the following command:

```terraform
./terraform init
```
{: pre}

You should see the following message: `Terraform has been successfully initialized!`.


## Step 5. Create a variables file
{: #terraform-vars-tf}

Create a variables file that is named `variables.tf` to include hard-coded values.

The following sample lists variables that you can use when you provision an instance:

```terraform
variable "service_type" {
  description = "Type of resource instance"
  type = string
  default = "sysdig-monitor"
}

variable "plan" {
  description = "Type of service plan."
  type = string
  default = "graduated-tier"
}

variable "default_receiver" {
  description = "Flag to select the instance to collect platform metrics"
  type = bool
  default = false
}

variable "location" {
  description = "Location where the resource is provisioned"
  type = string
  default = "us-south"
}

variable "name" {
  description = "Name of the resource instance"
  type = string
  default = "demo-monitoring-tf-instance"
}

variable "resource_group_name" {
  description = "Name of the resource group associated with the instance"
  type = string
  default = "observability-demo"
}

variable "key_name" {
  description = "Name of the resource key associated with the instance"
  type = string
  default = "demo-monitoring-tf-instance-key"
}

variable "wp_crn" {
  description = "CRN of rhe IBM Cloud Security and Compliance Center Workload Protection instance to be connected"
  type = string
  default = "crn:v1:bluemix:public:sysdig-secure:us-south:a/11111111111111111111111111111111:11111111-1111-1111-1111-111111111111"
}
```
{: codeblock}

To see the list of valid plan values, see [Plans](/docs/monitoring?topic=monitoring-pricing_plans).

To see the list of valid regions, see [Regions and endpoints](/docs/monitoring?topic=monitoring-endpoints).


## Step 6. Create a Terraform configuration file
{: #terraform-main-tf}

Next, create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a {{site.data.keyword.mon_short}} instance and to assign a user an access policy in Identity and Access Management (IAM) by using HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

The following code shows a sample configuration file to provision an instance. To retrieve the ID of the default resource group, the `ibm_resource_group` data source is used. The region is retrieved from the `terraform.tfvars` file that you created in step 1. Then, the user `user@ibm.com` is assigned the Manager role in the IAM access policy for the namespace for a particular region. The {{site.data.keyword.mon_short}} instance is also connected to an existing {{site.data.keyword.sysdigsecure_short}} instance.

Connecting your {{site.data.keyword.mon_short}} instance to an existing {{site.data.keyword.sysdigsecure_short}} instance is optional.
{: note}

```terraform
data "ibm_resource_group" "group" {
    name = var.resource_group_name
  }

  locals {
    instance_name = "${var.name}-${var.location}"
  }

  // Create a monitoring instance

  resource "ibm_resource_instance" "resource_instance" {
    name = local.instance_name
    service = var.service_type
    plan = var.plan
    location = var.location
    resource_group_id = data.ibm_resource_group.group.id
    tags = ["monitoring", "public"]
    parameters = {
      default_receiver= var.default_receiver,
      workload_protection_connected_instance = var.wp_crn
    }
  }

  // Create the resource key that is associated with the Monitoring instance

  resource "ibm_resource_key" "resourceKey" {
    name = var.key_name
    role = "Manager"
    resource_instance_id = ibm_resource_instance.instance.id
  }

  // Add a user policy for using the resource instance

  resource "ibm_iam_user_policy" "policy" {
    ibm_id = "user@ibm.com"
    roles  = ["Manager", "Viewer"]

    resources {
      service = "sysdig-monitor"
      resource_instance_id = element(split(":", ibm_resource_instance.instance.id), 7)
    }
  }
```
{: codeblock}

For additional information on how to use Terraform for {{site.data.keyword.cloud_notm}} resources, see:
- [ibm_resource_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/resource_instance)
- [ibm_resource_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/resource_key)
- [ibm_iam_service_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_policy)


## Step 7. Provision resources
{: #terraform-provision}

Complete the following steps:

1. Initialize the Terraform CLI.

    ```terraform
    ./terraform init
    ```
    {: pre}

2. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.mon_short}} instance, the resource Key, and IAM access policy in your account.

    ```terraform
    ./terraform plan
    ```
    {: pre}

3. Create the resources.

    ```terraform
    ./terraform apply
    ```
    {: pre}

    To delete resources, run `./terraform destroy`.
    {: tip}


## What's next?
{: #terraform_setup_next}


Verify that the resources are created.
- [Launch the *Observability* UI](/docs/monitoring?topic=monitoring-launch) and check the instance has been created.
- [Launch *Access (IAM)*](https://cloud.ibm.com/iam/overview){: external}. Select **Service IDs** and look for the resource key.
- [Review the user assigned access in the console](/docs/account?topic=account-assign-access-resources&interface=ui#review-your-access-console).
