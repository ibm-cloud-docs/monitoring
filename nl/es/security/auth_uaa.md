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


# Obtención de una señal de UAA
{: #auth_uaa}

Utilice el modelo de UAA de {{site.data.keyword.Bluemix}} para obtener una señal de autenticación que puede utilizar para trabajar con el servicio {{site.data.keyword.monitoringshort}}. Puede obtener la señal de autenticación utilizando la CLI de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

La señal tiene un tiempo de caducidad. 
		
## Obtención de la señal de UAA mediante la CLI de IBM Cloud
{: #uaa_cli}


Para obtener una señal de UAA, siga estos pasos:

1. (Requisito previo) Instalar la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
	
3. Ejecute el mandato `ibmcloud iam oauth-tokens` para obtener la señal de UAA.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	La salida devuelve la señal de UAA.

**Nota:** Cuando utilice la señal, elimine *Bearer* del valor de la señal que pasa en las llamadas de API.
	


	
