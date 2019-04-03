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


# Sicurezza
{: #security_ov}

Per controllare le azioni del servizio {{site.data.keyword.monitoringshort}} che un utente può eseguire, puoi assegnare uno o più ruoli all'utente. Per autenticare un utente ad utilizzare le metriche e gli avvisi, puoi utilizzare un token UAA, IAM o una chiave API. 
{:shortdesc}





## Modelli di autenticazione
{: #auth}

Per utilizzare le metriche archiviate nel servizio {{site.data.keyword.monitoringshort}} per uno spazio, ti serve un token di autenticazione oppure la chiave API. 

Per ottenere un token di sicurezza, consulta:

* [Acquisizione di un token UAA ](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa)
* [Acquisizione di un token IAM](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)

Per ottenere una chiave API, vedi [Generazione di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key). Se la chiave API è compromessa, puoi revocarla eliminandola. Puoi quindi ricrearne una nuova. Per ulteriori informazioni, vedi [Revoca di una chiave API utilizzando la IU {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_api_key.html#revoke_ui). 

Un token UAA e un token IAM scadono dopo un certo periodo di tempo. La chiave API non scade. 

La seguente tabella elenca i modelli di sicurezza supportati per ogni tipo di dominio:

<table>
  <caption>Tabella 1. Modelli di sicurezza supportati per ogni dominio</caption>
  <tr>
    <th></th>
	<th align="right">Account</th>
    <th align="right">Organizzazione</th>
    <th align="right">Spazio</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">No</td>
	<td align="center">Sì</td>
	<td align="center">Sì</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">Sì</td>
	<td align="center">Sì</td>
	<td align="center">Sì</td>
  </tr>
</table>

Il servizio {{site.data.keyword.monitoringshort}} utilizza la funzione di controllo dell'accesso IAM per regolare le azioni o le operazioni che possono essere eseguite da un utente o servizio nel dominio. Ad esempio, puoi definire una politica IAM per consentire a un utente di inviare e creare dashboard in un dominio, ma non di recuperare le metriche dal dominio.



## Ruoli Cloud Foundry
{: #bmx_roles}

La seguente tabella elenca i privilegi di ogni ruolo Cloud Foundry per utilizzare il servizio {{site.data.keyword.monitoringshort}}:

<table>
  <caption>Tabella 2. Ruoli e privilegi Cloud Foundry per utilizzare il servizio {{site.data.keyword.monitoringshort}}.</caption>
  <tr>
    <th>Ruolo</th>
	<th>Dominio</th>
	<th>Privilegi di accesso</th>
  </tr>
  <tr>
    <td>Gestore</td>
	<td>Organizzazione <br>Spazio</td>
	<td>Tutte le API RESTful</td>
  </tr>
  <tr>
    <td>Sviluppatore</td>
	<td>Spazio</td>
	<td>Tutte le API RESTful</td>
  </tr>
  <tr>
    <td>Revisore</td>
	<td>Organizzazione <br>Spazio</td>
	<td>Solo le API RESTful che eseguono operazioni di sola lettura, come le metriche di query.</td>
  </tr>
</table>

Per informazioni sull'assegnazione dei ruoli utente nell'IU, consulta [Gestione dell'accesso a Cloud Foundry](/docs/iam/mngcf.html#mngcf).



## Ruoli IAM
{: #iam_roles}

La seguente tabella elenca le azioni del servizio {{site.data.keyword.monitoringshort}} quando utilizzi le metriche e i ruoli IAM che concedono le autorizzazioni a un utente per eseguire queste attività:

<table>
  <caption>Tabella 3. Utilizzo delle metriche </caption>
  <tr>
	<th>Azione</th>
	<th>Ruolo IAM</th>
  </tr>
  <tr>
    <td>Inviare metriche al dominio</td>
	<td>Amministratore, Editor, Operatore</td>
  </tr>
  <tr>
    <td>Richiamare/eseguire query sulle metriche</td>
	<td>Amministratore, Editor, Visualizzatore</td>
  </tr>
  <tr>
    <td>Ricercare le metriche nel dominio</td>
	<td>Amministratore, Editor</td>
  </tr>
</table>

La seguente tabella elenca le azioni del servizio {{site.data.keyword.monitoringshort}} quando utilizzi le metriche e i ruoli IAM che concedono gli avvisi a un utente per eseguire queste attività:

<table>
  <caption>Tabella 4. Utilizzo degli avvisi </caption>
  <tr>
	<th>Azione</th>
	<th>Ruolo IAM</th>
  </tr>
  <tr>
    <td>Crea, modifica ed elimina le regole di avviso</td>
	<td>Amministratore, Editor</td>
  </tr>
  <tr>
    <td>Visualizza avvisi</td>
	<td>Amministratore, Editor, Visualizzatore</td>
  </tr>
  <tr>
    <td>Crea, modifica ed elimina le notifiche di avviso</td>
	<td>Amministratore, Editor</td>
  </tr>
  <tr>
    <td>Visualizza notifiche</td>
	<td>Amministratore, Editor, Visualizzatore</td>
  </tr>
  <tr>
    <td>Visualizza i record cronologici dell'avviso attivato</td>
	<td>Amministratore, Editor, Visualizzatore</td>
  </tr>
</table>

Per informazioni sull'assegnazione dei ruoli utente nell'IU, consulta [Gestione dell'accesso IAM](/docs/iam/mngiam.html#iammanidaccser).

