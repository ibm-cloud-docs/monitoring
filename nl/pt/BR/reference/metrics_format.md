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


# Formato geral
{: #metrics_format}

As consultas que você define no Grafana para monitorar um serviço do {{site.data.keyword.Bluemix}}
devem estar em conformidade com o formato a seguir: 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

em que [service fields] representam os campos específicos da consulta de métrica de um serviço ou app
CF. 

<table>
  <caption>Campos comuns em uma consulta</caption>
  <tr>
    <th>Campo</th>
	<th>Descrição</th>
	<th>Valor</th>
  </tr>
  <tr>
    <td>Fonte</td>
	<td>Este é um nome reservado. As métricas sob esta hierarquia são provenientes de serviços do
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
	  <td>Para o {{site.data.keyword.containershort}}, o valor é: *containers-kubernetes*</td>
  </tr>
  <tr>
    <td>Região</td>
	  <td>Define a região em que o contêiner está em execução.</td>
	  <td>Para a região Sul dos EUA, o valor é: *us-south* <br>Para a região do Reino Unido, o valor
é: *united-kingdom*  <br>Para Alemanha, o valor é: *frankfurt* <br>Para Sydney, o
valor é: *sydney* </td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	<td>O tipo de métrica.</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	<td>O subtipo da métrica.</td>
	<td>Por exemplo: *usage*, *num-cores*, *usage-pct*,
*usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Funções de consulta que podem ser selecionadas para visualizar uma métrica de contêiner no painel. </td>
    <td>[Functions ![(Ícone de link externo)](../../../icons/launch-glyph.svg "Ícone de link externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




