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

# 使用 Monitoring 插件 (collectd) 发送数据
{: #conf_monitoring_plugin}

您可以配置 collectd 以在环境中收集度量值。使用 {{site.data.keyword.monitoringshort}} 插件，将这些度量值从环境发送到空间域。
{: shortdesc}

下图显示了如何使用 {{site.data.keyword.monitoringshort}} 插件，将度量值发送到 {{site.data.keyword.monitoringshort}} 服务的高级视图：

![如果使用 {{site.data.keyword.monitoringshort}} 插件的高级视图](images/monitoring_plugin_ov.png "如何使用 {{site.data.keyword.monitoringshort}} 插件的高级视图")



## 安装 Monitoring 插件
{: #install}

通过终端，完成以下步骤： 

1. （先决条件）安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)。
   
   如果 CLI 已安装，请继续执行下一步。
	
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

    例如，要登录到美国南部区域，请运行以下命令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    遵循指示信息进行操作。输入您的 {{site.data.keyword.Bluemix_notm}} 凭证，然后选择组织和空间。

### 步骤 1：安装 collectd
{: #collectd}

以管理员的身份，完成以下步骤以安装 collectd：

1.	以 root 用户身份登录。

     

    ```
    sudo -s
    ```
    {: codeblock}

2.	安装网络时间协议 (NTP) 软件包以同步日志的时间。 

    例如，对于 Ubunutu 系统，请检查 `timedatectl status` 是否显示 *Network time on: yes*。如果是，那么您的 Ubuntu 系统已配置为使用 ntp，您可以跳过此步骤。
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    要在 Ubuntu 系统中安装 ntp，请完成以下步骤：

    1.	运行以下命令来更新软件包。 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	运行以下命令以安装 ntp 软件包。 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	运行以下命令以安装 ntpdate 软件包。 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	运行以下命令以停止服务。 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	运行以下命令以同步系统时钟。 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        结果将确认时间已调整，例如：

        
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	运行以下命令以再次启动 ntpd。 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        结果将确认服务正在启动。



3. 安装 collectd。运行以下命令：

    ```
	apt-get install collectd
	```
	{: codeblock}


### 步骤 2：安装 Monitoring 插件
{: #plugin}

要安装 {{site.data.keyword.monitoringshort}} 插件，请完成以下步骤：

1. 	以 root 用户身份登录。

     

    ```
    sudo -s
    ```
    {: codeblock}
	
2. 添加 {{site.data.keyword.monitoringshort}} 服务存储库。运行以下命令：

    ```
        wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. 安装插件。运行以下命令：

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## 配置 Monitoring 插件
{: #configure}

要配置 {{site.data.keyword.monitoringshort}} 插件，请完成以下步骤：
	
### 步骤 1：向用户分配 IAM 策略
{: #iam_policy}

要将度量值发送到任何域，必须向您的用户标识授予 IAM 角色，该角色具有将度量值发送到 Monitoring 服务的许可权。
 
* 通过在 IBM Cloud 中为该用户分配 IAM 策略来设置许可权。 
* 以下 IAM 角色允许用户发送度量值：*管理员*、*编辑者*和*操作员*。 

要为用户分配 IAM 策略，请选择以下某个方法：



* 通过 {{site.data.keyword.Bluemix_notm}} UI：有关更多信息，请参阅[通过 {{site.data.keyword.Bluemix_notm}} UI 向用户分配 IAM 策略](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui)。
* 通过使用命令行：有关更多信息，请参阅[使用命令行向用户分配 IAM 策略](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_commandline)。
 
### 步骤 2：获取 API 密钥
{: #api_key}
 
要将度量值发送到空间，您必须获取 API 密钥以向 {{site.data.keyword.monitoringshort}} 服务进行认证。



有关如何获取 API 密钥的更多信息，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)。
	
通过您登录到 {{site.data.keyword.Bluemix_notm}} 的相同终端，为令牌设置 APIKEY 变量。



例如：

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### 步骤 3：获取有关端点的信息
{: #endpoint}

要确定要发送度量值的 {{site.data.keyword.monitoringshort}} 端点，请查看每个区域的端点列表（请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)），并识别区域中要发送度量值的端点。

通过您登录到 {{site.data.keyword.Bluemix_notm}} 的相同终端，设置 **METRIC_ENDPOINT** 变量。例如：

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### 步骤 4：获取有关空间域标识的信息 
{: #domain}

要获取空间的域标识，请[获取空间 GUID](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid)。然后，按如下所示设置域标识：`s-SpaceID`，其中 SpaceID 是空间的 GUID。

通过您登录到 {{site.data.keyword.Bluemix_notm}} 的相同终端，设置 SpaceID 变量：



```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### 步骤 5：运行配置脚本
{: #script}

运行以下脚本以配置 {{site.data.keyword.monitoringshort}} 插件将度量值发送到空间：

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


该脚本会自动将 **Include** 节添加到主 collectd.conf 文件中：

```
<LoadPlugin IBMCloudMonitoring>
   FlushInterval 60
</LoadPlugin>
<Plugin IBMCloudMonitoring>
  <Endpoint "ng">
     Host "metrics.ng.bluemix.net"
     Port 9095
     ApiKey "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     SkipInternalPrefixForStatsd false
     RateCounter false
     ScopeId "s-cedc73c5-6d55-4193-a9de-378620d6fab5"
  </Endpoint>
</Plugin>
```
{: screen}


### 步骤 6：重新启动 collectd 守护程序
{: #restart}

请完成以下步骤：

1. 	以 root 用户身份登录。

     

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  重新启动 collectd。

   

   如果已将 collectd 守护程序添加为服务，请运行以下命令：
	
	
	
	```
	service collectd restart
	```
	{: codeblock}

在 collectd 中启用的度量值是可供在 Grafana 中进行分析的度量值。


