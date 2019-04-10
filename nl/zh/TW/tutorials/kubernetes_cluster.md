---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# 分析 Kubernetes 叢集中部署之應用程式的度量
{: #kubernetes_cluster}

使用此指導教學，可以瞭解如何配置叢集，以將度量轉遞至 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.mon_full_notm}} 服務。
{:shortdesc}

您可以使用 {{site.data.keyword.mon_full_notm}} 服務來監視 Kubernetes 叢集。

若要配置叢集以轉遞度量，您必須使用 DaemonSet，在 Kubernet 叢集的每一個工作者節點上安裝代理程式。Sysdig 代理程式會使用存取金鑰（記號），透過 {{site.data.keyword.mon_full_notm}} 實例進行鑑別。Sysdig 代理程式會充當資料收集器。它會自動收集度量，例如*工作者節點 CPU* 和工作者節點記憶體*、*進出容器* 的 HTTP 資料傳輸流量，以及幾個常見基礎架構軟體等的相關度量。此外，代理程式還可以使用 Prometheus 相容提取器或 Statsd Facade，來收集自訂應用程式度量。 

您可以透過 Sysdig 的 Web 型使用者介面來檢視度量。

![元件概觀，關於 {{site.data.keyword.cloud_notm}}](../images/kube.png "元件概觀，關於 {{site.data.keyword.cloud_notm}}")



## 開始之前
{: #kubernetes_cluster_prereqs}

為了完成此入門指導教學中的步驟，會提供指示以在美國南部地區佈建 {{site.data.keyword.mon_full_notm}} 的實例。您可以使用現有叢集或新的**叢集 1.10 版**。可在不同地區使用叢集。  

閱讀 {{site.data.keyword.mon_full_notm}} 的相關資訊。如需相關資訊，請參閱[關於](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)。

使用身為成員或是 {{site.data.keyword.cloud_notm}} 帳戶擁有者的使用者 ID。若要取得 {{site.data.keyword.cloud_notm}} 使用者 ID，請移至：[登錄 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

您的 {{site.data.keyword.IBM_notm}} ID 必須已獲指派下列每一個資源的 IAM 原則： 

| 資源                             | 存取原則的範圍 | 角色    | 地區    | 資訊                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| 資源群組 **Default**           |  資源群組            | 檢視者  | us-south  | 需要此原則，以容許使用者查看 Default 資源群組中的服務實例。|
| {{site.data.keyword.mon_full_notm}} 服務 |  資源群組            | 編輯者  | us-south  | 需要此原則，以容許使用者在 Default 資源群組中佈建及管理 {{site.data.keyword.mon_full_notm}} 服務。|
| Kubernetes 叢集實例          |  資源                 | 編輯者  | us-south  | 需要此原則，以在 Kubernetes 叢集中配置密碼及 Sysdig 代理程式。|
{: caption="表 1. 完成指導教學所需的 IAM 原則清單" caption-side="top"} 

如需 {{site.data.keyword.containerlong}} IAM 角色的相關資訊，請參閱[使用者存取權](/docs/containers?topic=containers-access_reference#access_reference)。

安裝 {{site.data.keyword.cloud_notm}} CLI 及 Kubernetes CLI 外掛程式。如需相關資訊，請參閱[安裝 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。


## 步驟 1：佈建 {{site.data.keyword.mon_full_notm}} 實例
{: #kubernetes_cluster_step1}

若要透過 {{site.data.keyword.cloud_notm}} 使用者介面佈建 {{site.data.keyword.mon_full_notm}} 的實例，請完成下列步驟：

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶。

    按一下 [{{site.data.keyword.cloud_notm}} 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}，以啟動 {{site.data.keyword.cloud_notm}} 儀表板。

	在使用您的使用者 ID 和密碼登入之後，即會開啟 {{site.data.keyword.cloud_notm}} 使用者介面。

2. 按一下**型錄**。即會開啟 {{site.data.keyword.cloud_notm}} 中可用的服務清單。

3. 若要過濾顯示的服務清單，請選取**開發人員工具**種類。

4. 按一下 **{{site.data.keyword.mon_full_notm}}** 磚。即會開啟*觀察* 儀表板。

5. 選取**建立案例**。 

6. 輸入服務實例的名稱。

7. 選取 **Default** 資源群組。 

    依預設，會設定 **Default** 資源群組。

8. 選取**試用**服務方案。 

    依預設，會設定**試用**方案。

    如需其他服務方案的相關資訊，請參閱[定價方案](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

9. 若要在您登入的 {{site.data.keyword.cloud_notm}} 資源群組中佈建 {{site.data.keyword.mon_full_notm}} 服務，請按一下**建立**。

在佈建實例之後，即會開啟*觀察* 儀表板。 


**附註：**若要透過 CLI 佈建實例，請參閱[透過 {{site.data.keyword.cloud_notm}} CLI 佈建實例](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)。


## 步驟 2：配置 Kubernets 叢集以將度量傳送至實例
{: #kubernetes_cluster_step2}

若要配置 Kubernetes 叢集以將度量傳送至 {{site.data.keyword.mon_full_notm}} 實例，您必須在叢集的每一個節點上安裝 Sysdig 代理程式 Pod。Sysdig 代理程式是透過 DaemonSet 安裝，其可確保代理程式的實例正在每個工作者節點上執行。Sysdig 代理程式會從已安裝它的 Pod 中收集度量，然後將資料轉遞至您的實例。

**附註：**為了提供整套的系統度量，Sysdig 代理程式需要具有特許狀態。

若要配置 Kubernetes 叢集以將度量轉遞至 {{site.data.keyword.mon_full_notm}} 實例，請從指令行完成下列步驟：

1. 開啟終端機。然後，登入 {{site.data.keyword.cloud_notm}}。請執行下列指令，並遵循提示：

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    選取您已佈建 {{site.data.keyword.mon_full_notm}} 實例的帳戶。

2. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

3. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

4. 取得汲取 URL。如需相關資訊，請參閱 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

5. 部署 Sysdig 代理程式。請執行下列指令：

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是實例的汲取金鑰。

    * COLLECTOR_ENDPOINT 是可以使用監視實例之地區的汲取 URL。

    * TAG_DATA 是以逗點區隔的標籤，其格式為 *TAG_NAME:TAG_VALUE*。您可以使一個以上的標籤與 Sysdig 代理程式產生關聯。例如：*role:serviceX,location:us-south*。稍後，您可以使用這些標籤，從執行代理程式的環境識別度量。

    * 將 **sysdig_capture_enabled** 設為 *false*，以停用 Sysdig 擷取功能。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

6. 驗證是否已順利建立 Sysdig 代理程式，並驗證其狀態。請執行下列指令：

    ```
    kubectl get pods
    ```
    {: codeblock}



## 步驟 3：啟動 Sysdig Web 使用者介面
{: #kubernetes_cluster_step3}

請完成下列步驟來啟動 Web 使用者介面：

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶。

    按一下 [{{site.data.keyword.cloud_notm}} 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}，以啟動 {{site.data.keyword.cloud_notm}} 儀表板。

	在使用您的使用者 ID 和密碼登入之後，即會開啟「{{site.data.keyword.cloud_notm}} 儀表板」。

2. 在導覽功能表中，選取**觀察**。 

3. 選取**監視**。 

    即會顯示 {{site.data.keyword.cloud_notm}} 上可用的實例清單。

4. 選取您的實例。然後，按一下**檢視 Sysdig**。

如果已順利配置 Sysdig 代理程式，則會開啟*探索* 視圖。

不過，如果未順利安裝 Sysdig 代理程式、指向錯誤的汲取端點，或存取金鑰不正確，則開啟的頁面會通知您，下一步做什麼。

每個瀏覽器只能開啟一個 Web 使用者介面階段作業。
{: tip}


## 步驟 4：監視叢集
{: #kubernetes_cluster_step4}

您可以在透過 Web 使用者介面使用的**探索**視圖中監視您的叢集。此視圖是疑難排解及監視基礎架構的起點。它是使用者 Web 使用者介面的預設首頁。

在*主機及容器* 區段中，您可以查看叢集中正在將度量轉遞至監視實例的工作者節點清單。每一個工作者節點項目代表該工作者節點的相關基礎架構物件群組。

按一下**主機及容器** ![主機及容器](../images/switch_hosts.png) 來切換資料來源。然後，選取工作者節點。顯示的資料對應於您已選取的工作者節點。

如果您按一下**回到探索表格**，則會顯示*探索表格*。每一欄都會顯示不同的度量。您可以個別配置每一個度量。您可以變更直欄的順序。請注意，若您對現有直欄的順序進行變更，則在您登入時，變更會在不同分組之間持續存在。如果您新增或移除直欄，則變更會持續存在。您也可以配置顏色，以強調顯示值並提高可讀性。

例如，若要配置直欄的顏色編碼，請完成下列步驟：

1. 選取一個直欄。將滑鼠移至直欄標題上方。然後，選取鉛筆圖示。
2. 切換功能表列以啟用顏色編碼。
3. 設定不同臨界值。

如果選取工作者節點，則會顯示預設儀表板。按一下 ![切換儀表板](images/switch_dashboards_1.png)，並探索不同的預設儀表板及度量。請注意，您只能選取與所選工作者節點相關的度量及儀表板。


## 後續步驟
{: #kubernetes_cluster_next_steps}

建立自訂儀表板。如需相關資訊，請參閱[使用儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)。

您也可以進一步瞭解警示。如需相關資訊，請參閱[使用警示](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。 






