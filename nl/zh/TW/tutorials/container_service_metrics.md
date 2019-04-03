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


# 在 Grafana 中分析 Kubernetes 叢集的度量值
{: #container_service_metrics}

使用此指導教學，以學習如何使用 {{site.data.keyword.monitoringlong}} 服務監視容器效能。
{:shortdesc}


## 目標
{: #ks_objectives}

學習如何搜尋及分析 Kubernetes 叢集中所部署應用程式的容器度量值：

1. 識別在何處將叢集中所收集的度量值轉遞至 {{site.data.keyword.monitoringshort}} 服務。 
2. 啟動 Grafana，並設定您可檢視叢集度量值的 {{site.data.keyword.monitoringshort}} 網域。
3. 搜尋及分析 {{site.data.keyword.Bluemix_notm}} 的 Kubernetes 叢集中所部署應用程式的容器度量值。

本指導教學逐步引導您取得在 {{site.data.keyword.Bluemix_notm}} 中運作之下列完整情境所需的步驟：佈建叢集、識別在何處叢集將度量值傳送至 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.monitoringshort}} 服務、在叢集中部署應用程式，以及使用 Grafana 來檢視及過濾該叢集的容器度量值。


**附註：**若要完成此指導教學，您必須完成必要條件以及不同步驟中所鏈結的指導教學。


## 必要條件
{: #ks_prereqs}

1. 是 {{site.data.keyword.Bluemix_notm}} 帳戶的成員或擁有者，並具有許可權可以建立 Kubernetes 標準叢集、將應用程式部署至叢集，以及查詢 {{site.data.keyword.Bluemix_notm}} 中 Grafana 監視的度量值。

    {{site.data.keyword.Bluemix_notm}} 的使用者 ID 必須已獲指派下列原則：
    
    * 具有 *operator* 或 *administrator* 許可權之 {{site.data.keyword.containershort}} 的 IAM 原則。
    
    如需相關資訊，請參閱[透過 IBM Cloud 使用者介面將 IAM 原則指派給使用者](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_ui)。

2. 具有終端機階段作業，您可以從中管理 Kubernetes 叢集，並從指令行部署應用程式。本指導教學中的範例是針對 Ubuntu Linux 系統。

3. 安裝 CLI，以在 Ubuntu 系統中使用 {{site.data.keyword.containershort}}。

    * 安裝 {{site.data.keyword.Bluemix_notm}} CLI。 
    * 安裝 {{site.data.keyword.containershort}} CLI，以在 {{site.data.keyword.containershort}} 中建立及管理 Kubernetes 叢集，以及將容器化應用程式部署至叢集。
    
    如需相關資訊，請參閱[安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview)。
    
    

    
 

## 步驟 1：佈建 Kubernetes 叢集
{: #ks_step1}

請完成下列步驟：

1. 建立標準 Kubernetes 叢集。如需相關資訊，請參閱[建立 Kubernetes 標準叢集](/docs/containers/cs_tutorials.html#cs_cluster_tutorial)。

2. 在終端機中設定叢集環境定義。設定環境定義之後，您可以管理 Kubernetes 叢集，並在 Kubernetes 叢集中部署應用程式。

    登入 {{site.data.keyword.Bluemix_notm}} 中與所建立叢集相關聯的地區、組織及空間。如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。

	起始設定 {{site.data.keyword.containershort}} 服務外掛程式。

	```
	ibmcloud cs init
	```
	{: codeblock}

    將終端機環境定義設為叢集。
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    此指令的執行輸出提供您必須在終端機中執行的指令，以設定配置檔的路徑。例如：

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    複製並貼上指令，以在終端機中設定環境變數，然後按 **Enter**。



## 將查看帳戶網域中度量值的許可權授與使用者
{: #ks_step2}

若要將檢視帳戶網域中度量值的許可權授與使用者，您必須為使用者指派 {{site.data.keyword.monitoringshort}} 服務的 IAM 原則及**檢視者**角色。

完成下列步驟，以授與使用者使用 {{site.data.keyword.monitoringshort}} 服務的許可權：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者* 視窗會顯示目前已選取帳戶的使用者及其電子郵件位址清單。
	
3. 如果使用者是帳戶成員，請從清單中選取使用者名稱，或按一下*動作* 功能表中的**管理使用者**。

    如果使用者不是帳戶的成員，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

4. 選取**存取原則 > 指派存取權 > 指派資源的存取權**。

5. 選擇服務 **{{site.data.keyword.monitoringlong}}**、選取叢集可用地區（在此指導教學中是**美國南部**），然後選取角色 **viewer**。



## 步驟 3：授與 {{site.data.keyword.containershort_notm}} 金鑰擁有者許可權
{: #ks_step3}

若要叢集將度量值轉遞至帳戶網域，{{site.data.keyword.containershort}} 金鑰擁有者必須要有下列 IAM 原則：

* {{site.data.keyword.monitoringshort}} 服務的 IAM 原則與 **editor** 許可權。
* {{site.data.keyword.containershort}} 的 IAM 原則與 **administrator** 許可權。


請完成下列步驟，以授與 {{site.data.keyword.containershort}} 金鑰擁有者許可權：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者* 視窗會顯示目前已選取帳戶的使用者及其電子郵件位址清單。
	
3. 尋找 {{site.data.keyword.containershort}} 金鑰擁有者使用者 ID。

    執行指令 `ibmcloud cs api-key-info ClusterName`，以取得 {{site.data.keyword.containershort}} 金鑰擁有者使用者 ID。

4. 選取**存取原則 > 指派存取權 > 指派資源的存取權**。

5. 選擇服務 **{{site.data.keyword.monitoringlong}}**、選取叢集可用地區（在此指導教學中是**美國南部**），然後選取角色 **editor**。	

6. 重複步驟 2 到 4，然後選擇 {{site.data.keyword.containershort}} 服務。選取**所有地區**，以及角色 **administrator**。	




## 步驟 4：在 Kubernetes 叢集中部署範例應用程式
{: #ks_step4}

在 Kubernetes 叢集中部署及執行範例應用程式。完成下列指導教學中的步驟，以部署範例應用程式：[課程 1：將單一實例應用程式部署至 Kubernetes 叢集](/docs/containers/cs_tutorials_apps.html#cs_apps_tutorial_lesson1)。

應用程式是 Hello World Node.js 應用程式：

```
    var express = require('express')
    var app = express()

    app.get('/', function(req, res) {
      res.send('Hello world! Your app is up and running in a cluster!\n')
    })
app.listen(8080, function() {
      console.log('Sample app is listening on port 8080.')
    })
```
{: screen}

在此範例應用程式中，當您在瀏覽器中測試應用程式時，應用程式會將下列訊息寫入至 stdout：`Sample app is listening on port 8080`。


## 步驟 5：啟動 Grafana 並設定度量值網域
{: #ks_step5}

從瀏覽器啟動 Grafana，並設定您可檢視叢集度量值的 {{site.data.keyword.monitoringshort}} 網域。

若要分析叢集的度量值，您必須在叢集建立所在的「雲端公用」地區中存取 Grafana。如需相關資訊，請參閱[從 Web 瀏覽器導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser)。

1. 從瀏覽器啟動 Grafana。 

    輸入您已建立叢集之地區的 {{site.data.keyword.monitoringshort}} 服務 URL。 
    
    若要取得每個地區的 URL，請參閱[監視服務的 URL](/docs/services/cloud-monitoring/monitoring_ov.html#region)。

    例如，對於「美國南部」地區，啟動：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 將 {{site.data.keyword.monitoringshort}} 網域設為 **Account**。

    在 Grafana 中，選取 ID。然後，確認您使用正確的帳戶，並選擇網域。選取 `Domain = account`。

    叢集會將度量值轉遞至帳戶度量值網域。 

## 步驟 6：在 Grafana 中監視叢集
{: #ks_step6}

{{site.data.keyword.containershort}} 提供 Grafana 儀表板，以用來監視叢集度量值。 

請完成下列步驟，以開啟範例儀表板：

1. 選取側邊功能表列切換 ![Grafana 側邊功能表列](images/grafana_settings.gif "Grafana 側邊功能表列")。
2. 選取**儀表板**。
3. 按一下**開啟**。
4. 選取 **ClusterMonitoringDashboard_v1**。

即會開啟範例儀表板。 

![Grafana 範例儀表板](images/cluster_grafana_sample_dashboard.png "Grafana 範例儀表板")



## 後續步驟
{: #ks_next_steps}

定義度量值的警示。如需相關資訊，請參閱[配置警示](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov)。
