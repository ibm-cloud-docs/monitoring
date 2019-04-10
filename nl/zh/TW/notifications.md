---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# 使用通知頻道
{: #notifications}

配置觸發警示時要通知的通知頻道。您可以透過 Web 使用者介面中的*設定* 畫面來管理通知頻道。
{:shortdesc}
 

## 配置通知頻道
{: #notifications_create}

請完成下列步驟來新增通知頻道：

1. 啟動 Web 使用者介面。如需如何啟動 Web 使用者介面的相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 從導覽列的*選取器* 按鈕中，選擇**設定**。

3. 選取**通知頻道**。

4. 按一下**我的頻道** ![新增圖示](../images/add.png)。然後，選取頻道。

    **附註：**第一次配置通知頻道時，請按一下任一頻道。

5. 配置通知頻道：

    * 輸入頻道的名稱。

    * 啟用*正常時通知* 欄位，以在不再觸發警示條件時接收通知。

    * 啟用*解決時通知* 條件，以在使用者手動解決警示時接收通知。

    * 若為**電子郵件**通知頻道，新增收件者的清單，以逗點區隔。

    * 若為 **slack** 通知頻道，新增 *Slack 頻道* 的名稱。

    * 若為 **Webhook** 通知頻道，新增 *Webhook URL*。**附註：**觸發警示時，通知會以 JSON 格式的「貼文」傳送至 Webhook 端點。如需相關資訊，請參閱[配置 Webhook 頻道 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}。例如，可以使用自訂 Webhook 將 Sysdig 與 ServiceNow 整合。若要瞭解如何使用 ServiceNow 來配置 Sysdig，請參閱[配置 ServiceNow ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}。

    * 若為 **VictorOps** 通知頻道，新增*API 金鑰* 及*遞送金鑰*。

    * 若為 **OpsGenie** 通知頻道，新增*OpsGenie API 金鑰*。請注意，您必須在 OpsGenie 中配置與 Sysdig 的整合。如需相關資訊，請參閱[在 Opsgenie 中新增 Sysdig Cloud Integration ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}。

    * 若為 **PagerDuty** 通知頻道，您必須先授權 Sysdig 與您的帳戶整合。選取 PagerDuty 時，會開啟一個精靈來配置與 Sysdig 的整合。按一下**授權整合**或**使用身分提供者登入**來授權 PagerDuty。選擇現有服務或針對 Sysdig 通知設定新服務，然後按一下**完成整合**。選取要用於 Sysdig 突發事件的呈報原則。然後，在*通知* 標籤上，確認 PagerDuty 帳戶、服務名稱及服務金鑰。 

    * 對於容許測試的整合，可以選擇性地啟用*測試通知* 條件，來接收測試通知。如果在 10 分鐘內未收到測試通知，請檢閱您的頻道配置。 

6. 按一下**建立頻道**。 



## 修改通知頻道
{: #notifications_update}

請完成下列步驟來修改通知頻道：

1. 啟動 Web 使用者介面。如需如何啟動 Web 使用者介面的相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 從導覽列的*選取器* 按鈕中，選擇**設定**。

3. 選取**通知頻道**。

4. 識別您要修改的目標頻道，然後按一下**編輯**。

5. 在進行變更之後，請按一下**儲存變更**。



## 測試通知頻道
{: #notifications_test}

請完成下列步驟來測試通知頻道：

1. 啟動 Web 使用者介面。如需如何啟動 Web 使用者介面的相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 從導覽列的*選取器* 按鈕中，選擇**設定**。

3. 選取**通知頻道**。

4. 識別您要修改的目標頻道，然後按一下**測試**。



## 停用通知頻道
{: #notifications_disable}

請完成下列步驟來停用通知頻道：

1. 啟動 Web 使用者介面。如需如何啟動 Web 使用者介面的相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 從導覽列的*選取器* 按鈕中，選擇**設定**。

3. 選取**通知頻道**。

4. 在*通知* 區段中，啟用*關閉時間* 來暫時停用警示，並將所有通知靜音。

## 刪除通知頻道
{: #notifications_delete}

請完成下列步驟來刪除通知頻道：

1. 啟動 Web 使用者介面。如需如何啟動 Web 使用者介面的相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 從導覽列的*選取器* 按鈕中，選擇**設定**。

3. 選取**通知頻道**。

4. 識別您要修改的目標頻道，然後按一下**編輯**。

5. 按一下**刪除頻道**。

6. 確認刪除頻道。按一下**儲存變更**。




