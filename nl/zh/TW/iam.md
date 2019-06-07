---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# 管理 {{site.data.keyword.cloud_notm}} 中的使用者存取權
{: #iam}

{{site.data.keyword.iamlong}} (IAM) 可讓您在 {{site.data.keyword.cloud_notm}} 中，安全地鑑別使用者以及一致地控制對所有雲端資源的存取。
{:shortdesc}

**必須將已定義 IAM 使用者角色的存取原則，指派給在您帳戶中存取 {{site.data.keyword.mon_full_notm}} 服務的每位使用者。**原則決定使用者可以在您所選服務或實例的環境定義中執行什麼動作。容許的動作已經過自訂，且定義為容許對服務執行的作業。然後，這些動作會對映至 IAM 使用者角色。

*原則* 可讓您在不同層次上授與存取權。部分選項包括下列各項： 

* 對您帳戶中所有已啟用 IAM 功能之服務的存取權
* 在您帳戶的單一地區中，跨所有服務實例的存取權
* 對您帳戶中個別服務實例的存取權
* 對資源群組環境定義內所有服務實例的存取權
* 對資源群組環境定義內單一地區中所有服務實例的存取權
* 對資源群組環境定義內所有已啟用 IAM 功能之服務的存取權

*角色* 定義使用者或 serviceID 可以執行的動作。{{site.data.keyword.cloud_notm}} 中有不同類型的角色：
* *平台管理角色* 可讓使用者在平台層次對服務資源執行作業，例如，將服務的存取權指派給使用者、建立或刪除服務 ID、建立實例、將服務的原則指派給其他使用者，以及將實例連結至應用程式。
* *服務存取角色* 可將各種許可權層次指派給使用者，以呼叫服務的 API。

**若要將一組使用者和服務 ID 組織成單一實體，讓您可以輕鬆管理 IAM 許可權，請使用**存取群組*。** 您可以將單一原則指派給群組，而不是每個個別使用者或服務 ID 多次指派相同的存取權。
{: tip}


## 使用存取群組來管理存取權
{: #iam_groups}

若要使用存取群組來管理存取權或指派使用者的新存取權，您必須是帳戶擁有者、帳戶中所有已啟用「身分及存取」之服務上的管理者或編輯者，或是針對「IAM 存取群組服務」指派的管理者或編輯者。 

選擇下列任何動作來管理 {{site.data.keyword.cloud_notm}} 中的存取群組：

* [建立存取群組](/docs/iam?topic=iam-groups#create_ag)。
* [指派群組的存取權](/docs/iam?topic=iam-groups#access_ag)。


## 將原則直接指派給使用者來管理存取權
{: #iam_users}

若要透過使用 IAM 原則來管理存取權或指派使用者的新存取權，您必須是帳戶擁有者、帳戶中所有服務的管理者，或特定服務或服務實例的管理者。 

選擇下列任何動作來管理 {{site.data.keyword.cloud_notm}} 中的 IAM 原則：

* 若要修改使用者的許可權，請參閱[編輯現有的存取權](/docs/iam?topic=iam-iammanidaccser#edit_existing)。
* 若要將許可權授與使用者，請參閱[指派新的存取權](/docs/iam?topic=iam-iammanidaccser#assign_new_access)。
* 若要撤銷許可權，請參閱[移除存取權](/docs/iam?topic=iam-iammanidaccser#removing_access)。
* 若要檢閱使用者的許可權，請參閱[檢閱您指派的存取權](/docs/iam?topic=iam-iammanidaccser#review_your_access)。


## {{site.data.keyword.cloud_notm}} 平台角色
{: #iam_platform}

使用下表來識別平台角色，您可以在 {{site.data.keyword.cloud_notm}} 中授與使用者這些角色，以執行下列任何平台動作：

| 平台動作                                                        | {{site.data.keyword.cloud_notm}} 平台角色    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `授與其他帳戶成員使用服務的存取權`           | 管理者                                        | 
| `佈建服務實例`                                          |管理者 </br>編輯者| 
| `刪除服務實例`                                             |管理者 </br>編輯者| 
| `建立服務 ID`                                                   |管理者 </br>編輯者|
| `檢視服務實例的詳細資料`                                    |管理者 </br>編輯者 </br>操作員 </br>檢視者| 
| `檢視「觀察監視」儀表板中的服務實例`      |管理者 </br>編輯者 </br>操作員 </br>檢視者| 
{: caption="表 1. IAM 使用者角色及動作" caption-side="top"}



## Sysdig 角色
{: #iam_sysdig_roles}

下表概述 Sysdig 角色及每個角色的動作：

| 動作                                                                    | Sysdig 角色                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `重設 Sysdig 存取金鑰`                                              | Admin                                                |
| `管理使用者`                                                             | Admin                                                |
| `建立、配置及刪除團隊`                                      | Admin                                                |
| `配置及移除通知頻道`                              | Admin                                                | 
| `配置及移除 Sysdig 代理程式`                                       | Admin                                                |
| `在 Sysdig Web 使用者介面中建立、刪除及編輯內容`                    | Admin </br>User                                      |  
| `透過 Sysdig Web 使用者介面檢視度量值`                                   | Admin </br>User                                      |  
| `建立及刪除警示`                                                 | Admin </br>User                                      | 
| `建立及刪除擷取`                                               | Admin </br>User                                      |   
{: caption="表 2. Sysdig 角色與動作" caption-side="top"}


## 將 Sysdig 角色對映至 {{site.data.keyword.cloud_notm}} 角色
{: #iam_sysdig}

請使用下表來查看 {{site.data.keyword.cloud_notm}} 角色如何對映至 Sysdig 角色：

| 角色類型        | 角色               | Sysdig 角色                | 說明                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| 平台角色       | 管理者      | Admin                      | 授與使用者 Sysdig 管理者專用權。   | 
| 服務角色        | 管理員            | Admin                      | 授與使用者 Sysdig 管理者專用權。   | 
| 服務角色        |撰寫者| User                       | 授與使用者 Sysdig 使用者專用權。   |
| 服務角色        | 讀者             |                            | 未授與任何許可權。                 |
{: caption="表 3. Sysdig 角色" caption-side="top"}


