---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, panels

subcollection: Sysdig

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


# Gerenciando painéis
{: #panels}

Use um painel para exibir uma métrica ou grupo de métricas em um painel. É possível copiar, mudar o escopo, duplicar, excluir, exportar e explorar painéis.
{:shortdesc}

É possível usar qualquer um dos tipos de painel a seguir:

| Tipo | Descrição |
|------|-------------|
| `Line` | Use esse painel para visualizar as tendências ao longo do tempo para uma ou mais métricas.  |
| `Area` | Use esse painel para visualizar as tendências ao longo do tempo para uma ou mais métricas.  |
| `Top list` | Use esse painel para comparar uma métrica entre grupos de entidades. O gráfico de barras é classificado em ordem decrescente.  |
| `Histogram` | Use esse painel para visualizar a distribuição de frequência de uma métrica em depósitos.  |
| `Topology` | Use esse painel para visualizar a infraestrutura como um mapa de topologia e as relações entre entidades no mapa.  |
| `Number` | Use esse painel para visualizar um único número que representa o valor de uma métrica agregada ao longo do tempo para uma ou mais entidades.  |
| `Table` | Use esse painel para exibir dados numéricos para sua infraestrutura com base em métricas e segmentos.  |
| `Text` | Use esse painel para incluir texto. Use redução para incluir seu texto.  |
{: caption="Tabela 1. Tipos de painéis" caption-side="top"} 



## Copiar um painel em um painel
{: #panels_copy}

Conclua as etapas a seguir para copiar um painel:

1. Navegue para a seção *PAINEL** na IU da web. Selecione um painel. Em seguida, identifique o painel que exibe a métrica que você deseja copiar.

2. Selecione o ícone *Mais opções* ![Ícone de reticências](images/actions.png) e selecione **Copiar painel** ![Ícone de cópia](images/actions.png).

3. Selecione um dos painéis que estão listados ou insira um nome para um novo painel. 

4. Clique em  ** Copiar e Abrir **.



## Mudar o escopo de um painel
{: #panels_scope}

Conclua as etapas a seguir para mudar o escopo de um painel:

1. Navegue para a seção *PAINEL** na IU da web. Selecione um painel. Em seguida, identifique o painel que exibe a métrica para a qual você deseja mudar o escopo.

2. No painel, clique em **Editar escopo** para mudar o escopo padrão. 

    Por padrão, **Em toda parte** é selecionado.
    
3. Selecione o escopo. 

4. Opcionalmente, clique em **Substituir os escopos do painel customizado** para substituir o escopo de todos os painéis com um escopo customizado definido. 

    **Nota: não é possível desfazer essa ação.** 

    Para reconfigurar o escopo do painel para a infraestrutura inteira ou para atualizar o escopo de um painel existente para a infraestrutura inteira, selecione **Em toda parte**.
    {: tip}

5. Clique em **Salvar**.



## Painel duplicado
{: #panels_duplicate}

Conclua as etapas a seguir para duplicar um painel no painel atual:

1. Navegue para a seção *PAINEL** na IU da web. Selecione um painel. Em seguida, identifique o painel que exibe a métrica que você deseja copiar.

2. Selecione o ícone *Mais opções* ![Ícone de reticências](images/actions.png) e selecione **Duplicar painel**![Ícone de cópia](images/duplicate.png).


## Excluir painel
{: #panels_delete}

Conclua as etapas a seguir para excluir um painel no painel atual:

1. Navegue para a seção *PAINEL** na IU da web. Selecione um painel. Em seguida, identifique o painel que exibe a métrica que você deseja copiar.

2. Selecione o ícone *Mais opções* ![Ícone de reticências](images/actions.png) e selecione **Excluir painel**![Ícone de cópia](images/delete.png).

3. Clique em **Sim, excluir painel** para confirmar a exclusão do painel.



## Exportar dados de um painel
{: #panels_export}

Considere as informações a seguir ao exportar dados:

* É possível exportar dados para um **arquivo json** por meio de um gráfico de linha.
* É possível exportar dados para um **arquivo csv** por meio de um gráfico de tabela ou de um gráfico de linha.

Conclua as etapas a seguir para exportar dados de um painel:

1. Navegue para a seção *PAINEL** na IU da web. Selecione um painel. Em seguida, identifique o painel que exibe a métrica que você deseja copiar.

2. Selecione o ícone *Mais opções* ![Ícone de reticências](images/actions.png).

3. Escolha uma das opções a seguir:

    * Selecione **Exportar JSON** para exportar dados para um arquivo formatado json.

    * Selecione **Exportar CSV** para exportar dados para um arquivo formatado csv.

4. Clique em  ** Salvar o arquivo **.




## Criar Alerta
{: #panels_alert}

É possível criar alertas diretamente de um painel.

Conclua as etapas a seguir para criar um alerta:

1. Navegue para a seção *PAINEL** na IU da web. Selecione um painel. Em seguida, identifique o painel que exibe a métrica que você deseja copiar.

2. Selecione o ícone *Mais opções* ![Ícone de reticências](images/actions.png).

3. Selecione  ** Criar Alerta **.

4. Configure o alerta.

5. Clique em  ** Criar **.


