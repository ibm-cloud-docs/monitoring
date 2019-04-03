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


# 授與使用者許可權
{: #grant_permissions}

在 {{site.data.keyword.Bluemix}} 中，您可以將一個以上的角色指派給使用者。這些角色定義針對該使用者啟用哪些作業來使用 {{site.data.keyword.monitoringshort}} 服務。
{:shortdesc}

若要授與使用者使用度量值的許可權，您必須新增該使用者的原則，說明此使用者可以對帳戶中的 {{site.data.keyword.monitoringshort}} 服務執行的動作。僅帳戶擁有者可以將個別原則指派給使用者。


## 透過 IBM Cloud 使用者介面為使用者指派 IAM 原則 
{: #assign_policy_ui}

完成下列步驟，以授與使用者使用 {{site.data.keyword.monitoringshort}} 服務的許可權：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://console.bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者*視窗會顯示目前已選取帳戶的使用者及其電子郵件位址清單。
	
3. 如果使用者是帳戶成員，請從清單中選取使用者名稱，或按一下*動作*功能表中的**管理使用者**。

    如果使用者不是帳戶的成員，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

4. 按一下**指派服務原則**。

5. 輸入原則的相關資訊。下表列出定義原則的必要或選用欄位： 

    <table>
	  <caption>配置 IAM 原則的欄位清單。</caption>
	  <tr>
	    <th>欄位</th>
		<th>值</th>
		<th>狀態</th>
	  </tr>
	  <tr>
	    <td>服務</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>必要</td>
	  </tr>
	  <tr>
	    <td>角色</td>
		<td>選取一個以上 IAM 角色。<br>有效角色包含：*管理者*、*操作員*、*編輯者*及*檢視者*。<br>如需每個角色容許的動作的相關資訊，請參閱 [IAM 角色](/docs/services/cloud-monitoring/security_ov.html#iam_roles)。</td>
		<td>必要</td>
	  </tr>
	  <tr>
	    <td>地區</td>
		<td>您可以指定將授與使用者存取權以使用度量值的地區。選取**指定選用的服務環境定義**。然後，個別新增一個以上地區，或選取**所有現行地區**來授與所有地區的存取權。</td>
		<td>選用</td>
	  </tr>
	</table>
	
6. 按一下**指派原則**。
	
配置的原則適用於選取的地區。 

## 使用指令行為使用者指派 IAM 原則
{: #assign_policy_commandline}

完成下列步驟，以使用指令行授與使用者檢視度量值的存取權：

1. （必要條件）安裝 {{site.data.keyword.Bluemix_notm}} CLI。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview)。
   
   如果已安裝 CLI，請繼續進行下一步。
	
2. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
	
3. 取得帳戶 ID。 

    執行下列指令，以取得帳戶 ID：

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	即會顯示含有其 GUID 的帳戶清單。
	
	匯出您計劃授與使用者許可權的帳戶 ID。配置 `$acct_id` 這類 Shell 變數，例如：
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. 取得您要授與許可權之使用者的 {{site.data.keyword.IBM_notm}} ID。

    1. 顯示與此帳戶相關聯的使用者。執行下列指令：
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. 取得使用者的 GUID。**附註：此步驟必須由您計劃授與許可權的使用者完成。**
	
	    例如，要求使用者執行下列指令以取得其使用者 ID：
		
		取得 IAM 記號。如需相關資訊，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli)。

        從 IAM 記號中前 2 兩個點之間的 IAM 記號中取得資料。將資料匯出至 Shell 變數，例如 `$user_data`。 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		例如，執行下列指令以取得使用者 ID。此指令在這個範例中使用 jq，將資訊解碼為 JSON 格式化文字：
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		執行此指令的輸出如下：
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		將使用者 ID（這是欄位 *id* 的值）傳送給帳戶擁有者。 
		
	3. 將使用者 ID 匯出至 Shell 變數，例如 `$user_ibm_id`。
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. 如果使用者還不是成員，請邀請使用者加入帳戶。如需相關資訊，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

    例如，執行下列指令以邀請使用者 xxx@yyy.com 加入帳戶 zzz@ggg.com：
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. 建立原則檔案名稱。 

    例如，使用下列範本來授與在「美國南部」地區的檢視許可權：
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	將原則檔案命名為：`policy.json`
	
5. 取得使用者 ID 的 IAM 記號。

    如需相關資訊，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli)。

    將 IAM 記號匯出至 `$iam_token` 這類 Shell 變數，例如：
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. 授與使用者使用 {{site.data.keyword.monitoringshort}} 服務的許可權。 

   執行下列 cURL 指令，以授與在「美國南部」地區的許可權：
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	執行下列 cURL 指令，以授與在「英國」地區的許可權：
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## 透過 IBM Cloud 使用者介面將 CF 角色授與使用者 
{: #grant_permissions_ui_space}


若要在空間網域或組織網域中使用度量值，使用者必須在 {{site.data.keyword.Bluemix_notm}} 中已獲指派 Cloud Foundry (CF) 角色。CF 角色說明使用者可以使用 {{site.data.keyword.monitoringshort}} 服務在空間或組織中執行的動作。 

完成下列步驟，以授與使用者使用 {{site.data.keyword.monitoringshort}} 服務的許可權：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者*視窗會顯示目前已選取帳戶的使用者及其電子郵件位址清單。
	
3. 如果使用者是帳戶成員，請從清單中選取使用者名稱，或按一下*動作*功能表中的**管理使用者**。

    如果使用者不是帳戶的成員，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

4. 按一下**指派組織**。

5. 輸入原則的相關資訊。下表列出定義原則的必要或選用欄位： 

    <table>
	  <caption>配置 CF 原則的欄位清單。</caption>
	  <tr>
	    <th>欄位</th>
		<th>值</th>
	  </tr>
	  <tr>
	    <td>組織</td>
		<td>從清單中選擇一個組織。</td>
	  </tr>
	  <tr>
	    <td>組織角色</td>
		<td>選取**無組織角色**。不過，如果使用者具有組織角色，請從清單中選擇一個組織角色。<br>有效值包含：**帳單管理員**、**審核員**、**管理員**</td>
	  </tr>
	  <tr>
	    <td>地區</td>
		<td>從清單中選擇一個地區。<br>有效值包含：**所有現行地區**、**美國南部**、**英國**</td>
	  </tr>
	  <tr>
	    <td>空間</td>
		<td>依預設，在*地區* 欄位設為**所有現行地區**時，會預先定義**所有現行空間**。若要授與個別空間的許可權，請選擇特定地區，然後從清單中選擇一個空間。</td>
	  </tr>
	  <tr>
	    <td>空間角色</td>
		<td>從清單中選擇一個空間角色。<br>有效值包含：**管理員**、**審核員**、**開發人員**及**無空間角色**。如需相關資訊，請參閱 [Cloud Foundry 角色](/docs/services/cloud-monitoring/security_ov.html#bmx_roles)。</td>
	  </tr>
	</table>
	
6. 按一下**指派原則**。
	
配置的原則適用於選取的地區。 


