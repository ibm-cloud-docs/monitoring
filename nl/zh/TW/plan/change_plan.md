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


# 變更方案
{: #change_plan}

您可以透過 {{site.data.keyword.monitoringlong_notm}} 儀表板或執行 `cf update-service` 指令，來變更 {{site.data.keyword.monitoringshort}} 服務方案。您隨時可以升級或降低方案。
{:shortdesc}

## 透過使用者介面變更服務方案
{: #change_plan_ui}

若要在 {{site.data.keyword.monitoringlong_notm}} 儀表板中變更服務方案，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從「儀表板」中按一下 {{site.data.keyword.monitoringshort}} 服務。 

    即會開啟 {{site.data.keyword.monitoringshort}} 服務儀表板。
    
2. 選取**方案**標籤。

    即會顯示現行方案的相關資訊。
	
3. 選取新方案以升級或降低您的方案。 

4. 按一下**儲存**。



## 透過 CLI 變更服務方案
{: #change_plan_cli}

若要在 {{site.data.keyword.Bluemix_notm}} 中透過 CLI 變更服務方案，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
	
2. 執行 `ibmcloud service list` 指令來檢查現行方案，以及從空間中的可用服務清單取得 {{site.data.keyword.loganalysisshort}} 服務名稱。 

    **name** 欄位的值就是您必須用來變更方案的值。 

    例如，
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. 升級或降低您的方案。執行 `ibmcloud service update` 指令。
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	其中 
	
	* *service_name* 是服務的名稱。 
	* *new_plan* 是方案的名稱。
	
	下表列出不同的方案及其支援的值：
	
	<table>
	  <caption>表 1. 方案清單。</caption>
	  <tr>
	    <th>方案</th>
		<th>特性</th>
	    <th>名稱</th>
	  </tr>
	  <tr>
	    <td>精簡</td>
	    <td>免費監視。</td>
		<td>lite</td>
	  </tr>
	  <tr>
	    <td>超值</td>
	    <td>超值監視。</td>
		<td>premium</td>
	  </tr>
	</table>
	
	例如，若要將您的方案降低為*精簡* 方案，請執行下列指令：
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. 驗證新的方案已變更。執行 `ibmcloud service list` 指令。

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service       plan   bound apps   last operation
    Monitoring-0c     Monitoring    lite                create succeeded
	```
	{: screen}






