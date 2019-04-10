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

# Configurando um agente Sysdig
{: #config_agent}

Depois de provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}, deve-se configurar um agente Sysdig em cada ambiente que você deseja monitorar. O agente Sysdig coleta e relata automaticamente as métricas predefinidas. É possível configurar quais métricas devem ser monitoradas em cada ambiente.
{:shortdesc}

É possível associar uma ou mais tags a cada agente Sysdig. As tags são valores separados por vírgula formatados como **TAG_NAME:TAG_VALUE**. Ao monitorar seu ambiente, é possível usar essas tags para identificar as métricas que estão disponíveis em um agente. Por exemplo, é possível incluir informações sobre o nome do serviço e o local com todas as métricas que são coletadas por esse agente.
{: tip}

## Configurando um agente Sysdig no Linux
{: #config_agent_linux}

Conclua as etapas a seguir para configurar um agente Sysdig no Linux para coletar e encaminhar métricas para uma instância do serviço {{site.data.keyword.mon_full_notm}}:

1. Obtenha a chave de acesso do Sysdig. Para obter mais informações, consulte [Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenha a URL de ingestão. Para obter mais informações, consulte [Terminais do coletor Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Implemente o agente Sysdig. Execute o comando a seguir em um terminal.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Em que

    * SYSDIG_ACCESS_KEY é a chave de ingestão para a instância.

    * COLLECTOR_ENDPOINT é a URL de ingestão da região na qual a instância de monitoramento está disponível.

    * TAG_DATA são tags separadas por vírgulas formatadas como *TAG_NAME:TAG_VALUE*. É possível associar uma ou mais tags a seu agente Sysdig. Por exemplo: *role:serviceX,location:us-south*. 

    * Configure **sysdig_capture_enabled** como *false* para desativar o recurso de captura de Sysdig. Por padrão, é configurado como *true*. Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    * Configure **secure** como *true* para usar SSL com a comunicação.

Se o agente Sysdig falhar em ser instalado corretamente, instale os cabeçalhos de kernel manualmente. Escolha uma distribuição e execute o comando para essa distribuição. Em seguida, tente novamente a implementação do agente Sysdig.

* **Para distribuições Debian e Ubuntu do Linux**, execute o comando a seguir:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Para distribuições RHEL, CentOS e Fedora do Linux**, execute o comando a seguir:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Configurando um agente Sysdig em um contêiner do Docker
{: #config_agent_docker}

Conclua as etapas a seguir para configurar um agente Sysdig em um contêiner do Docker para coletar e encaminhar métricas para uma instância do serviço {{site.data.keyword.mon_full_notm}}:

1. Obtenha a chave de acesso do Sysdig. Para obter mais informações, consulte [Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenha a URL de ingestão. Para obter mais informações, consulte [Terminais do coletor Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Implemente o agente Sysdig. Execute o seguinte comando:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    sendo

    * SYSDIG_ACCESS_KEY é a chave de ingestão para a instância.

    * COLLECTOR_ENDPOINT é a URL de ingestão da região na qual a instância de monitoramento está disponível.

    * TAG_DATA são tags separadas por vírgulas formatadas como *TAG_NAME:TAG_VALUE*. É possível associar uma ou mais tags a seu agente Sysdig. Por exemplo: *role:serviceX,location:us-south*. 

    * Configure **sysdig_capture_enabled** como *false* para desativar o recurso de captura de Sysdig. Por padrão, é configurado como *true*. Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    * Configure **SECURE** como *true* para usar SSL com a comunicação.

    **Nota:** o contêiner é executado no modo separado. Para ver a saída do contêiner, remova *-d*.




## Configurando um agente Sysdig em um cluster Kubernetes usando um script
{: #config_agent_kube_script}

Conclua as etapas a seguir para configurar um agente Sysdig em um cluster Kubernetes executado no {{site.data.keyword.containerlong_notm}}:

1. Obtenha a chave de acesso do Sysdig. Para obter mais informações, consulte [Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenha a URL de ingestão. Para obter mais informações, consulte [Terminais do coletor Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

4. Implemente o agente Sysdig. Execute o seguinte comando:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    sendo

    * SYSDIG_ACCESS_KEY é a chave de ingestão para a instância.

    * COLLECTOR_ENDPOINT é a URL de ingestão da região na qual a instância de monitoramento está disponível.

    * TAG_DATA são tags separadas por vírgulas formatadas como *TAG_NAME:TAG_VALUE*. É possível associar uma ou mais tags a seu agente Sysdig. Por exemplo: *role:serviceX,location:us-south*. 

    * Configure **sysdig_capture_enabled** como *false* para desativar o recurso de captura de Sysdig. Por padrão, é configurado como *true*. Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Configurando um agente Sysdig em um cluster Kubernetes manualmente
{: #config_agent_kube_manually}

Conclua as etapas a seguir para configurar um agente Sysdig em um cluster Kubernetes executado no {{site.data.keyword.containerlong_notm}}:

1. Obtenha a chave de acesso do Sysdig. Para obter mais informações, consulte [Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenha a URL de ingestão. Para obter mais informações, consulte [Terminais do coletor Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

4. Crie uma conta de serviço chamada **sysdig-agent** para monitorar o cluster Kubernetes. Execute o seguinte comando:

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Inclua um segredo em seu cluster Kubernetes. Execute o seguinte comando:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    O SYSDIG_ACCESS_KEY é a chave de ingestão para a instância.

    O segredo do Kubernetes contém a chave de ingestão que é usada para autenticar o agente Sysdig com o serviço {{site.data.keyword.mon_full_notm}}. Ele é usado para abrir um soquete seguro da web para o servidor de ingestão no sistema back-end de monitoramento.

6. Crie uma função de cluster e uma ligação de função de cluster. 

    Faça download do  [ ** sysdig-agent-clusterrole.yaml ** ](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    Para incluir uma função de cluster, execute o comando a seguir:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    Para incluir uma ligação de função de cluster, execute o comando a seguir:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. Edite o **sysdig-agent-configmap.yaml** e inclua os parâmetros necessários para configurar o agente para trabalhar no {{site.data.keyword.cloud_notm}}.

    Faça download do  [ ** sysdig-agent-configmap.yaml ** ](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Use um editor para abrir o arquivo sysdig-agent-configmap.yaml. Em seguida, inclua os parâmetros a seguir:

    * **k8s_cluster_name**: esse parâmetro especifica o nome do cluster como um rótulo de métrica. É possível usar o rótulo *kubernetes.cluster.name* para navegar pelos painéis do Kubernetes por nome do cluster e filtrar as métricas associadas ao cluster.

    * **collector**: esse parâmetro especifica a URL de ingestão para a região na qual a instância de monitoramento está disponível. 

    * **collector_port**: esse parâmetro indica a porta na qual o coletor está atendendo. O valor deve ser  * 6443 *.
    
    * **ssl**: esse parâmetro deve ser configurado como *true*.
    
    * **ssl_verfiy_certificate**: esse parâmetro deve ser configurado como *true*.
    
    * **new_k8s**: esse parâmetro deve ser configurado como *true* para capturar as métricas de estado do kube.

    * **sysdig_capture_enabled**: esse parâmetro ativa ou desativa o recurso de captura do Sysdig. Por padrão, é configurado como *true*. Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    Um arquivo yaml de exemplo é semelhante ao seguinte:

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

8. Aplique o mapa de configuração ao cluster. Execute o seguinte comando:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. Aplique o daemonset para implementar o agente Sysdig no cluster. Execute o seguinte comando:

    Faça download do [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




