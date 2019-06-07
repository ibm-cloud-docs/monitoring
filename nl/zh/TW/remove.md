---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# 移除實例
{: #remove}

您可以從 {{site.data.keyword.Bluemix}} 使用者介面或透過指令行移除 {{site.data.keyword.mon_full_notm}} 服務的實例。
{:shortdesc}

從 {{site.data.keyword.cloud_notm}} 移除實例時，請考量下列資訊來開始：

1. 寫下要將度量值轉遞至您要移除之 {{site.data.keyword.mon_full_notm}} 實例的來源清單。您必須從每一個來源中移除 Sysdig 代理程式。
2. 移除授與使用者以使用該實例的許可權。 

    如果您使用存取群組來管理存取實例的許可權，則必須移除存取群組。

    如果您使用存取群組來管理存取不同服務實例的許可權，則必須移除授與您要移除之實例許可權的原則。
    
    如果您已將個別原則授與使用者，則必須收集具有存取權之每一個使用者的資訊。然後逐一移除與要刪除之實例相關的原則。


然後，從「{{site.data.keyword.cloud_notm}} 儀表板」刪除實例。


## 透過 {{site.data.keyword.cloud_notm}} 使用者介面移除實例
{: #remove_ui}

若要使用 {{site.data.keyword.cloud_notm}} 使用者介面移除 {{site.data.keyword.mon_full_notm}} 的實例，請完成下列步驟：

1. [登入 {{site.data.keyword.cloud_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}。

	在使用您的使用者 ID 和密碼登入之後，即會開啟 {{site.data.keyword.cloud_notm}} 使用者介面。

2. 選取**觀察**。 

3. 選取**監視**。即會顯示實例的清單。

4. 選取您要刪除的實例。

5. 從*動作* 功能表中，選取**移除**。


## 透過 CLI 移除實例
{: #remove_cli}

若要透過指令行移除 {{site.data.keyword.mon_full_notm}} 的實例，請完成下列步驟：

1. [必要條件] 安裝 {{site.data.keyword.cloud_notm}} CLI。如果已安裝 CLI，請繼續進行下一步。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

2. 登入 {{site.data.keyword.cloud_notm}} 中要佈建實例的地區。請執行下列指令：[`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. 設定佈建實例的資源群組。請執行下列指令：[`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    依預設，會設定 `default` 資源群組。

4. 移除實例。請執行 [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete) 指令：

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    其中 NAME 是實例的名稱

    例如，若要移除實例，請執行下列指令：

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
