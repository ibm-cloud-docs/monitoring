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

# Configurazione degli avvisi in Grafana
{: #config_alerts_grafana}

Il servizio {{site.data.keyword.monitoringshort}} fornisce un sistema di avvisi basati su query. Puoi configurare gli avvisi in Grafana nei dashboard che non hanno variabili del template. 
{:shortdesc}

Per configurare un avviso per una query della metrica tramite la IU Grafana, completa la seguente procedura:

1. Avvia Grafana.
2. Definisci uno o più canali di notifica.
3. Crea un dashboard Grafana che include un grafico e almeno una query della metrica. 
4. Configura l'avviso tramite la scheda **Avvisi** in un grafico Grafana.

## Passo 1: avvia Grafana
{: #step1_cag1}

Avvia Grafana da un browser. Ad esempio, immetti il seguente URL per aprire Grafana nella regione Stati Uniti Sud: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

Per un elenco di URL Grafana per regione, consulta [URL per il servizio {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/monitoring_ov.html#region).

## Passo 2: definisci uno o più canali di notifica
{: #step2_cag2}

Completa la seguente procedura:

1. In Grafana, seleziona la barra dei menu laterale.

2. Seleziona **Avviso > Canali di notifica > Nuovo canale**.

3. Immetti i dati per il nuovo canale. Aggiungi un canale di notifica email, ad esempio.

<table>
  <caption>Dati e metodo di notifica email che devi inserire per creare un nuovo canale</caption>
  <tr>
     <th>Campo</th>
     <th>Descrizione</th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Il nome del canale di notifica. Questo valore deve essere univoco.</td>
  </tr>
  <tr>
    <td>Descrizione</td>
    <td>Le informazioni aggiuntive che potresti voler includere per scopi di documentazione.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Seleziona: **Email**</td>
  </tr>
  <tr>
    <td>ID email</td>
    <td>Immetti l'indirizzo e-mail del destinatario. </br>Puoi immettere più indirizzi email separati da virgole.</td>
  </tr>
</table>

<table>
  <caption>Dati e metodo di notifica webhook che devi inserire per creare un nuovo canale</caption>
  <tr>
     <th>Campo</th>
     <th>Descrizione</th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Il nome del canale di notifica. Questo valore deve essere univoco.</td>
  </tr>
  <tr>
    <td>Descrizione</td>
    <td>Le informazioni aggiuntive che potresti voler includere per scopi di documentazione.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Seleziona: **Webhook**</td>
  </tr>
  <tr>
    <td>URL POST webhook</td>
    <td>Immetti l'URL dove deve essere eseguito POST.</td>
  </tr>
  <tr>
    <td>Intestazioni webhook</td>
    <td>Immetti tutte le intestazioni.</td>
  </tr>
  <tr>
    <td>Parametri di query webhook</td>
    <td>Immetti tutti i parametri di query.</td>
  </tr>
</table>

<table>
  <caption>Dati e metodo di notifica PagerDuty che devi inserire per creare un nuovo canale</caption>
  <tr>
     <th>Campo</th>
     <th>Descrizione</th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Il nome del canale di notifica. Questo valore deve essere univoco.</td>
  </tr>
  <tr>
    <td>Descrizione</td>
    <td>Le informazioni aggiuntive che potresti voler includere per scopi di documentazione.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Seleziona: **PagerDuty**</td>
  </tr>
  <tr>
    <td>Chiave API PagerDuty</td>
    <td>Immetti la chiave PagerDuty.</td>
  </tr>
</table>

## Passo 3: definisci una metrica
{: #step3_cag3}

Completa la seguente procedura per creare un nuovo dashboard:

1. Seleziona il commutatore della barra dei menu laterale ![Barra di menu laterale Grafana](images/grafana_settings.gif "Barra dei menu laterale Grafana").
2. Seleziona **Dashboard**.
3. Fai clic su **Nuovo**

Si aprirà un dashboard. Il dashboard include una riga vuota che è pronta per la configurazione. 

Successivamente, aggiungi una query della metrica:

1. Aggiungi un pannello *Grafico*.
2. Seleziona **Grafico**.
3. Fai clic sul titolo del grafico e quindi seleziona **modifica**.
    
    Si apre la scheda *Metriche*. Qui puoi vedere l'origine dati predefinita.
    
4. Definisci la query della metrica che filtra i dati da visualizzare nel grafico. 


## Passo 4: definisci un avviso
{: #step4_cag4}

Completa la seguente procedura per definire un avviso nella IU Grafana:

1. Seleziona la scheda **Avviso**.
2. Nella sezione **Configurazione avvisi**, definisci la regola che definisce le condizioni per cui viene generata una notifica di avviso.

    Configura il campo **Valuta tutto** e la sezione **Condizioni**.

3. Nella sezione **Notifiche**, seleziona uno o più canali di notifica.

**Nota:** 

* Quando viene configurata una condizione, puoi vedere una linea rossa nel grafico per definire la soglia impostata. Puoi trascinarla nel grafico per modificarla.
* Dopo aver creato l'avviso, se desideri modificarlo, devi farlo utilizzando l'API Avvisi.
* Se selezioni **Elimina**, l'avviso viene eliminato.

## Successivamente: verifica che è stato generato avviso
{: #next_cag5}

Ad esempio, se hai creato un canale di notifica email, controlla la tua email.

Ricerca le email con mittente **IBM Cloud Monitoriing**.

Un'email include le informazioni sull'avviso attivato e un link al dashboard Grafana in cui puoi visualizzare la situazione.

Ad esempio:

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


