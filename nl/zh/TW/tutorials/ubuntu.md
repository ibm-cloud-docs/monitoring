---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# 分析 Ubuntu 主機的度量值
{: #ubuntu}

使用此指導教學，可以瞭解如何配置 Ubuntu 主機，以將度量值轉遞至 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.mon_full_notm}} 服務。
{:shortdesc}

若要配置 Ubuntu 伺服器以轉遞度量值，您必須安裝 Sysdig 代理程式。此代理程式會使用存取金鑰（記號），透過 {{site.data.keyword.mon_full_notm}} 實例進行鑑別。Sysdig 代理程式會充當資料收集器。它會自動收集度量值。

您可以透過 Sysdig 的 Web 型使用者介面來檢視度量值。

![元件概觀，關於 {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "元件概觀，關於 {{site.data.keyword.cloud_notm}}")



## 開始之前
{: #ubuntu_prereqs}

在美國南部地區工作。 

閱讀 {{site.data.keyword.mon_full_notm}} 的相關資訊。如需相關資訊，請參閱[關於](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)。

使用身為成員或是 {{site.data.keyword.cloud_notm}} 帳戶擁有者的使用者 ID。若要取得 {{site.data.keyword.cloud_notm}} 使用者 ID，請移至[登錄 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

您的 {{site.data.keyword.IBM_notm}} ID 必須已獲指派下列每一個資源的 IAM 原則： 

| 資源                             | 存取原則的範圍 | 角色    | 地區    | 資訊                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| 資源群組 **Default**           |  資源群組            | 檢視者  | `Us-south`  | 需要此原則，以容許使用者查看 Default 資源群組中的服務實例。|
| {{site.data.keyword.mon_full_notm}} 服務 |  資源群組            | 編輯者  | `Us-south`  | 需要此原則，以容許使用者在 Default 資源群組中佈建及管理 {{site.data.keyword.mon_full_notm}} 服務。|
{: caption="表 1. 完成指導教學所需的 IAM 原則清單" caption-side="top"} 

安裝 {{site.data.keyword.cloud_notm}} CLI。如需相關資訊，請參閱[安裝 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。


## 步驟 1. 佈建 {{site.data.keyword.mon_full_notm}} 實例
{: #ubuntu_step1}

若要透過 {{site.data.keyword.cloud_notm}} 使用者介面佈建 {{site.data.keyword.mon_full_notm}} 的實例，請完成下列步驟：

1. [登入 {{site.data.keyword.cloud_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

	在使用您的使用者 ID 和密碼登入之後，即會開啟 {{site.data.keyword.cloud_notm}} 使用者介面。

2. 按一下**型錄**。即會開啟 {{site.data.keyword.cloud_notm}} 中可用的服務清單。

3. 若要過濾顯示的服務清單，請選取**開發人員工具**種類。

4. 按一下 **{{site.data.keyword.mon_full_notm}}** 磚。即會開啟*觀察* 儀表板。

5. 選取**建立案例**。 

6. 輸入服務實例的名稱。

7. 選取 **Default** 資源群組。 

    依預設，會設定 **Default** 資源群組。

8. 選取**精簡**服務方案。 

    依預設，會設定**精簡**方案。

    如需其他服務方案的相關資訊，請參閱[定價方案](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

9. 若要在您登入的 {{site.data.keyword.cloud_notm}} 資源群組中佈建 {{site.data.keyword.mon_full_notm}} 服務，請按一下**建立**。

在佈建實例之後，即會開啟*觀察* 儀表板。 


**附註：**若要透過 CLI 佈建實例，請參閱[透過 {{site.data.keyword.cloud_notm}} CLI 佈建實例](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)。


## 步驟 2. 配置 Ubuntu 伺服器以將度量值傳送到實例
{: #ubuntu_step2}

若要配置 Ubuntu 伺服器以將度量值轉遞至 {{site.data.keyword.mon_full_notm}} 實例，您必須安裝 Sysdig 代理程式。 

請從指令行完成下列步驟：

1. 開啟終端機。然後，登入 {{site.data.keyword.cloud_notm}}。請執行下列指令，並遵循提示：

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    選取 {{site.data.keyword.mon_full_notm}} 實例可用的帳戶。

2. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

3. 取得汲取 URL。如需相關資訊，請參閱 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

4. 部署 Sysdig 代理程式。請執行下列指令：

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是實例的汲取金鑰。

    * COLLECTOR_ENDPOINT 是可以使用監視實例之地區的汲取 URL。

    * TAG_DATA 是以逗點區隔的標籤，其格式為 *TAG_NAME:TAG_VALUE*。您可以使一個以上的標籤與 Sysdig 代理程式產生關聯。例如 *role:serviceX,location:us-south*。稍後，您可以使用這些標籤，從執行代理程式的環境識別度量值。

    * 將 **sysdig_capture_enabled** 設為 *false*，以停用 Sysdig 擷取特性。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

如果 Sysdig 代理程式無法正確安裝，請手動安裝核心標頭。選擇發行套件，並執行該發行套件的指令。然後，重試部署 Sysdig 代理程式。

* **若為 Debian 及 Ubuntu Linux 發行套件**，請執行下列指令：

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **若為 RHEL、CentOS 及 Fedora Linux 發行套件**，請執行下列指令：

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## 步驟 3. 啟動 Sysdig Web 使用者介面
{: #ubuntu_step3}

請完成下列步驟來啟動 Web 使用者介面：

1. [登入 {{site.data.keyword.cloud_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

	在使用您的使用者 ID 和密碼登入之後，即會開啟「{{site.data.keyword.cloud_notm}} 儀表板」。

2. 在導覽功能表中，選取**觀察**。 

3. 選取**監視**。 

    即會顯示 {{site.data.keyword.cloud_notm}} 上可用的實例清單。

4. 選取您的實例。然後，按一下**檢視 Sysdig**。

如果已順利配置 Sysdig 代理程式，則會開啟*探索* 視圖。

不過，如果未順利安裝 Sysdig 代理程式、指向錯誤的汲取端點，或存取金鑰不正確，則開啟的頁面會通知您，下一步做什麼。

每個瀏覽器只能開啟一個 Web 使用者介面階段作業。
{: tip}


## 步驟 4. 監視 Ubuntu 伺服器
{: #ubuntu_step4}

您可以在透過 Web 使用者介面使用的**探索**視圖中監視 Ubuntu 伺服器。此視圖是疑難排解及監視基礎架構的起點。它是使用者 Web 使用者介面的預設首頁。

在*主機及容器* 區段中，您可以找到 Ubuntu 伺服器的項目。按一下**主機及容器** ![主機及容器](../images/switch_hosts.png) 來切換資料來源。然後，選取您的 Ubuntu 伺服器。顯示的資料對應於所選取的 Ubuntu 伺服器。

例如，若要配置直欄的顏色編碼，請完成下列步驟：

1. 選取一個直欄。將滑鼠移至直欄標題上方。然後，選取鉛筆圖示。
2. 切換功能表列以啟用顏色編碼。
3. 設定不同臨界值。



## 後續步驟
{: #ubuntu_next_steps}

建立自訂儀表板。如需相關資訊，請參閱[使用儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)。

您也可以進一步瞭解警示。如需相關資訊，請參閱[使用警示](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。 






