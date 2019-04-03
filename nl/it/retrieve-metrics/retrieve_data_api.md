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

# Recupero di metriche
{: #retrieve_data_api}

Puoi recuperare le metriche dal servizio {{site.data.keyword.monitoringshort}} utilizzando [l'API Metriche](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}.
{:shortdesc}


## Recupero di metriche da uno spazio
{: #uaa}

Per recuperare le metriche da uno spazio, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Configura il token di sicurezza o la chiave API
  
    Devi configurare il campo **X-Auth-User-Token** con un token di sicurezza o una chiave API. Puoi utilizzare un token UAA, IAM o una chiave API.

    Per prima cosa, scegli uno dei seguenti metodi per ottenere il token di sicurezza di cui hai bisogno per inviare le metriche:
	
    * Per ottenere un token UAA, vedi [Acquisizione del token UAA utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
    
	* Per ottenere un token IAM, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
    
	* Per ottenere una chiave API, vedi [Ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key). 

    Una chiave API o un token devono avere come prefisso uno dei seguenti valori: `apikey`, `iam` o `uaa` 

    dove 

    * *apikey* identifica che il token è una chiave API.
    * *iam* identifica che il token specificato è un token generato da IAM.
    * *uaa* identifica che il token specificato è un token generato da UAA.

    Ad esempio, puoi impostare la seguente intestazione per una chiave API: `X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	Successivamente, dallo stesso terminale a cui hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, configura la variabile Token per il token.

    Ad esempio, configura un token UAA e rimuovi la parte *Bearer* dal valore del token:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Ottieni l'ID dello spazio.

    Per richiamare le metriche, il campo di intestazione **X-Auth-Scope-Id** è obbligatorio e deve essere impostato sul GUID dello spazio. 

    Immetti il seguente comando:
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	Dove *SpaceName* è il nome dello spazio in cui intendi definire una notifica.
	
	Ad esempio, per ottenere il GUID di uno spazio con nome *dev*, immetti il seguente comando:
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	Il risultato di questo comando è il seguente:
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	Quindi, esporta la variabile *Space*. **Nota:** il GUID deve avere come prefisso *s-* per identificare uno spazio.
	
	Ad esempio:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}

4. Immetti il seguente comando cURL per inviare le metriche:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA {{site.data.keyword.Bluemix_notm}}.
	
	* Auth_Type è il prefisso che definisce il tipo di token. I valori validi sono: *uaa* per un token UAA, *iam* per un token IAM e *api* per una chiave API.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria solo se usi l'autenticazione UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* *Token* rappresenta il token di sicurezza.
	
	* *Space* rappresenta il GUID dello spazio. 
	
	* *Start_Time* definisce l'inizio della richiesta. Queste informazioni vengono utilizzate per calcolare il periodo di tempo relativo o assoluto. *End_Time* definisce la fine della richiesta. Queste informazioni vengono utilizzate per calcolare il periodo di tempo relativo o assoluto. Per ulteriori informazioni, vedi [Impostazione di un periodo di tempo](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#time).
	
	* *Path*  identifica una o diverse metriche. Puoi, facoltativamente, applicare delle funzioni a ciascuna metrica. I percorsi supportano anche i caratteri jolly, che ti consentono di identificare più di una metrica in un singolo percorso. Per ulteriori informazioni, vedi [Definizione delle metriche](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#metrics).
	
	* *METRICS_ENDPOINT* rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
## Definizione delle metriche
{: #metrics}

Per recuperare i dati per una metrica, devi specificare il percorso della metrica dalla root della struttura ad albero delle metriche fino alla metrica stessa e devi separare ciascun passo con un punto (.).

Il percorso è specificato nel parametro **Destinazione**. Può essere specificato un massimo di 5 destinazioni per richiesta.  

Puoi, facoltativamente, applicare delle funzioni alla metrica. Per ulteriori informazioni sulle funzioni supportate, vedi il documento relativo alle [funzioni di Graphite 0.9.15![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html).

Puoi utilizzare dei caratteri jolly per definire un percorso. Utilizzando i caratteri jolly, puoi identificare più di una metrica in un singolo percorso. 

* **Asterisco**: puoi utilizzare un asterisco (*) per una corrispondenza a zero o più caratteri. 

    Puoi avere più di un asterisco in un singolo elemento percorso, ad esempio: `servers.sp*aeg*r.cpu.total.*` Questo esempio restituisce i dati relativi alla CPU totale per tutti i server che corrispondono allo schema.

* **Elenco o intervallo di caratteri**: puoi definire i caratteri tra parentesi ([...]) per specificare una singola posizione di carattere nella stringa percorso. 

    Puoi impostare un intervallo inclusivo di caratteri specificando due caratteri separati da un trattino (-). La corrispondenza sarà con tutti i caratteri compresi tra questi due caratteri. 
	
	Puoi definire uno o più intervalli di caratteri tra parentesi. 
	
	Quando i caratteri all'interno di un set di parentesi non possono essere letti come un intervallo, i caratteri vengono trattati come un elenco di valori. 
	
	Puoi includere un trattino (-) come un carattere in un elenco di valori inserendolo all'inizio a alla fine all'interno delle parentesi.

* **Elenco valori**: puoi impostare dei valori separati da virgole all'interno di parentesi graffe per definire degli elenchi di valori. 

    Ad esempio, per scaricare le metriche per i seguenti percorsi: `servers.myserver.cpu.total.user` e `servers.myserver.cpu.total.system`, puoi impostare un singolo percorso per entrambi i tipi: `servers.myserver.cpu.total.{user,system}`



## Impostazione di un periodo di tempo
{: #time}

Puoi, facoltativamente, specificare un periodo di tempo utilizzando un tempo relativo o un tempo assoluto. Devi definire i parametri di query **From** e **Until**.  

* Quando l'ora di inizio del periodo di tempo viene omessa, il valore predefinito è 24 ore fa. 

* Quando l'ora di fine del periodo di tempo viene omessa, il valore predefinito è l'ora corrente *now*.

Il tempo relativo (**Relative time**) è sempre preceduto da un segno meno (-) e seguito da un'unità di tempo. 

La seguente tabella elenca le diverse abbreviazioni di tempo relativo che puoi usare:


| Abbreviazione | Descrizione |
|--------------|-------------|
| s            | Secondi     |
| min          | Minuti     |
| h            | Ore       |
| d            | Giorni        |
| w            | Settimane       |
| mon          | Mesi      |
| now          | Ora corrente |


Puoi utilizzare i seguenti formati per definire un tempo assoluto (**Absolute time**): `HH:MM_YYMMDD`, `YYYYMMDD`, `MM/DD/YY`

| Abbreviazione | Descrizione |
|--------------|-------------|
| YYYY         | Anno a quattro cifre |
| MM           | Mese a due cifre (01=Gen ecc.) |
| DD           | Giorno del mese a due cifre (da 01 a 31) |
| hh           | Due cifre dell'ora (da 00 a 23) |
| mm           | Due cifre del minuto (da 00 a 59) |
| ss           | Due cifre del secondo (da 00 a 59) |

**Esempio**

La seguente tabella mostra diversi esempi di come impostare diversi periodi di tempo impostando i parametri *from* e *until*:

<table>
  <caption>Tabella 1. Diversi esempi che mostrano come impostare diversi periodi di tempo impostando i parametri *from* e *until*</caption>
  <tr>
    <th>Esempio</th>
	<th>Descrizione</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>Periodo di tempo che include i dati da lunedì scorso fino a ora.</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>Periodo di tempo impostato su un mese, ad esempio novembre </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>Per visualizzare i dati in un ciclo di 24 ore, ad esempio, dalle 02.00 alle 14.00 del 1° luglio 2017</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>Per visualizzare lo stesso giorno della settimana, ad esempio, la settimana scorsa</td>
  </tr>
  
</table>


