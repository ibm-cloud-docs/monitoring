---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

 
# 在 {{site.data.keyword.cloud_notm}} 中管理用户访问权
{: #iam}

通过 {{site.data.keyword.iamlong}} (IAM)，您能够在 {{site.data.keyword.cloud_notm}} 中安全地认证用户，并以一致的方式控制对所有云资源的访问权。
{:shortdesc}

**对于访问您帐户中的 {{site.data.keyword.mon_full_notm}} 服务的每个用户，必须向其分配定义了 IAM 用户角色的访问策略。**该策略确定用户可以在所选服务或实例的上下文中执行的操作。允许的操作可定制且定义为允许在服务上执行的操作。然后，这些操作将映射到 IAM 用户角色。

*策略*允许在不同级别授予访问权。部分选项包括： 

* 对帐户中所有启用 IAM 的服务的访问权
* 对帐户中单个区域中所有服务实例的访问权
* 对帐户中单个服务实例的访问权
* 对资源组上下文中所有服务实例的访问权
* 对资源组上下文中单个区域内所有服务实例的访问权
* 对资源组上下文中所有启用 IAM 的服务的访问权

*角色*定义用户或服务标识可以运行的操作。{{site.data.keyword.cloud_notm}} 中有不同类型的角色：
* *平台管理角色*支持用户在平台级别对服务资源执行任务，例如为用户分配对服务的访问权，创建或删除服务标识，创建实例，将服务的策略分配给其他用户，以及将实例绑定到应用程序。
* *服务访问角色*支持为用户分配各种级别的许可权以调用服务的 API。

**要将一组用户和服务标识组织成单个实体，以便轻松管理 IAM 许可权，请使用***访问组*。* 可以将单个策略分配给组，而不必逐个用户或服务标识多次分配相同的访问权。
{: tip}


## 使用访问组管理访问权
{: #iam_groups}

要使用访问组来管理用户的访问权或为用户分配新的访问权，您必须是帐户中所有启用 Identity and Access 的服务的帐户所有者、管理员或编辑者，或者分配有对“IAM 访问组”服务的管理员或编辑者角色。 

选择以下任一操作来管理 {{site.data.keyword.cloud_notm}} 中的访问组：

* [创建访问组](/docs/iam?topic=iam-groups#create_ag)。
* [为组分配访问权](/docs/iam?topic=iam-groups#access_ag)。


## 通过将策略直接分配给用户来管理访问权
{: #iam_users}

要使用 IAM 策略来管理用户的访问权或为用户分配新访问权，您必须是帐户所有者、帐户中所有服务的管理员，或者是特定服务或服务实例的管理员。 

选择以下任一操作来管理 {{site.data.keyword.cloud_notm}} 中的 IAM 策略：

* 要修改用户的许可权，请参阅[编辑现有访问权](/docs/iam?topic=iam-iammanidaccser#edit_existing)。
* 要向用户授予许可权，请参阅[分配新访问权](/docs/iam?topic=iam-iammanidaccser#assign_new_access)。
* 要撤销许可权，请参阅[除去访问权](/docs/iam?topic=iam-iammanidaccser#removing_access)。
* 要复查用户的许可权，请参阅[复查分配的访问权](/docs/iam?topic=iam-iammanidaccser#review_your_access)。


## {{site.data.keyword.cloud_notm}} 平台角色
{: #iam_platform}

使用下表可确定可以在 {{site.data.keyword.cloud_notm}} 中授予用户以用于运行以下任一平台操作的平台角色：

|平台操作|{{site.data.keyword.cloud_notm}} 平台角色| 
|-------------------------------------------------------------------------|------------------------------------------------------|
|`授予其他帐户成员使用服务的访问权`|管理员| 
|`供应服务实例`| 管理员 </br>编辑者 | 
|`删除服务实例`| 管理员 </br>编辑者 | 
|`创建服务标识`| 管理员 </br>编辑者 |
|`查看服务实例的详细信息`| 管理员 </br>编辑者 </br>操作员</br>查看者| 
|`在“可观察性监视”仪表板中查看服务实例`| 管理员 </br>编辑者 </br>操作员</br>查看者| 
{: caption="表 1. IAM 用户角色和操作" caption-side="top"}



## Sysdig 角色
{: #iam_sysdig_roles}

下表概述了 Sysdig 角色和每个角色可执行的操作：

|操作|Sysdig 角色| 
|----------------------------------------------------------------------------|------------------------------------------------------|
|`重置 Sysdig 访问密钥`|管理员|
|`管理用户`|管理员|
|`创建、配置和删除团队`|管理员|
|`配置和除去通知通道`|管理员| 
|`配置和除去 Sysdig 代理程序`|管理员|
|`在 Sysdig Web UI 中创建、删除和编辑内容`| 管理 </br>用户                                      |  
|`通过 Sysdig Web UI 查看度量值`| 管理 </br>用户                                      |  
|`创建和删除警报`| 管理 </br>用户                                      | 
|`创建和删除捕获`| 管理 </br>用户                                      |   
{: caption="表 2. Sysdig 角色和操作" caption-side="top"}


## 将 Sysdig 角色映射到 {{site.data.keyword.cloud_notm}} 角色
{: #iam_sysdig}

使用下表可查看 {{site.data.keyword.cloud_notm}} 角色如何映射到 Sysdig 角色：

|角色类型|角色|Sysdig 角色|描述|
|---------------------|--------------------|----------------------------|---------------------------------------------|
|平台角色|管理员|管理员|向用户授予 Sysdig 管理员特权。| 
|服务角色|管理者|管理员|向用户授予 Sysdig 管理员特权。| 
|服务角色|写入者|用户|向用户授予 Sysdig 用户特权。|
|服务角色|读取者|                            |未授予许可权。|
{: caption="表 3. Sysdig 角色" caption-side="top"}


