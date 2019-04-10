---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# 使用存取金鑰
{: #access_key}

**存取金鑰**是一個記號，您必須將其用來配置 Sysdig 代理程式，才能順利將資料轉遞至 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.mon_full_notm}} 實例。   
{:shortdesc}


## 透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰
{: #access_key_ibm_cloud_ui}

若要透過 {{site.data.keyword.cloud_notm}} 使用者介面取得 {{site.data.keyword.mon_full_notm}} 實例的存取金鑰，請完成下列步驟：

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶。

    按一下 [{{site.data.keyword.cloud_notm}} 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/login){:new_window}，以啟動 {{site.data.keyword.cloud_notm}} 儀表板。

	使用您的使用者 ID 和密碼登入之後，即會開啟 {{site.data.keyword.cloud_notm}} 使用者介面。

2. 在導覽功能表中，選取**觀察**。 

3. 選取**監視**。即會開啟 {{site.data.keyword.mon_full_notm}} 儀表板。您可以看到清單，列出 {{site.data.keyword.cloud_notm}} 上可用的監視實例。

3. 識別您要取得其存取金鑰的實例，然後按一下**檢視存取金鑰**。

4. 即會開啟蹦現視窗，您可以在其中按一下**顯示**來檢視存取金鑰。



## 透過 CLI 取得存取金鑰
{: #access_key_cli}

若要透過指令行取得 Sysdig 實例的存取金鑰，請完成下列步驟：

1. [必要條件] 安裝 {{site.data.keyword.cloud_notm}} CLI。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

   如果已安裝 CLI，請繼續進行下一步。

2. 登入 {{site.data.keyword.cloud_notm}} 中執行 Sysdig 實例的地區。執行下列指令：[`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. 設定執行 Sysdig 實例的資源群組。執行下列指令：[`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    依預設，會設定 `default` 資源群組。

4. 取得實例名稱。執行下列指令：[`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. 取得與 Sysdig 實例相關聯的 API 金鑰名稱。執行 [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) 指令：

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    其中 INSTANCE_NAME 是您在前一個步驟中取得的實例名稱。

6. 取得存取金鑰。執行 [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) 指令：

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    其中 APIKEY_NAME 是 API 金鑰的名稱。
 
    此指令的輸出包括 **Sysdig 存取金鑰**欄位，其中包含實例的存取金鑰。


例如，下列指令顯示範例服務 ID 的輸出：

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## 重設存取金鑰 
{: #access_key_reset}

如果存取金鑰已遭洩露，或者您有原則可以在幾天之後更新該金鑰，則可以產生新的金鑰並刪除舊金鑰。

若要更新 {{site.data.keyword.mon_full_notm}} 實例的存取金鑰，請完成下列步驟：

1. 啟動 {{site.data.keyword.mon_full_notm}} Web 使用者介面。如需相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。

2. 從導覽列的*選取器* 按鈕中，選擇**設定**。

2. 在*密碼管理* 區段中，按一下**重設您的密碼**。

**附註：**在重設 Sysdig 存取金鑰之後，對於任何已配置為將度量轉遞至此 {{site.data.keyword.mon_full_notm}} 實例的日誌來源，您必須更新其存取金鑰。
