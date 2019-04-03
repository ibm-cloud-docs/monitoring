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


# {{site.data.keyword.containershort_notm}}
{: #metrics_format_containers}

As consultas que você define no Grafana para monitorar o
serviço do {{site.data.keyword.containershort_notm}}
seguem o padrão a seguir: 
{:shortdesc}



## Formato de consulta para as métricas da CPU coletadas para contêineres
{: #cpu_containers}

O formato de uma consulta que você define no Grafana para monitorar uma métrica de CPU para um contêiner
que é executado no serviço do {{site.data.keyword.containershort_notm}} é descrito como segue: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

Em que

<table>
  <caption>Campos obrigatórios para definir uma métrica de CPU para um contêiner </caption>
  <tr>
    <th>Campo</th>
	  <th>Descrição</th>
	  <th>Valor</th>
  </tr>
  <tr>
    <td>Fonte</td>
	  <td>Este é um nome reservado. As métricas sob esta hierarquia são provenientes de aplicativos e serviços do
{{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo de nuvem</td>
	  <td>Indica o tipo do Cloud. </td>
	  <td>Para a nuvem pública do {{site.data.keyword.Bluemix_notm}}, o valor é: *public*</td>
  </tr>
  <tr>
    <td>Nome do serviço</td>
	  <td>Define o nome do serviço no {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Para apps CF, o valor é: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Região</td>
	  <td>Define a região em que o contêiner está em execução.</td>
	  <td>Para a região Sul dos EUA, o valor é: *us-south* <br>Para a região do Reino Unido, o valor
é: *united-kingdom*  <br>Para Alemanha, o valor é: *frankfurt* <br>Para Sydney, o
valor é: *sydney* </td>
  </tr>
  <tr>
    <td>Nome do cluster</td>
	  <td>O nome do cluster a ser monitorado.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Origem de métrica</td>
	  <td>A origem dos dados.</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>O namespace no qual o contêiner é implementado em um cluster do Kubernetes.</td>
	<td></td>
  </tr>
   <tr>
    <td>Nome do pod</td>
	<td>Nome do módulo.</td>
	<td></td>
  </tr>
  <tr>
    <td>Nome do contêiner</td>
	<td>O nome do contêiner.</td>
	<td></td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	  <td>O tipo de métrica.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica a ser exibida.</td>
	  <td>*usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Funções de consulta que podem ser selecionadas para visualizar uma métrica de contêiner no painel. </td>
    <td>[Functions ![(Ícone de link externo)](../../../icons/launch-glyph.svg "Ícone de link externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Por exemplo, uma consulta para monitorar o uso de CPU para um contêiner que está em execução em um
cluster do Kubernetes na região sul dos EUA é definida como segue:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## Formato de consulta para as métricas de carregamento coletadas para os trabalhadores
{: #load_workers}

O formato de uma consulta que você define no Grafana para monitorar uma métrica de carregamento para um
trabalhador que é executado no serviço do {{site.data.keyword.containershort_notm}} é descrito
como segue: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

Em que

<table>
  <caption>Campos obrigatórios para definir uma métrica de carregamento de um trabalhador </caption>
  <tr>
    <th>Campo</th>
	<th>Descrição</th>
	<th>Valor</th>
  </tr>
  <tr>
    <td>Fonte</td>
	  <td>Este é um nome reservado. As métricas sob esta hierarquia são provenientes de aplicativos e serviços do
{{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo de nuvem</td>
	  <td>Indica o tipo do Cloud. </td>
	  <td>Para a nuvem pública do {{site.data.keyword.Bluemix_notm}}, o valor é: *public*</td>
  </tr>
  <tr>
    <td>Nome do serviço</td>
	  <td>Define o nome do serviço no {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Para apps CF, o valor é: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Região</td>
	  <td>Define a região em que o contêiner está em execução.</td>
	  <td>Para a região Sul dos EUA, o valor é: *us-south* <br>Para a região do Reino Unido, o valor
é: *united-kingdom*  <br>Para Alemanha, o valor é: *frankfurt* <br>Para Sydney, o
valor é: *sydney* </td>
  </tr>
  <tr>
    <td>Nome do cluster</td>
	<td>O nome do cluster a ser monitorado.</td>
	<td></td>
  </tr>
  <tr>
    <td>Origem de métrica</td>
	<td>A origem dos dados.</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>Nome do trabalhador</td>
	<td>O nome do trabalhador.</td>
	<td></td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	<td>O tipo de métrica.</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica a ser exibida.</td>
	  <td>*avg-1*, *avg-5*, *avg-15*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Funções de consulta que podem ser selecionadas para visualizar uma métrica de contêiner no painel. </td>
    <td>[Functions ![(Ícone de link externo)](../../../icons/launch-glyph.svg "Ícone de link externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Por exemplo, uma consulta para monitorar o uso de CPU para um trabalhador que está em execução em um
cluster do Kubernetes na região sul dos EUA é definida como segue:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## Formato de consulta para as métricas da memória coletadas para contêineres
{: #mem_containers}

O formato de uma consulta que você define no Grafana para monitorar uma métrica de memória para um
contêiner que é executado no serviço do {{site.data.keyword.containershort_notm}} é descrito
como segue: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

Em que

<table>
  <caption>Campos obrigatórios para definir uma métrica de memória para um contêiner</caption>
  <tr>
    <th>Campo</th>
	<th>Descrição</th>
	<th>Valor</th>
  </tr>
  <tr>
    <td>Fonte</td>
	  <td>Este é um nome reservado. As métricas sob esta hierarquia são provenientes de aplicativos e serviços do
{{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo de nuvem</td>
	  <td>Indica o tipo do Cloud. </td>
	  <td>Para a nuvem pública do {{site.data.keyword.Bluemix_notm}}, o valor é: *public*</td>
  </tr>
  <tr>
    <td>Nome do serviço</td>
	  <td>Define o nome do serviço no {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Para apps CF, o valor é: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Região</td>
	  <td>Define a região em que o contêiner está em execução.</td>
	  <td>Para a região Sul dos EUA, o valor é: *us-south* <br>Para a região do Reino Unido, o valor
é: *united-kingdom*  <br>Para Alemanha, o valor é: *frankfurt* <br>Para Sydney, o
valor é: *sydney* </td>
  </tr>
  <tr>
    <td>Nome do cluster</td>
	<td>O nome do cluster a ser monitorado.</td>
	<td></td>
  </tr>
  <tr>
    <td>Origem de métrica</td>
	<td>A origem dos dados.</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>O namespace no qual o contêiner é implementado em um cluster do Kubernetes.</td>
	<td></td>
  </tr>
   <tr>
    <td>Nome do pod</td>
	<td>Nome do módulo.</td>
	<td></td>
  </tr>
  <tr>
    <td>Nome do contêiner</td>
	  <td>O nome do contêiner.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
  	<td>O tipo de métrica.</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica a ser exibida.</td>
	  <td>*limit*, *current*, *usage-pct*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Funções de consulta que podem ser selecionadas para visualizar uma métrica de contêiner no painel. </td>
    <td>[Functions ![(Ícone de link externo)](../../../icons/launch-glyph.svg "Ícone de link externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Por exemplo, uma consulta para monitorar o uso de memória para um contêiner que está em execução em um
cluster do Kubernetes na região sul dos EUA é definida como segue:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
