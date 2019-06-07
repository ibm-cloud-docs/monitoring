---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-10"

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


# 分析 Kubernetes 叢集裡部署之應用程式的度量
{: #kubernetes_cluster}

使用本指導教學瞭解如何配置 {{site.data.keyword.containerlong}} 叢集，以將度量值轉遞至 {{site.data.keyword.mon_full}} 服務。
{:shortdesc}

若要配置叢集以轉遞度量值，必須使用 [DaemonSet ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) 將 Sysdig 代理程式安裝到 Kubernetes 叢集裡的每個工作者節點上。Sysdig 代理程式會使用存取金鑰（記號），向 {{site.data.keyword.mon_full_notm}} 實例進行鑑別。Sysdig 代理程式會充當資料收集器。它會自動收集度量值，例如*工作者節點 CPU* 和*工作者節點記憶體* 用量、*進出容器的 HTTP 資料流量* 以及幾個基礎架構元件的相關資料。此外，代理程式還可以使用 Prometheus 相容提取器或 StatsD Facade，來收集自訂應用程式度量值。 

您可以透過 Sysdig 的 Web 型使用者介面來檢視度量值。

![元件概觀，關於 {{site.data.keyword.cloud_notm}}](../images/kube.png "元件概觀，關於 {{site.data.keyword.cloud_notm}}")

## 目標
{: #kubernetes_cluster_objectives}

在本指導教學中，您使用 {{site.data.keyword.containerlong}} 叢集裡的 Sysdig 配置度量值。尤其是：
*  佈建 {{site.data.keyword.mon_full_notm}} 實例。
*  配置您叢集裡的 Sysdig 代理程式，以將度量值傳送至 Sysdig。
*  使用 Sysdig Web 使用者介面分析叢集度量值。


## 開始之前
{: #kubernetes_cluster_prereqs}

1. 閱讀 {{site.data.keyword.mon_full_notm}} 的相關資訊。如需相關資訊，請參閱[關於](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)。

2. 具有身為成員或是 {{site.data.keyword.cloud_notm}} 帳戶擁有者的使用者 ID。若要取得 {{site.data.keyword.cloud_notm}} 使用者 ID，請移至：[登錄 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

3. 安裝 {{site.data.keyword.cloud_notm}} CLI 及 Kubernetes CLI 外掛程式。如需相關資訊，請參閱[安裝 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

4. [建立叢集](/docs/containers?topic=containers-clusters#clusters)或使用現有的 {{site.data.keyword.containerlong_notm}} 叢集。
    *  叢集必須執行 Kubernetes V1.10 或更高版本。
    *  叢集不必位於**達拉斯**位置，但可以位於任何 [{{site.data.keyword.containerlong_notm}} 地區](/docs/containers/cs_regions.html#regions-and-zones)。

5. 確保您的使用者 ID 指派有下列 {{site.data.keyword.iamlong}} 原則：

| 資源                             | 存取原則的範圍 | 角色    | 地區    | 資訊                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
|資源群組 **Default**           |  資源群組            | 檢視者  | Us-south  | 需要此原則，以容許使用者查看 Default 資源群組中的服務實例。|
| {{site.data.keyword.mon_full_notm}} 服務 |  資源群組            | 編輯者  | Us-south  |要容許使用者在 Default 資源群組中佈建和管理 {{site.data.keyword.mon_full_notm}} 服務，此原則是為必要。|
| Kubernetes 叢集實例          |  資源                 | 編輯者  | Us-south  | 需要此原則，以在 Kubernetes 叢集裡配置密碼及 Sysdig 代理程式。|
{: caption="表 1. 完成指導教學所需的 IAM 原則清單" caption-side="top"}

如需 {{site.data.keyword.containerlong}} IAM 角色的相關資訊，請參閱[使用者存取權](/docs/containers?topic=containers-access_reference#access_reference)。



## 步驟 1. 佈建 {{site.data.keyword.mon_full_notm}} 實例
{: #kubernetes_cluster_step1}

在本入門指導教學中，提供了在美國南部地區中佈建 {{site.data.keyword.mon_full_notm}} 實例的指示。如需支援的地區的相關資訊，請參閱[地區](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints)。

若要透過 {{site.data.keyword.cloud_notm}} 使用者介面佈建 {{site.data.keyword.mon_full_notm}} 的實例，請完成下列步驟：

1. [登入 {{site.data.keyword.cloud_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

	在使用您的使用者 ID 和密碼登入之後，即會開啟 {{site.data.keyword.cloud_notm}} 使用者介面。

2. 按一下**型錄**。即會開啟 {{site.data.keyword.cloud_notm}} 中可用的服務清單。

3. 若要過濾顯示的服務清單，請選取**開發人員工具**種類。

4. 按一下 **{{site.data.keyword.mon_full_notm}}** 磚。即會開啟*觀察* 儀表板。

5. 選取**建立案例**。 

6. 輸入服務實例的名稱。

7. 選取 **Default** 資源群組。 

    您可以在您有建立資源的許可權的任何資源群組中佈建實例。

    依預設，會設定 **default** 資源群組。

8. 選取**試用**服務方案。 

    依預設，會設定**試用**方案。

    如需其他服務方案的相關資訊，請參閱[定價方案](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

9. 按一下**建立**。

    佈建實例後，*觀察* 儀表板將開啟並顯示**監視**實例的詳細資料。 


若要透過 CLI 來佈建實例，請參閱[透過 {{site.data.keyword.cloud_notm}} CLI 來佈建實例](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)。
{: note}


## 步驟 2. 配置 Kubernetes 叢集以將度量值傳送到實例
{: #kubernetes_cluster_step2}

若要配置 Kubernetes 叢集以將度量值傳送至 {{site.data.keyword.mon_full_notm}} 實例，您必須在叢集的每一個節點上安裝 Sysdig 代理程式 Pod。Sysdig 代理程式是透過 DaemonSet 安裝，其可確保代理程式的實例正在每個工作者節點上執行。Sysdig 代理程式會從已安裝它的 Pod 中收集度量值，然後將資料轉遞至您的實例。

為了提供整套的系統度量，Sysdig 代理程式需要具有特許狀態。
{: note}

若要配置 Kubernetes 叢集以將度量值轉遞至 {{site.data.keyword.mon_full_notm}} 實例，請從指令行完成下列步驟：

1. 開啟終端機。然後，登入 {{site.data.keyword.cloud_notm}}。請執行下列指令，並遵循提示：

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    選取叢集可用的帳戶。

2. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。複製並貼上終端機中顯示的指令，以設定 `KUBECONFIG` 環境變數。

    每次登入到 {{site.data.keyword.containerlong}} CLI 來使用叢集時，必須執行這些指令以將叢集配置檔的路徑設定為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。
    {: tip}

3. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

4. 從 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)獲取汲取 URL。

5. 部署 Sysdig 代理程式。請執行下列指令：

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: pre}

    其中

    * **SYSDIG_ACCESS_KEY** 是先前所擷取實例的汲取金鑰。

    * **COLLECTOR_ENDPOINT** 是可使用先前所擷取監視實例之地區的汲取 URL。

    * **TAG_DATA** 是格式為 *TAG_NAME:TAG_VALUE* 的逗號分隔標籤。您可以使一個以上的標籤與 Sysdig 代理程式產生關聯。例如：*role:serviceX,location:us-south*。稍後，您可以使用這些標籤，從執行代理程式的環境識別度量值。

    * 將 **sysdig_capture_enabled** 設為 *false*，以停用 Sysdig 擷取特性。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

6. 驗證是否已順利建立 Sysdig 代理程式，並驗證其狀態。請執行下列指令：

    ```
    kubectl get pods -n ibm-observe
    ```
    {: codeblock}

    當您看到一個以上 `sysdig-agent` pod 時，表示部署順利完成。`sysdig-agent` Pod 的數目與叢集裡工作者節點的數目相同。所有 Pod 都必須處於`執行中`狀態。


## 步驟 3. 啟動 Sysdig Web 使用者介面
{: #kubernetes_cluster_step3}

若要透過 {{site.data.keyword.cloud_notm}} 主控台啟動 Sysdig Web 使用者介面，請完成下列步驟。

每個瀏覽器只能開啟一個 Web 使用者介面階段作業。
{: imp}

1. [登入 {{site.data.keyword.cloud_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

	在使用您的使用者 ID 和密碼登入之後，即會開啟「{{site.data.keyword.cloud_notm}} 儀表板」。

2. 從功能表 ![外部鏈結圖示](../../../icons/icon_hamburger.svg "「功能表」圖示") 中，選取**觀察**。 

3. 選取**監視**。即會顯示 {{site.data.keyword.cloud_notm}} 上可用的實例清單。

4. 找到您的實例，並按一下**檢視 Sysdig**。

    * **首次使用**：因為您已經安裝了 Sysdig 代理程式，您可以跳過安裝精靈、開始使用，然後完成上線。
    
    * **後續使用**：將開啟**探索**視圖。


如果未順利安裝 Sysdig 代理程式、指向錯誤的汲取端點，或存取金鑰不正確，則開啟的頁面會通知您，下一步做什麼。

例如，如果未順利安裝 Sysdig 代理程式，則無法跳過安裝精靈。您可能看到與下列內容類似的訊息：
    
```
Waiting for the first node to connect... Go ahead and follow the instructions below.
```
{: screen}
    
您可以嘗試下列動作：
*  驗證您使用的是否為 `ingest` [端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)，而不是 Sysdig 端點。 
*  驗證[存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key)是否正確。
*  遵循任何其他指示，並重複本指導教學中的步驟。



## 步驟 4. 監視叢集
{: #kubernetes_cluster_step4}

可以在 Sysdig Web 使用者介面提供的**探索**視圖中監視叢集。此視圖是預設首頁，也是您對叢集基礎架構和資源進行疑難排解和監視的起點。

在*主機和容器* 區段中，可以查看*探索表*，這是叢集裡正在將度量值轉遞至監視實例的工作者節點清單。每一個工作者節點項目代表該工作者節點的相關基礎架構物件群組。

按一下**主機及容器** ![主機及容器](../images/switch_hosts.png) 來切換資料來源。然後，選取工作者節點。顯示的資料對應於您已選取的工作者節點。如果您按一下**回到探索表格**，則會顯示*探索表格*。 

**自訂_探索表_**

您可以自訂*探索表*。 

* 每一欄都會顯示不同的度量值。 
* 您可以個別配置每一個度量值。 
* 您可以變更直欄的順序。 

    請注意，若您對現有直欄的順序進行變更，則在您登入時，變更會在不同分組之間持續存在。如果新增或移除直欄，則該變更會持續存在。 

* 您也可以配置顏色，以強調顯示值並提高可讀性。 

例如，若要配置直欄的顏色編碼，請完成下列步驟：

1. 選取一個直欄。將滑鼠移至直欄標題上方。然後，選取鉛筆圖示。
2. 切換功能表列以啟用顏色編碼。
3. 設定不同臨界值。


**自訂儀表板**

若要檢視特定工作者節點的其他詳細資料，請按一下相應基礎架構項目，然後表格中將開啟*依主機的概觀* 儀表板。您可以按一下 ![切換儀表板](../images/switch_dashboards_1.png) 圖示來探索其他儀表板和度量值。請注意，您只能選取與所選工作者節點相關的度量值和儀表板。

若要回到完整的_探索表_，請按一下 **X（返回探索表）**按鈕。


如需相關資訊，請參閱 [Sysdig 文件](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822446/The+Explore+Table)。



## 後續步驟
{: #kubernetes_cluster_next_steps}

建立自訂儀表板。如需相關資訊，請參閱[使用儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)。

您也可以進一步瞭解警示。如需相關資訊，請參閱[使用警示](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。 






