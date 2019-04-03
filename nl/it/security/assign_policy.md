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


# Concessione delle autorizzazioni utente
{: #grant_permissions}

In {{site.data.keyword.Bluemix}}, puoi assegnare uno o più ruoli agli utenti. Questi ruoli definiscono quali attività sono abilitate per tale utente per l'utilizzo con il servizio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

Per concedere a un utente le autorizzazioni per utilizzare le metriche, devi aggiungere una politica per tale utente che descrive le azioni che può eseguire con il servizio {{site.data.keyword.monitoringshort}} nell'account. Solo i proprietari dell'account possono assegnare politiche individuali agli utenti.


## Assegnazione a un utente di una politica IAM tramite la IU IBM Cloud 
{: #assign_policy_ui}

Completa la seguente procedura per concedere a un utente le autorizzazioni per utilizzare il servizio {{site.data.keyword.monitoringshort}}:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra del menu, fai clic su **Gestisci > Account > Utenti**. 

    La finestra *Utenti* visualizza un elenco di utenti con i rispettivi indirizzi email per l'account attualmente selezionato.
	
3. Se l'utente è un membro dell'account, seleziona il nome utente dall'elenco o fai clic su **Gestisci utente** dal menu *Azioni*.

    Se l'utente non è un membro dell'account, consulta [Invito di utenti](/docs/iam/iamuserinv.html#iamuserinv).

4. Fai clic su **Assegna politiche del servizio**.

5. Immetti le informazioni sulla politica. La seguente tabella elenca i campi che sono necessari o facoltativi per definire una politica: 

    <table>
	  <caption>Elenco dei campi per configurare una politica IAM.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valore</th>
		<th>Stato</th>
	  </tr>
	  <tr>
	    <td>Servizio</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>Obbligatorio</td>
	  </tr>
	  <tr>
	    <td>Ruoli</td>
		<td>Seleziona uno o più ruoli IAM. <br>I ruoli validi sono: *amministratore*, *operatore*, *editor* e *visualizzatore*. <br>Per ulteriori informazioni sulle azioni consentite per un ruolo, consulta [Ruoli IAM](/docs/services/cloud-monitoring/security_ov.html#iam_roles).</td>
		<td>Obbligatorio</td>
	  </tr>
	  <tr>
	    <td>Regioni</td>
		<td>Puoi specificare le regioni in cui sta per essere concessa la possibilità di utilizzare le metriche all'utente. Seleziona **Specifica contesto del servizio facoltativo**. Quindi, aggiungi una o più regioni individualmente o seleziona **Tutte le regioni correnti** per concedere l'accesso a tutte le regioni.</td>
		<td>Facoltativo</td>
	  </tr>
	</table>
	
6. Fai clic su **Assegna criterio**.
	
La politica che configuri è applicabile alle regioni selezionate. 

## Assegnazione a un utente di una politica IAM utilizzando la riga di comando
{: #assign_policy_commandline}

Completa la seguente procedura per concedere a un utente l'accesso per visualizzare le metriche utilizzando la riga di comando:

1. (Pre-req) Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
   
   Se la CLI è installata, vai al passo successivo.
	
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Ottieni l'ID dell'account. 

    Immetti il seguente comando per ottenere l'ID dell'account:

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	Viene visualizzato un elenco di account con i rispettivi GUID.
	
	Esporta l'ID dell'account in cui pianifichi di concedere le autorizzazioni a un utente. Configura una variabile shell come ad esempio `$acct_id`:
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. Ottieni l'ID {{site.data.keyword.IBM_notm}} dell'utente a cui desideri concedere le autorizzazioni.

    1. Visualizza gli utenti associati all'account. Immetti il seguente comando:
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. Ottieni il GUID dell'utente. **Nota: questo passo deve essere completato dall'utente a cui pianifichi di concedere le autorizzazioni.**
	
	    Ad esempio, richiedi all'utente di eseguire i seguenti comandi per ottenere il proprio ID utente:
		
		Ottieni il token IAM. Per ulteriori informazioni, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli).

        Ottieni i dati dal token IAM compresi tra i primi due punti nel token IAM. Esporta i dati in una variabile shell come `$user_data`. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Esegui il seguente comando, ad esempio, per ottenere l'ID dell'utente. Questo comando utilizza jq in questo esempio per decodificare le informazioni nel testo formattato JSON:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		L'output di esecuzione di questo comando è il seguente:
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Invia l'ID dell'utente, che è il valore del campo *id* al proprietario dell'account. 
		
	3. Esporta l'ID dell'utente in una variabile shell come `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Invita l'utente nell'account se non ne è ancora un membro. Per ulteriori informazioni, vedi [Invito di utenti](/docs/iam/iamuserinv.html#iamuserinv).

    Ad esempio, esegui il seguente comando per invitare l'utente xxx@yyy.com nell'account zzz@ggg.com:
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Crea un nome del file della politica. 

    Ad esempio, utilizza il seguente template per concedere le autorizzazioni di visualizzazione nella regione Stati Uniti Sud:
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Nome del file della politica: `policy.json`
	
5. Ottieni il token IAM per il tuo ID utente.

    Per ulteriori informazioni, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli).

    Esporta il token IAM in una variabile shell come ad esempio `$iam_token`:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Concedi all'utente le autorizzazioni per utilizzare il servizio {{site.data.keyword.monitoringshort}}. 

   Immetti il seguente comando cURL per concedere le autorizzazioni nella regione Stati Uniti Sud:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Immetti il seguente comando cURL per concedere le autorizzazioni nella regione Regno Unito:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## Concessione a un utente di un ruolo CF tramite la IU IBM Cloud 
{: #grant_permissions_ui_space}


Per utilizzare le metriche nel dominio dello spazio o dell'organizzazione, a un utente deve essere assegnato un ruolo Cloud Foundry (CF) in {{site.data.keyword.Bluemix_notm}}. Un ruolo CF illustra le azioni che un utente può eseguire con il servizio {{site.data.keyword.monitoringshort}} in uno spazio o organizzazione. 

Completa la seguente procedura per concedere a un utente le autorizzazioni per utilizzare il servizio {{site.data.keyword.monitoringshort}}:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra del menu, fai clic su **Gestisci > Account > Utenti**. 

    La finestra *Utenti* visualizza un elenco di utenti con i rispettivi indirizzi email per l'account attualmente selezionato.
	
3. Se l'utente è un membro dell'account, seleziona il nome utente dall'elenco o fai clic su **Gestisci utente** dal menu *Azioni*.

    Se l'utente non è un membro dell'account, consulta [Invito di utenti](/docs/iam/iamuserinv.html#iamuserinv).

4. Fai clic su **Assegna organizzazione**.

5. Immetti le informazioni sulla politica. La seguente tabella elenca i campi che sono necessari o facoltativi per definire una politica: 

    <table>
	  <caption>Elenco dei campi per configurare una politica CF.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valore</th>
	  </tr>
	  <tr>
	    <td>Organizzazione</td>
		<td>Scegli un'organizzazione dall'elenco.</td>
	  </tr>
	  <tr>
	    <td>Ruoli organizzazione</td>
		<td>Seleziona **Nessun ruolo organizzazione**. Tuttavia, se l'utente ha un ruolo dell'organizzazione, scegline uno dall'elenco. <br>I valori validi sono: **Gestore fatturazione**, **Revisore**, **Gestore**</td>
	  </tr>
	  <tr>
	    <td>Regione</td>
		<td>Scegli una regione dall'elenco: <br>I valori validi sono: **Tutte le regioni correnti**, **Stati Uniti Sud**, **Regno Unito**</td>
	  </tr>
	  <tr>
	    <td>Spazio</td>
		<td>Per impostazione predefinita, **Tutti gli spazi correnti** è il valore predefinito quando il campo *Regione* è impostato su **Tutte le regioni correnti**. Per concedere l'autorizzazione a uno spazi individuale, scegli una regione specifica e poi uno spazio dall'elenco.</td>
	  </tr>
	  <tr>
	    <td>Ruoli spazio</td>
		<td>Scegli un ruolo dello spazio dall'elenco. <br>I valori validi sono: **Gestore**, **Revisore**, **Sviluppatore** e **Nessun ruolo spazio**. Per ulteriori informazioni, vedi [Ruoli Cloud Foundry](/docs/services/cloud-monitoring/security_ov.html#bmx_roles).</td>
	  </tr>
	</table>
	
6. Fai clic su **Assegna criterio**.
	
La politica che configuri è applicabile alle regioni selezionate. 


