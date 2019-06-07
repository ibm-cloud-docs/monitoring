---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# 自訂 Kubernetes Sysdig 代理程式
{: #change_kube_agent}

在 {{site.data.keyword.mon_full_notm}} 中，您可以自訂 Sysdig 代理程式配置來設定記載層次、封鎖埠、包括或排除度量值資料、新增或移除事件，以及過濾掉容器。
{:shortdesc}

若要自訂 Kubernetes Sysdig 代理程式，您可能需要配置下列任何檔案中的區段：

| 檔名                        | 動作       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | 修改記載層次。 |
| `sysdig-agent-configmap.yaml`    | 封鎖埠。 </br>包含或排除度量值資料。</br>新增或移除事件。</br>過濾掉容器。|
{: caption="表 1. Kubernetes Sysdig 代理程式配置檔" caption-side="top"} 

若要編輯 Kubernetes Sysdig 代理程式，您可能需要編輯 *sysdig-agent-configmap.yaml*、*sysdig-agent-daemonset-v2.yaml* 或兩者。
{: tip}

有兩種您可以用來修改配置檔的方法：
* 方法 1：直接在執行代理程式的叢集上修改檔案。
* 方法 2：在本端修改檔案，並將變更套用至叢集。

## 使用 kibectl edit 來編輯 Kubernetes Sysdig 代理程式配置
{: #change_kube_agent_edit_kube_agent_method1}

請完成下列步驟來編輯 Kubernetes Sysdig 代理程式配置：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    進行變更。**附註：**請參閱 `vi` 編輯器指示，以瞭解如何進行變更。

    儲存變更。會自動套用變更。 

3. 編輯 *sysdig-agent-daemonset-v2.yaml* 檔。 

    請執行下列指令： 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    進行變更。**附註：**請參閱 `vi` 編輯器指示，以瞭解如何進行變更。

    儲存變更。會自動套用變更。

## 使用 kibectl apply 來編輯 Kubernetes Sysdig 代理程式配置
{: #change_kube_agent_edit_kube_agent_method2}

如果您已在來源控制系統中儲存及管理配置 yaml 檔，請使用此方法。

請完成下列步驟來編輯 Kubernetes Sysdig 代理程式配置：

1. 從來源控制器取得每一個檔案的最新副本。 

    若要使用在叢集裡部署的配置來建立本端檔案，您也可以執行下列指令：
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    或 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. 編輯配置。

3. 使用下列指令來套用變更：

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    或
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

在 Kubernetes 跨叢集裡的所有節點推送變更之後，執行中代理程式會自動取得新配置。


## 將更多標籤新增至從 Kubernetes Sysdig 代理程式收集的資料
{: #change_kube_agent_add_tags}

請完成下列步驟，將更多標籤新增至您已部署的 Kubernetes Sysdig 代理程式配置：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。**附註：**請參閱 `vi` 編輯器指示，以瞭解如何進行變更。

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. 儲存變更。 

會自動套用變更。 

對於提供的範例，您將取得標籤 **agent.tag.cluster_version** 及 **agent.tag.region**。您可以使用它們來定義警示、自訂範圍等。



## 收集一組 Kubernetes 事件
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} 支援與 Kubernetes 進行事件整合。Sysdig 代理程式會自動探索這些服務，並從中收集事件資料。您可以編輯代理程式配置檔來變更其預設行為，以及包括或排除事件資料。 

依預設，只會收集有限的一組事件。如需依預設收集之事件的相關資訊，請參閱 [Kubernetes 事件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}。

若要新增或移除事件，您必須自訂 *sysdig-agent-configmap.yaml* 檔，並指定要包括哪些事件，以及要過濾掉哪些事件。**附註：***sysdig-agent-configmap.yaml* 中的區段項目會置換預設配置中的整個區段。
{: tip}

若要從 Kubernetes Pod 中過濾事件，請完成下列步驟：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *events* 區段或更新區段。

    **附註：**請參閱 `vi` 編輯器指示，以瞭解如何進行變更。

    例如，您可能想要收集 Kubernetes Pod 取回事件，並過濾掉其他依預設收集的 Pod 事件。您仍然想要收集節點和 replicationController 的預設 Kubernetes 事件。

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. 儲存變更。 

會自動套用變更。 


另一個您可以在其中查看如何收集 Kubernetes 事件子集的範例：您只想要監視 Pod 的取回中、已取回及失敗事件。

* 選項 1：將項目上的順序定義為項目符號清單：

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* 選項 2：在以方括弧括住的單一行上定義項目上的順序：

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

如需如何使用自訂事件的相關資訊，請參閱[使用自訂事件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}。


## 停用事件的收集
{: #change_kube_agent_disable_events}

若要停用 Sysdig 代理程式收集 Kubernetes 事件，請修改 *sysdig-agent-configmap.yaml* 檔。將 **events** 區段中的 **Kubernetes** 項目設為 *none*。 

請完成下列步驟：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *events* 區段或更新區段。

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. 儲存變更。 

會自動套用變更。 






## 包括及排除度量值
{: #change_kube_agent_inc_exc_metrics}

若要過濾自訂度量值，您必須自訂 *sysdig-agent-configmap.yaml* 檔中的 **metrics_filter** 區段。您可以配置 **include** 及 **exclude** 過濾參數，來指定要包括哪些度量值，以及要過濾掉哪些度量。

<p class="important">過濾規則順序設定如下：套用符合度量值的第一個規則。忽略該度量值的後續規則。</p>

請完成下列步驟：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *metrics_filter* 區段或更新區段。

    比方說，如果 Sysdig 代理程式的 *metrics_filter* 區段如下所示：

    ```
    metrics_filter:
      - include: metricA.*
      - exclude: metricA.*
      - include: metricB.*
      - include: haproxy.backend.*
      - exclude: haproxy.*
      - exclude: metricC.*
    ```
    {: screen}

    * 您正在配置 Sysdig 代理程式，從開頭為 *metricA*、*metricB* 及 *haproxy.backend* 的度量值中收集所有資料。 

    * 您正在過濾掉開頭為 *metricC* 的度量值，以及其他開頭為 *haproxy* 的度量值。 

    * 忽略 `exclude: metricA.*` 項目。

4. 儲存變更。 

會自動套用變更。 




## 過濾從中收集資料的 kubernetes 物件及容器
{: #change_kube_agent_filter_data}

Kubernetes Sysdig 代理程式會自動從叢集中偵測到的*所有容器* 收集度量值，包括 Prometheus、StatsD、JMX、app-checks 及內建度量值。
 
您可以自訂 Sysdig 代理程式，從度量值集合排除容器。 

排除容器時，請考量下列資訊：
* 您可以減少代理程式和後端負載。
* 您只會從要監視的容器中收集資料。
* 您可以透過報告重要容器，以及過濾掉不必要或不重要的容器來控制成本。

若要啟用 Sysdig 代理程式過濾器容器的特性，您必須自訂 *sysdig-agent-configmap.yaml* 檔。將 **containers** 區段中的 **use_container_filter** 項目設為 *true*。**附註：**預設會關閉此特性。然後，定義包含一個以上的條件且您要套用的規則。

下表概述您可以定義以在叢集裡設定過濾規則的參數：

| 參數                          | 條件                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | 容器映像檔名稱                           |
| `container.name`                   | 容器名稱                                 |
| `container.label.*`                | 容器標籤                                |
| `kubernetes.object.*`            | Kubernetes 物件。物件可以是 Pod、名稱空間等。   |
| `kubernetes.object.annotation.*` | Kubernetes 物件註釋                   |
| `kubernetes.object.label.*`      | Kubernetes 物件標籤                        |
| `all`                              | 用來指定所有物件的預設規則            |
{: caption="表 2. 用來在容器上定義條件的參數" caption-side="top"} 

請考量下列資訊，以瞭解 Sysdig 代理程式如何套用您已在 **container_filter** 區段中定義的規則：
* 您可以定義條件，方法為使用 **include** 及 **exclude** 過濾參數來配置它們。 
* 清單中的第一個相符規則決定包括還是排除容器。
* 條件由索引鍵名稱及值組成。如果容器的給定索引鍵符合該值，則會套用規則。
* 當一個規則包含多個條件時，需要符合`所有條件`，才能套用規則。

請完成下列步驟，以過濾掉叢集裡 Sysdig 代理程式監視的容器：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *metrics_filter* 區段或更新區段。

    例如，請參閱配置對映的下列摘要：

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. 儲存變更。 

會自動套用變更。 


## 封鎖埠
{: #change_kube_agent_block_ports}

若要封鎖來自網路埠的網路資料流量及度量值，您必須自訂 *sysdig-agent-configmap.yaml* 檔案中的 **blacklited_ports** 區段。您必須列出要從中過濾掉任何資料的埠。

**附註：**埠 53 (DNS) 一律列入黑名單。 

請完成下列步驟：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-configmap.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *metrics_filter* 區段或更新區段。

    例如，下列範例顯示如何設定 Sysdig 代理程式的 *blackted_ports* 區段，以排除來自埠 6666 及 6379 的資料：

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. 儲存變更。 

會自動套用變更。 



## 變更記載層次
{: #change_kube_agent_log_level}

若要配置記載層次，您必須自訂 *sysdig-agent-daemonset-v2.yaml* 檔中的 **log** 區段。 

Sysdig 代理程式會在 */opt/draios/logs/draios.log* 中產生日誌項目。 
* 日誌檔在大小達到 10MB 時即會替換。
* 保留 10 個最近的日誌檔。附加至檔名的日期戳記是用來決定要保留哪些檔案。
* 有效的記載層次為：*none*、*error*、*warning*、*info*、*debug*、*trace*
* 預設記載層次為 *info*，其中除了任何警告及錯誤的項目外，每次將聚集的度量值傳輸至後端伺服器時都會建立一個項目，每秒一次。
* 您可以自訂日誌類型，以及藉由配置 Sysdig 代理程式配置檔 **/opt/draios/etc/dragent.yaml** 所收集的項目。在編輯檔案之後，必須使用 `service dragent restart` 在 Shell 上重新啟動代理程式，才能啟動變更。

下表列出一些常用的情境，以及您必須在其中每一個情境中設定的值：

| 使用案例                                     | 日誌區段項目           |
|-----------------------------------------------|-----------------------------|
| 疑難排解代理程式行為                   | `file_priority: debug`      |
| 減少容器主控台輸出               | `console_priority: warning` |
| 依嚴重性過濾事件                  | `event_priority: warning`   |
| 驗證包括或排除哪些度量值  | `metrics_excess_log: true`  |
{: caption="表 2. 日誌區段項目" caption-side="top"} 

請完成下列步驟來配置記載層次：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-daemonset-v2.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *log* 區段或更新區段。

    例如，若要過濾掉低嚴重性事件（*notice*、*information*、*debug*），您必須將 **log** 區段中的 **metrics_excess_log** 項目設為 *true*：

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. 儲存變更。 

會自動套用變更。 


## 依嚴重性過濾 Kubernetes 事件
{: #change_kube_agent_filterby_severity}

若要依嚴重性過濾事件，您必須修改 *sysdig-agent-daemonset-v2.yaml* 檔。將 **log** 區段中的 **event_priority** 項目設為 *none*。 

預設記載層次為 **information**。這表示只會傳輸警告及更高的嚴重性事件。

有效層次為：*emergency*、*alert*、*critical*、*error*、*warning*、*notice*、*information*、*debug* 及 *none*。**附註**：從高優先順序至低優先順序列出這些值。

請完成下列步驟：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-daemonset-v2.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *log* 區段或更新區段。

    例如，若要過濾掉低嚴重性事件（*notice*、*information*、*debug*），您必須將日誌區段 **event_priority** 設為 *warning*：

    ```
    log:
      event_priority: warning
    ```
    {: codeblock}

6. 儲存變更。 

會自動套用變更。 

## 將包括或排除哪些度量值記載至檔案
{: #change_kube_agent_log_metrics}

若要將包括哪些自訂度量值及排除哪些自訂度量值的相關資訊記載至檔案，您必須自訂 *sysdig-agent-daemonset-v2.yaml* 檔。將 **log** 區段中的 **metrics_excess_log** 項目設為 **true**。

* 依預設，已停用記載。 
* 每隔 30 秒會在 INFO 層次進行記載，並持續 10 秒。 
* 日誌檔位於 */opt/draios/logs/draios.log*。
* 記載資料的格式如下：

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* 是一個符號，指出包括還是排除度量值。加號 (*+*) 指出包括度量值。減號 (*-*) 指出排除度量值。 

    * *[type]* 指定度量值類型，例如 *statsd*。
    
    * *[metric included/excluded]* 以人類可讀的方式指出包括還是排除度量值。

    *  *metric.name* 指出度量值名稱。

    * *(filter: +/-[metric.filter])* 提供 *sysdig-agent-daemonset-v2.yaml* 檔中 **metrics_filter** 區段中所定義之任何過濾器的相關資訊。

範例項目如下所示：

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

請完成下列步驟：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

2. 編輯 *sysdig-agent-daemonset-v2.yaml* 檔。 

    請執行下列指令：

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 進行變更。新增 *log* 區段或更新區段。

    例如，若要過濾掉低嚴重性事件（*notice*、*information*、*debug*），您必須將 **log** 區段中的 **metrics_excess_log** 項目設為 *true*：

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. 儲存變更。 

會自動套用變更。 


## 範例 configmap yaml 檔案
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter: 
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## 範例 daemonset yaml 檔案
{: #change_kube_agent_sample_daemonset}

```
 Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

