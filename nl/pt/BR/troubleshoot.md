---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Resolução de problemas para o  {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Saiba mais sobre alguns problemas gerais que podem ser encontrados ao usar o serviço {{site.data.keyword.mon_full_notm}}. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{:shortdesc}

## Você está recebendo um erro ao criar uma captura?
{: #troubleshoot-entry-1}

Você está falhando ao criar um [arquivo de captura](/docs/services/Monitoring-with-Sysdig/captures.html#captures) para um host em sua infraestrutura. 

Na seção *Capturas* da IU da web, você obtém um erro quando tenta criar um arquivo de captura para um host.
{: tsSymptoms}

O agente Sysdig que é executado no host tem o recurso **sysdig_capture_enabled** configurado como *false*.
{: tsCauses}

Ative o recurso **sysdig_capture_enabled** no agente Sysdig que é executado no host.
{: tsResolve}


## O status de seu arquivo de captura é configurado como *solicitado* e não muda para o status *transferido por upload*?
{: #troubleshoot-entry-2}

O status de um [arquivo de captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures) é configurado como *solicitado* e não muda para o status *transferido por upload*. Você está esperando o arquivo de captura ficar disponível para análise.

Na seção *Capturas* da IU da web, o status do arquivo de captura de um host não muda
para *transferido por upload*.
{: tsSymptoms}

O host tem a porta TCP 6443 desativada.
{: tsCauses}


Verifique se a porta 6443 está aberta. Para obter mais informações, consulte [Gerenciando o tráfego de rede](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)
{: tsResolve}


