---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# Gerenciando capturas
{: #captures}

Uma captura é um arquivo de rastreio que pode ser gerado para analisar o que acontece em um host durante um prazo. Por exemplo, é possível usá-lo para analisar interações de componentes ou gargalos. No serviço {{site.data.keyword.mon_full_notm}}, é possível criar, explorar, fazer download e excluir *capturas* para nós individuais. 
{:shortdesc}

Para obter mais informações, consulte [Capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


## Criando uma Captura
{: #captures_create}

Você cria uma captura na visualização *Explorar*.

Conclua as etapas a seguir para criar um arquivo de captura:

1. Navegue para a seção *EXPLORAR* na IU da web. [Saiba mais](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Clique no ícone do host do comutador ![Ícone do host do comutador](images/switch_hosts.png).

3. Selecione um host ou um contêiner.

4. Clique no ícone de ações ![Ícone de reticências](images/actions.png) e
selecione **Captura do Sysdig**.

    A janela *Captura do Sysdig* é aberta.

5. Na janela *Captura do Sysdig*, defina os parâmetros a seguir:

    1. No campo *Caminho e nome da captura*, insira o nome do arquivo de captura. É possível deixar o valor padrão ou modificá-lo. O nome padrão inclui a data e o registro de data e hora de quando a captura é criada. 

    2. Configure um *Prazo* para especificar o número de segundos para reunir dados. O tempo de captura padrão é 15 segundos. O tempo máximo de captura é de 86.400 segundos (24 horas). 

    3. (Opcional) Inclua um filtro para restringir a quantia de informações de rastreio que são coletadas. 

6. Clique em  ** Iniciar captura **. O agente Sysdig é sinalizado para iniciar uma captura e enviar de volta o arquivo de rastreio resultante. 

7. Clique em **Acessar a página de capturas** para exibir a lista de capturas na seção *Capturas* da IU da web. 

A página *Capturas* mostra uma tabela que lista o nome do arquivo de captura, o host do qual ele foi recuperado, o prazo e o tamanho da captura. 

O status de um arquivo de captura pode ser qualquer um dos valores a seguir:
* ` Solicitado `: um arquivo está sendo gerado.
* `Transferido por upload`: um arquivo está disponível para download e análise.
* `Erro`: um arquivo não está disponível devido a um tempo limite, dados que nunca foram recebidos ou um erro do agente.



## Excluindo uma Captura
{: #captures_delete}

Conclua as etapas a seguir para excluir um arquivo de captura:

1. Navegue para a seção *CAPTURAS* na IU da web. [Saiba mais](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifique e selecione o arquivo de captura que você deseja excluir.
3. Clique em **Excluir**.



## Explorando uma Captura
{: #captures_explore}

Conclua as etapas a seguir para explorar um arquivo de captura:

1. Navegue para a seção *CAPTURAS* na IU da web. [Saiba mais](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifique e selecione o arquivo de captura que contém os dados para o host que você deseja analisar.
3. Clique em  ** EXPLORE **.



## Fazendo download de uma captura
{: #captures_download}

Conclua as etapas a seguir para fazer download de um arquivo de captura:

1. Navegue para a seção *CAPTURAS* na IU da web. [Saiba mais](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifique e selecione o arquivo de captura que contém os dados dos quais você deseja fazer download.
3. Clique em  ** DOWNLOAD **.


## Chisels
{: #captures_chisels}

Um chisel Sysdig é um script escrito em Lua, uma linguagem de script. É possível usá-lo para analisar dados em um arquivo de captura. 

Para obter mais informações, veja [Guia do usuário do Chisels ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}.



## Csysdig
{: #captures_csysdig}

A Csysdig é uma ferramenta de software livre para Linux que é projetada para monitoramento e depuração. É possível usá-la para analisar arquivos de captura. 

Para obter mais informações, consulte os recursos a seguir:
* [Blog da Csysdig ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Vídeo da Csysdig ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


