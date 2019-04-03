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


# 導覽至 Grafana 儀表板
{:#navigating_grafana}

在 {{site.data.keyword.Bluemix}} 中，您可以使用 Grafana（一種開放程式碼分析與視覺化平台），以各種圖形（例如圖表和表格）監視、搜尋、分析及視覺化您的度量值。使用 Grafana 來執行進階分析作業。
{:shortdesc}

您可以使用下列任何方式來啟動 Grafana：

* 從 {{site.data.keyword.Bluemix_notm}}

    在 Grafana 中，您可以在特定 Docker 容器的環境定義下，啟動至該特定容器的度量值。此特性只適用於 {{site.data.keyword.Bluemix_notm}} 所管理基礎架構中部署的容器。 
    
    如需相關資訊，請參閱[從 {{site.data.keyword.Bluemix_notm}} 儀表板導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_bluemix)。

* 從直接瀏覽器鏈結

    您可以啟動 Grafana，以讓您看到的資料能從所提供的 {{site.data.keyword.Bluemix_notm}} 空間內的服務聚集日誌。
    
    如需相關資訊，請參閱[從 Web 瀏覽器導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。
    
如需 Grafana 的相關資訊，請參閱 [Grafana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://docs.grafana.org/guides/getting_started/){: new_window}。


##  從 IBM Cloud 儀表板導覽至 Grafana 儀表板
{: #launch_grafana_from_bluemix}

**附註：**此特性只適用於 {{site.data.keyword.Bluemix_notm}} 所管理基礎架構中部署的容器。 

用來過濾 Grafana 顯示資料的查詢，會擷取 Kibana 啟動所在之 {{site.data.keyword.Bluemix_notm}} 容器的資料。 

若要在 Grafana 中查看 Docker 容器的度量值，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從*儀表板* 按一下容器。 
    
2. 在導覽列中，按一下**監視及日誌**。即會開啟「監視」標籤。 
    
3. 按一下**進階視圖**。即會開啟 **Grafana** 儀表板。


##  從 Web 瀏覽器導覽至 Grafana 儀表板
{: #launch_grafana_from_browser}

用來過濾 Grafana 顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的資料。Grafana 顯示的度量值資訊，包括部署在 {{site.data.keyword.Bluemix_notm}} 組織中您登入空間內之所有資源的記錄。

完成下列步驟，以從瀏覽器啟動 Grafana：

1. 開啟 Web 瀏覽器。 
2. 輸入您要監視度量值之地區的 URL。 

    下表列出每個地區的 URL：
	<table>
      <caption>在不同地區啟動 Grafana 的 URL</caption>
      <tr>
        <th>地區</th>
	    <th>端點</th>
      </tr>
      <tr>
        <td>德國</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>英國</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>美國南部</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>英國</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. 選取 **Grafana**。
     

