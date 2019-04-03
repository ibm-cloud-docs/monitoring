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


# Analisar métricas no Grafana para um app CF
{: #cfapps_metrics}

Use este tutorial para aprender como usar o serviço do {{site.data.keyword.monitoringlong}}
para monitorar o desempenho de um app Cloud Foundry (CF) que é executado no
{{site.data.keyword.Bluemix_notm}} Public. 
{:shortdesc}


## Objetivos
{: #objectives}

Aprenda como procurar e analisar métricas de um app CF:

1. Implementar um app CF.
2. Ativar o Grafana e configurar o domínio do {{site.data.keyword.monitoringshort}} no qual
é possível visualizar as métricas do app CF.
3. Procurar por e analisar as métricas deum app CF que é executado em um espaço do
{{site.data.keyword.Bluemix_notm}}.

Este tutorial supõe que você está trabalhando na região Sul dos EUA.


## Pré-requisitos
{: #cfapps_prereqs}

1. Ser membro ou proprietário de uma conta do
{{site.data.keyword.Bluemix_notm}} com permissões para fornecer serviços em um espaço,
implementar apps CF e consultar métricas no {{site.data.keyword.Bluemix_notm}} por meio do
serviço do {{site.data.keyword.monitoringshort}}.

    Seu ID do usuário para o {{site.data.keyword.Bluemix_notm}} deve ter uma função CF para o
espaço no qual o serviço do {{site.data.keyword.monitoringshort}} e o app CF são fornecidos. A função
necessária é *desenvolvedor*.
    
    Para obter mais informações, consulte
[Concedendo
a um usuário uma função CF usando a UI do IBM Cloud](/docs/services/cloud-monitoring/security/assign_policy.html#grant_permissions_ui_space).

2. Forneça o serviço do {{site.data.keyword.monitoringshort}} em um espaço no qual você tenha permissões para fornecimento de serviços na região Sul dos EUA.

    Para obter mais informações, consulte
[Fornecendo o
serviço do {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/how-to/provision.html#provision).

## Etapa 1: Conceder ao usuário permissões para trabalhar com apps CF e com o serviço
do {{site.data.keyword.monitoringshort}}
{: #cfapps_step1}

Para conceder a um usuário permissões para implementar apps CF em um espaço ou para visualizar métricas
em um domínio de espaço, deve-se designar a esse usuário uma função do CF que descreva as ações que esse usuário
pode executar com o serviço do {{site.data.keyword.monitoringshort}} no espaço e no
{{site.data.keyword.Bluemix_notm}}. 

**Nota:** este tutorial supõe que você seja o proprietário da conta ou que tenha
permissões para incluir funções em seu ID do usuário. Se você não tiver permissões, solicite ao proprietário
para concluir esta etapa.

Conclua as etapas a seguir para conceder a um usuário permissões para concluir o tutorial:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Localize seu nome de usuário na lista e clique em **Gerenciar usuários** no
menu *Ações*.

4. Selecione **Acesso ao Cloud Foundry** e, em seguida, selecione
**Designar uma organização**.

5. Digite os seguintes valores: 

    <table>
      <caption>Lista de valores a selecionar</caption>
      <tr>
        <th>Campo</th>
        <th>Valor</th>
      </tr>
      <tr>
        <td>Organização</td>
        <td>MyOrg</td>
      </tr>
      <tr>
        <td>Função de organização</td>
        <td>Nenhuma função de organização</td>
      </tr>
      <tr>
        <td>Região</td>
        <td>Sul dos Estados Unidos</td>
      </tr>
      <tr>
        <td>Espaço</td>
        <td>dev</td>
      </tr>
      <tr>
        <td>Função de espaço</td>
        <td>revelador</td>
      </tr>
    </table>
	
6. Clique em **Salvar função**.
 

## Etapa 2: Implementar um app CF
{: #cfapps_step2}

Conclua as etapas no console do {{site.data.keyword.Bluemix_notm}}:

1. Clique em **Catálogo** na barra de ferramentas do
{{site.data.keyword.Bluemix_notm}}.

2. Clique em **Cloud Foundry Apps > Liberty for Java**. 

3. Digite as informações a seguir:

    * **Nome do app**: o nome do aplicativo. Deve ser exclusivo.
    * **Região**: escolha Sul dos EUA.
    * **Organização**: escolha a organização na qual você forneceu o serviço
do {{site.data.keyword.monitoringshort}}
    * **Espaço**: escolha o espaço no qual você forneceu o serviço
do {{site.data.keyword.monitoringshort}}

3. Clique em **Criar**.

Assim que o app CF está em execução, as métricas são coletadas e encaminhadas para o serviço
do {{site.data.keyword.monitoringshort}}.

## Etapa 3: Ativar o Grafana e configurar o domínio de métricas
{: #cfapps_step3}

Ative o Grafana em um navegador e configure o domínio do {{site.data.keyword.monitoringshort}}
no qual é possível visualizar as métricas do app CF.

1. Em um navegador, ative o Grafana. 

    Insira a URL de serviço do {{site.data.keyword.monitoringshort}} para a
região em que o serviço do {{site.data.keyword.monitoringshort}} é fornecido.
    
    Para obter as URLs por região, consulte
[URLs para o serviço de
monitoramento](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Por exemplo, para a região Sul dos EUA, ative:
[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Configure o domínio do {{site.data.keyword.monitoringshort}} no qual é possível
visualizar as métricas de cluster.

    No Grafana, selecione seu ID. Em seguida, verifique se você está na conta correta e escolha
`Domain = space`.

    Verifique se o nome da organização e o nome do espaço correspondem àqueles nos quais você
implementou o app CF e forneceu o serviço do {{site.data.keyword.monitoringshort}}.


## Etapa 4: Criar um painel Grafana para monitorar uma métrica
{: #cfapps_step4}


Conclua as etapas a seguir para criar um novo painel no Grafana:

1. Selecione a alternância de barra de menus lateral ![Barra de menus lateral do Grafana](images/grafana_settings.gif "Barra de menus lateral do Grafana").
2. Selecione **Painéis**.
3. Clique em **Novo**

Um painel se abre. O painel inclui uma linha vazia que está pronta para configuração.

![Grafana dashboard](images/grafana4_f1.gif "Grafana dashboard")

No Grafana, você inclui linhas para dividir o painel em seções. Uma linha agrupa um ou mais painéis. Dentro de uma linha, um painel é a menor unidade de visualização que pode ser configurada para exibir dados para uma métrica; por exemplo, é possível escolher um painel de gráfico ou um painel de tabela. É possível arrastar e soltar painéis para reorganizá-los em um dashboard. Os dados que um painel exibe são configurados por meio de consultas. É possível definir uma ou mais consultas em um painel. Cada consulta representa um conjunto diferente de dados. Também é possível configurar o intervalo de tempo para um painel. Normalmente, o intervalo de tempo é configurado pelo selecionador de tempo do *Dashboard*.

Defina a consulta que filtra os dados que são exibidos no gráfico. Essa consulta monitora a porcentagem
de utilização da CPU para o limite do contêiner.

Para obter informações sobre o formato da consulta, consulte
[Formato
de consulta do Grafana para apps CF](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format).
    
1. Inclua um painel de *Graph* para monitorar os nanossegundos de tempo de CPU em todos os núcleos para um contêiner.
    
    1. Selecione **Gráfico**.
    
    2. Clique no título do gráfico e, em seguida, selecione **Editar**.
    
        O *Métricas* guia é aberta. É possível ver aqui a origem de dados padrão.
    
        ![Painel de gráfico incluindo guias de configuração](images/grafana4_f2.gif "Painel de gráfico incluindo guias de configuração")
    
2. Defina a consulta que filtra os dados que são exibidos no gráfico. 
    
    Na guia *Métricas*, selecione **Incluir consulta**. <br>Uma entrada de consulta é incluído. Cada consulta é rotulada com uma letra.
    
    ![New query entry](images/grafana4_query_f1.gif "New query entry")
        
    1. Clique em **Selecionar métrica** e, em seguida, escolha a origem:
`ibmcloud`.
    
    2. Clique em **Selecionar métrica** e, em seguida, escolha o tipo de nuvem:
`public`.
    
    3. Clique em **Selecionar métrica** e, em seguida, escolha
`cloud-foundry`.
    
    4. Clique em **Selecionar métrica** e, em seguida, escolha a região em que você
está trabalhando, por exemplo, `us-south` para a região Sul dos EUA.
    
    5. Clique em **Selecionar métrica** e, em seguida, escolha o nome do app CF, por
exemplo, `logtester`.
    
    6. Clique em **Selecionar métrica** e, em seguida, escolha o índice da instância
do app CF, por exemplo, `0`.

    7. Clique em **Selecionar métrica** e, em seguida, escolha
`container`.
    
    9. Clique em **Selecionar métrica** e, em seguida, escolha uma métrica. Para
monitorar a *Porcentagem de uso da CPU* de um contêiner, escolha
`cpu-utilization`.

    10. Clique na imagem de mais ![Ícones Incluir](images/grafana_plus_image.gif "Imagem de mais") e escolha uma função. Será possível incluir uma função para transformar, combinar e executar cálculos nos dados que estiverem disponíveis para uma métrica.
        
        Por exemplo, é possível incluir a função **alias(newName)** para incluir um alias para uma métrica. Esse alias é usado para imprimir uma sequência em vez do nome da métrica na legenda que é exibida no gráfico.
        
        Para incluir um alias para sua métrica, conclua as etapas a seguir:
        
        1. Clique no símbolo de mais.
        2. Selecione **Especial**. 
        3 Selecione **alias**.
        4. Insira uma sequência, por exemplo, `My sample metric`.
        

## Etapa 5: Salvar o painel
{: #cfapps_step5}

Salve o painel para reutilização posterior.

1. Clique na imagem de painel salvar ![Imagem de painel salvar](images/grafana_save_image.gif "Imagem de painel salvar").

    ![Save dashboard](images/grafana_save_dashboard.gif "Save dashboard")

2. Insira o nome do painel.
3. Clique em **Salvar**.


## Etapas Seguintes
{: #cfapps_next_steps}

Defina um alerta para uma métrica. Para obter mais informações, consulte [Configurando alertas](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).
