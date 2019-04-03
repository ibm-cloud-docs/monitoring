---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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


# 更改套餐
{: #change_plan}

可以通过 {{site.data.keyword.monitoringlong_notm}} 仪表板或通过运行 `cf update-service` 命令来更改 {{site.data.keyword.monitoringshort}} 服务套餐。您可以随时升级或降级套餐。
{:shortdesc}

## 通过 UI 更改服务套餐
{: #change_plan_ui}

要在 {{site.data.keyword.monitoringlong_notm}} 仪表板中更改服务套餐，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后在“仪表板”中单击 {{site.data.keyword.monitoringshort}} 服务。 

    这将打开 {{site.data.keyword.monitoringshort}} 服务仪表板。
    
2. 选择**套餐**选项卡。

    这将显示有关当前套餐的信息。
	
3. 选择新套餐以升级或降级现有套餐。 

4. 单击**保存**。



## 通过 CLI 更改服务套餐
{: #change_plan_cli}

要在 {{site.data.keyword.Bluemix_notm}} 中通过 CLI 更改服务套餐，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
	
2. 运行 `ibmcloud service list` 命令以检查当前套餐，并从空间中可用的服务列表中获取 {{site.data.keyword.loganalysisshort}} 服务名称。 

    **name** 字段的值是必须用于更改套餐的名称。 

    例如：
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. 升级或降级套餐。运行 `ibmcloud service update` 命令。
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	其中 
	
	* *service_name* 是服务的名称。 
	* *new_plan* 是套餐的名称。
	
	下表列出了不同的套餐及其支持的值：
	
	<table>
	  <caption>表 1. 套餐列表</caption>
	  <tr>
	    <th>套餐</th>
		<th>功能</th>
	    <th>名称</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>免费监视。</td>
		<td>lite</td>
	  </tr>
	  <tr>
	    <td>高级</td>
	    <td>高级监视。</td>
		<td>premium</td>
	  </tr>
	</table>
	
	例如，要将套餐降级到*轻量*套餐，请运行以下命令：
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. 验证是否已更改为新套餐。运行 `ibmcloud service list` 命令。

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service       plan       bound apps   last operation
    Monitoring-0c     Monitoring    lite                    create succeeded
	```
	{: screen}






