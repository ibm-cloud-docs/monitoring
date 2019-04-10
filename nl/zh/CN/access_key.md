---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# 使用访问密钥
{: #access_key}

**访问密钥**是一种令牌，必须使用此令牌来配置 Sysdig 代理程序，才能成功将数据转发到 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.mon_full_notm}} 实例。   
{:shortdesc}


## 通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥
{: #access_key_ibm_cloud_ui}

要通过 {{site.data.keyword.cloud_notm}} UI 获取 {{site.data.keyword.mon_full_notm}} 实例的访问密钥，请完成以下步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} 帐户。

    单击 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window} 以启动 {{site.data.keyword.cloud_notm}}“仪表板”。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}} UI 将打开。

2. 在导航菜单中，选择**可观察性**。 

3. 选择**监视**。这将打开 {{site.data.keyword.mon_full_notm}} 仪表板。可以查看 {{site.data.keyword.cloud_notm}} 上可用的监视实例的列表。

3. 确定要获取其访问密钥的实例，然后单击**查看访问密钥**。

4. 这将打开一个弹出窗口，在其中可以单击**显示**以查看访问密钥。



## 通过 CLI 获取访问密钥
{: #access_key_cli}

要通过命令行获取 Sysdig 实例的访问密钥，请完成以下步骤：

1. [先决条件] 安装 {{site.data.keyword.cloud_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

   如果 CLI 已安装，请继续执行下一步。

2. 登录到 {{site.data.keyword.cloud_notm}} 中运行 Sysdig 实例的区域。运行以下命令：[`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. 设置运行 Sysdig 实例的资源组。运行以下命令：[`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    缺省情况下，已设置 `default` 资源组。

4. 获取实例名称。运行以下命令：[`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. 获取与 Sysdig 实例关联的 API 密钥的名称。运行 [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) 命令：

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    其中，INSTANCE_NAME 是在上一步中获取的实例的名称。

6. 获取访问密钥。运行 [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) 命令：

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    其中，APIKEY_NAME 是 API 密钥的名称。
 
    此命令的输出包含 **Sysdig Access Key** 字段，其中含有实例的访问密钥。


例如，以下命令显示样本服务标识的输出：

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## 重置访问密钥 
{: #access_key_reset}

如果访问密钥泄露，或者您有用于在一定天数后更新访问密钥的策略，那么可以生成新密钥并删除旧密钥。

要更新 {{site.data.keyword.mon_full_notm}} 实例的访问密钥，请完成以下步骤：

1. 启动 {{site.data.keyword.mon_full_notm}} Web UI。有关更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。

2. 通过导航栏中的*选择器*按钮，选择**设置**。

2. 在*密码管理*部分中，单击**重置密码**。

**注：**重置 Sysdig 访问密钥后，必须更新已配置为将度量值转发到此 {{site.data.keyword.mon_full_notm}} 实例的任何日志源的访问密钥。
