---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# 導覽至 Web 使用者介面
{: #launch}

在 {{site.data.keyword.Bluemix}} 中佈建 {{site.data.keyword.mon_full_notm}} 服務的實例，並為度量來源配置 Sysdig 代理程式之後，您可以透過 {{site.data.keyword.mon_full_notm}} Web 使用者介面來檢視、監視及管理度量。{:shortdesc}


## 將 IAM 原則授與使用者以檢視資料 
{: #launch_step1}

**附註：**您必須是 {{site.data.keyword.mon_full_notm}} 服務的管理者、{{site.data.keyword.mon_full_notm}} 實例的管理者，或具有帳戶 IAM 許可權，才能將原則授與其他使用者。

下表列出使用者必須擁有才能啟動 {{site.data.keyword.mon_full_notm}} Web 使用者介面及檢視資料的最低原則：

| 服務                        | 角色                      | 授與的許可權     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | 平台角色：檢視者     | 容許使用者在「觀察監視」儀表板中檢視服務實例的清單。|
| `{{site.data.keyword.mon_full_notm}}` | 服務角色：作者      | 容許使用者啟動 Web 使用者介面，並在 Web 使用者介面中檢視度量。|
{: caption="表 1. IAM 原則" caption-side="top"} 

如需如何為使用者配置這些原則的相關資訊，請參閱[將許可權授與使用者以檢視度量](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig)。


## 透過 {{site.data.keyword.cloud_notm}} 使用者介面啟動 Web 使用者介面
{: #launch_step2}

您可以從 {{site.data.keyword.cloud_notm}} 使用者介面，在 {{site.data.keyword.mon_full_notm}} 實例的環境定義內啟動 Web 使用者介面。 

請完成下列步驟來啟動 Web 使用者介面：

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶。

    按一下 [{{site.data.keyword.cloud_notm}} 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}，以啟動 {{site.data.keyword.cloud_notm}} 儀表板。

	在使用您的使用者 ID 和密碼登入之後，即會開啟「{{site.data.keyword.cloud_notm}} 儀表板」。

2. 在導覽功能表中，選取**觀察**。 

3. 選取**監視**。 

    即會顯示 {{site.data.keyword.cloud_notm}} 上可用的實例清單。

4. 選取一個實例。然後，按一下**檢視 Sysdig**。

即會開啟 Web 使用者介面。


