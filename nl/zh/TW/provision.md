---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# 佈建實例
{: #provision}

在可以使用 Sysdig 來監視及管理度量之前，您必須先在 {{site.data.keyword.Bluemix}} 佈建服務的實例。
{:shortdesc}

若要在「公用雲端」地區中佈建 Sysdig 實例，您必須選取與該實例相關聯的服務方案、收集度量的地區，以及決定您可以監視之度量數及其保留期的方案。



## 從型錄佈建 Sysdig 實例
{: #provision_ui}

若要從 {{site.data.keyword.cloud_notm}} 型錄佈建 Sysdig 的實例，請完成下列步驟：

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶。

    按一下 [{{site.data.keyword.cloud_notm}} 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}，以啟動 {{site.data.keyword.cloud_notm}} 儀表板。

	在使用您的使用者 ID 和密碼登入之後，即會開啟 {{site.data.keyword.cloud_notm}} 使用者介面。

2. 按一下**型錄**。即會開啟 {{site.data.keyword.cloud_notm}} 上可用的服務清單。

3. 若要過濾顯示的服務清單，請選取**開發人員工具**種類。

4. 按一下 **{{site.data.keyword.mon_full_notm}}** 磚。即會開啟*觀察* 儀表板。

5. 選取**建立案例**。 

6. 選取服務方案。依預設，會設定**試用**方案。

    如需服務方案的相關資訊，請參閱[服務方案](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

7. 選取資源群組。依預設，會設定 **Default** 資源群組。

8. 按一下**建立**。

在佈建實例之後， 

* 即會開啟*觀察* 儀表板。 
* 即會自動建立服務 ID。您可以使用此服務 ID 來取得實例的 Sysdig 存取金鑰。

接著，新增 Sysdig 代理程式來配置度量來源。此代理程式負責收集度量，並將其轉遞至 Sysdig。 



## 透過 CLI 佈建 Sysdig 實例
{: #provision_cli}

若要透過指令行佈建 Sysdig 的實例，請完成下列步驟：

1. [必要條件] 安裝 {{site.data.keyword.cloud_notm}} CLI。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

   如果已安裝 CLI，請繼續進行下一步。

2. 登入 {{site.data.keyword.cloud_notm}} 中要佈建實例的地區。請執行下列指令：[`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. 設定您要佈建實例的資源群組。請執行下列指令：[`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    依預設，會設定 `default` 資源群組。

4. 建立 Sysdig 實例。請執行 [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) 指令：

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    其中

    * NAME 是 Sysdig 實例的名稱
    
    * *sysdig-monitor* 是 {{site.data.keyword.cloud_notm}} 中 {{site.data.keyword.mon_full_notm}} 服務的名稱
    
    * SERVICE_PLAN_NAME 是方案的類型。有效值為：*lite*、*graduated-tier*
    
    * LOCATION 是建立實例的地區

    例如，若要使用付款方案來佈建實例，請執行下列指令：

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

