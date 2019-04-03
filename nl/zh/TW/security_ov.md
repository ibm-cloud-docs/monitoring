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


# 安全
{: #security_ov}

若要控制容許使用者執行的 {{site.data.keyword.monitoringshort}} 服務動作，您可以將一個以上角色指派給使用者。若要鑑別使用者以使用度量值及警示，您可以使用 UAA 記號、IAM 記號或 API 金鑰。
{:shortdesc}





## 鑑別模型
{: #auth}

若要使用儲存在空間的 {{site.data.keyword.monitoringshort}} 服務中的度量值，您需要鑑別記號或 API 金鑰。 

若要取得安全記號，請參閱：

* [取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa)
* [取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)

若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。如果 API 金鑰外洩，您可以藉由刪除它來加以撤銷。然後，您可以重建新的金鑰。如需相關資訊，請參閱[使用 {{site.data.keyword.Bluemix_notm}} 使用者介面撤銷 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#revoke_ui)。 

UAA 記號和 IAM 記號會在一段時間後到期。API 金鑰不會到期。
 

下表列出每一種網域類型支援的安全模型：

<table>
  <caption>表 1. 每一個網域支援的安全模型</caption>
  <tr>
    <th></th>
	<th align="right">帳戶</th>
    <th align="right">組織</th>
    <th align="right">空間</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">否</td>
	<td align="center">是</td>
	<td align="center">是</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">是</td>
	<td align="center">是</td>
	<td align="center">是</td>
  </tr>
</table>

{{site.data.keyword.monitoringshort}} 服務會使用 IAM 存取控制特性，控管使用者或服務可對網域執行哪些動作或作業。例如，您可以定義一個 IAM 原則，容許使用者針對網域傳送及建立儀表板，但不容許從網域擷取度量值。



## Cloud Foundry 角色
{: #bmx_roles}

下表列出每一個 Cloud Foundry 角色使用 {{site.data.keyword.monitoringshort}} 服務的專用權：

<table>
  <caption>表 2. 使用 {{site.data.keyword.monitoringshort}} 服務的 Cloud Foundry 角色及專用權。</caption>
  <tr>
    <th>角色</th>
	<th>網域</th>
	<th>存取權</th>
  </tr>
  <tr>
    <td>管理員</td>
	<td>組織<br>空間</td>
	<td>所有 RESTful API</td>
  </tr>
  <tr>
    <td>開發人員</td>
	<td>空間</td>
	<td>所有 RESTful API</td>
  </tr>
  <tr>
    <td>審核員</td>
	<td>組織<br>空間</td>
	<td>僅執行唯讀作業的 RESTful API，如查詢度量值。</td>
  </tr>
</table>

如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理 Cloud Foundry 存取](/docs/iam/mngcf.html#mngcf)。



## IAM 角色
{: #iam_roles}

下表列出在使用度量值時的 {{site.data.keyword.monitoringshort}} 服務動作，以及授與使用者執行下列作業之許可權的 IAM 角色：

<table>
  <caption>表 3. 使用度量值</caption>
  <tr>
	<th>動作</th>
	<th>IAM 角色</th>
  </tr>
  <tr>
    <td>將度量值傳送至網域</td>
	<td>管理者、編輯者、操作員</td>
  </tr>
  <tr>
    <td>擷取/查詢度量值</td>
	<td>管理者、編輯者、檢視者</td>
  </tr>
  <tr>
    <td>搜尋網域中的度量值</td>
	<td>管理者、編輯者</td>
  </tr>
</table>

下表列出在處理警示時的 {{site.data.keyword.monitoringshort}} 服務動作，以及授與使用者執行下列作業之許可權的 IAM 角色：

<table>
  <caption>表 4. 處理警示。</caption>
  <tr>
	<th>動作</th>
	<th>IAM 角色</th>
  </tr>
  <tr>
    <td>建立、編輯及刪除警示規則</td>
	<td>管理者、編輯者</td>
  </tr>
  <tr>
    <td>檢視警示</td>
	<td>管理者、編輯者、檢視者</td>
  </tr>
  <tr>
    <td>建立、編輯及刪除警示通知</td>
	<td>管理者、編輯者</td>
  </tr>
  <tr>
    <td>檢視通知</td>
	<td>管理者、編輯者、檢視者</td>
  </tr>
  <tr>
    <td>檢視觸發的警示歷程記錄</td>
	<td>管理者、編輯者、檢視者</td>
  </tr>
</table>

如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理 IAM 存取](/docs/iam/mngiam.html#iammanidaccser)。

