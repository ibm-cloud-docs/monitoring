---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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

# 配置 Sysdig 代理程式
{: #config_agent}

在 {{site.data.keyword.cloud_notm}} 中佈建 {{site.data.keyword.mon_full_notm}} 服務的實例之後，您必須在每一個要監視的環境中配置一個 Sysdig 代理程式。Sysdig 代理程式會自動收集及報告預先定義的度量。您可以配置要在每一個環境中監視的度量。
{:shortdesc}

您可以使一個以上的標籤與每一個 Sysdig 代理程式產生關聯。標籤是以逗點區隔的值，其格式為 **TAG_NAME:TAG_VALUE**。監視環境時，您可以使用這些標籤來識別代理程式中可用的度量。例如，您可以包括服務名稱及位置的相關資訊，以及此代理程式所收集的所有度量。
{: tip}

## 在 Linux 上配置 Sysdig 代理程式
{: #config_agent_linux}

請完成下列步驟，在 Linux 上配置 Sysdig 代理程式，以收集度量並將其轉遞至 {{site.data.keyword.mon_full_notm}} 服務的實例：

1. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 取得汲取 URL。如需相關資訊，請參閱 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 部署 Sysdig 代理程式。從終端機執行下列指令。

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是實例的汲取金鑰。

    * COLLECTOR_ENDPOINT 是可以使用監視實例之地區的汲取 URL。

    * TAG_DATA 是以逗點區隔的標籤，其格式為 *TAG_NAME:TAG_VALUE*。您可以使一個以上的標籤與 Sysdig 代理程式產生關聯。例如：*role:serviceX,location:us-south*。 

    * 將 **sysdig_capture_enabled** 設為 *false*，以停用 Sysdig 擷取功能。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

    * 將 **secure** 設為 *true*，以使用 SSL 進行通訊。

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


## 在 Docker 容器上配置 Sysdig 代理程式
{: #config_agent_docker}

請完成下列步驟，在 Docker 容器上配置 Sysdig 代理程式，以收集度量並將其轉遞至 {{site.data.keyword.mon_full_notm}} 服務的實例：

1. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 取得汲取 URL。如需相關資訊，請參閱 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 部署 Sysdig 代理程式。請執行下列指令：

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是實例的汲取金鑰。

    * COLLECTOR_ENDPOINT 是可以使用監視實例之地區的汲取 URL。

    * TAG_DATA 是以逗點區隔的標籤，其格式為 *TAG_NAME:TAG_VALUE*。您可以使一個以上的標籤與 Sysdig 代理程式產生關聯。例如：*role:serviceX,location:us-south*。 

    * 將 **sysdig_capture_enabled** 設為 *false*，以停用 Sysdig 擷取功能。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig/captures.html#captures)。

    * 將 **SECURE** 設為 *true*，以使用 SSL 進行通訊。

    **附註：**容器以分離模式執行。若要查看容器的輸出，請移除 *-d*。




## 使用 Script 在 Kubernetes 叢集上配置 Sysdig 代理程式
{: #config_agent_kube_script}

請完成下列步驟，在執行於 {{site.data.keyword.containerlong_notm}} 的 Kubernetes 叢集上配置 Sysdig 代理程式：

1. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 取得汲取 URL。如需相關資訊，請參閱 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

4. 部署 Sysdig 代理程式。請執行下列指令：

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是實例的汲取金鑰。

    * COLLECTOR_ENDPOINT 是可以使用監視實例之地區的汲取 URL。

    * TAG_DATA 是以逗點區隔的標籤，其格式為 *TAG_NAME:TAG_VALUE*。您可以使一個以上的標籤與 Sysdig 代理程式產生關聯。例如：*role:serviceX,location:us-south*。 

    * 將 **sysdig_capture_enabled** 設為 *false*，以停用 Sysdig 擷取功能。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig/captures.html#captures)。



## 在 Kubernetes 叢集上手動配置 Sysdig 代理程式
{: #config_agent_kube_manually}

請完成下列步驟，在執行於 {{site.data.keyword.containerlong_notm}} 的 Kubernetes 叢集上配置 Sysdig 代理程式：

1. 取得 Sysdig 存取金鑰。如需相關資訊，請參閱[透過 {{site.data.keyword.cloud_notm}} 使用者介面取得存取金鑰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 取得汲取 URL。如需相關資訊，請參閱 [Sysdig 收集器端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

    **附註：**每次您登入 {{site.data.keyword.containerlong}} CLI 來使用叢集，您必須執行這些指令，將叢集配置檔的路徑設為階段作業變數。Kubernetes CLI 會使用此變數來尋找與 {{site.data.keyword.cloud_notm}} 中的叢集連接所需的本端配置檔及憑證。

4. 建立一個稱為 **Sysdig-agent** 的服務帳戶，以監視 kubernetes 叢集。請執行下列指令：

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. 將密碼新增至您的 Kubernet 叢集。請執行下列指令：

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY 是實例的汲取金鑰。

    Kubernetes 密碼包含汲取金鑰，可使用此金鑰，透過 {{site.data.keyword.mon_full_notm}} 服務鑑別 Sysdig 代理程式。它是用來在監視後端系統上，開啟汲取伺服器的安全 Web Socket。

6. 建立叢集角色及叢集角色連結。 

    下載 [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml)。
    
    若要新增叢集角色，請執行下列指令：
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    若要新增叢集角色連結，請執行下列指令：

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. 編輯 **sysdig-agent-configmap.yaml**，並新增必要參數，以配置要在 {{site.data.keyword.cloud_notm}} 中運作的代理程式。

    下載 [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml)。

    使用編輯器來開啟 sysdig-agent-configmap.yaml 檔。然後，新增下列參數：

    * **k8s_cluster_name**：此參數會將叢集名稱指定為度量標籤。您可以使用標籤 *kubernetes.cluster.name*，依叢集名稱導覽 Kubernetes 儀表板，並濾出與叢集相關聯的度量。

    * **collector**：此參數指定可以使用監視實例之地區的汲取 URL。 

    * **collector_port**：此參數指出正在其上接聽收集器的埠。其值必須是 *6443*。
    
    * **ssl**：此參數必須設為 *true*。
    
    * **ssl_verfiy_certificate**：此參數必須設為 *true*。
    
    * **new_k8s**：此參數必須設為 *true*，才能擷取 kube 狀態度量。

    * **sysdig_capture_enabled**：此參數可啟用或停用 Sysdig 擷取功能。依預設會設為 *true*。如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

    範例 yaml 檔案如下所示：

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. 將配置對映套用至叢集。請執行下列指令：

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. 套用 daemonset 以將 Sysdig 代理程式部署至叢集。請執行下列指令：

    下載 [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml)。

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




