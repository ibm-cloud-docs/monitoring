---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

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


# Venda
{: #pricing_plans}

Há diferentes planos de precificação disponíveis para uma instância do {{site.data.keyword.mon_full_notm}}.
{:shortdesc}
 

| Planos            | Camada         | Coleta de Dados  |
|------------------|--------------|------------------|
| `Trial`          |              | Os dados são coletados para um máximo de 20 contêineres por nó ou para 200 métricas customizadas por nó somente por 30 dias. |
| `Graduated tier` | `Basic`      | Os dados são coletados para um máximo de 20 contêineres por nó ou para 200 métricas customizadas por nó. |
| `Graduated tier` | `Pro`        | Os dados são coletados para um máximo de 50 contêineres por nó ou para 500 métricas customizadas por nó. |
| `Graduated tier` | `Advanced`   | Os dados são coletados para um máximo de 110 contêineres por nó ou para 1.000 métricas customizadas por nó. |
{: caption="Tabela 1. Lista de planos de serviços" caption-side="top"} 


**Nota:** um nó pode ser um host, um contêiner, uma máquina virtual, um bare metal ou qualquer origem de métricas na qual você instala um agente Sysdig.

Quando o número de contêineres por nó ou o número de métricas está acima do limite do plano de camada graduada durante um período de tempo, a detecção de camada automática é aplicada. Uma notificação de alerta será acionada após a configuração de notificação de uso de faturamento se você ativar o alerta a seguir **[{{site.data.keyword.IBM_notm}}]: Usage Mudança de camada**

É possível solicitar uma **cotação de preço customizado** para qualquer coisa além do limite superior do *Plano de precificação pago da camada graduada avançada* abrindo um chamado com o [Suporte do IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

Os dados são coletados e retidos de acordo com as diretrizes padrão em todos os planos. Para obter mais informações, consulte [coleta de dados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) e [retenção de dados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


## Verificando seu uso
{: #pricing_usage}

Para monitorar como o serviço {{site.data.keyword.mon_full_notm}} é usado e os custos associados a seu uso, consulte [Visualizando seu uso](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Ativando o alerta que notifica sobre uma mudança de camada
{: #pricing_alert}

Para ser notificado quando há uma mudança de camada, deve-se ativar o alerta a seguir: **[{{site.data.keyword.IBM_notm}}]: Usage Mudança de camada**

Conclua as etapas a seguir para ativar um alerta:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
2. Crie um canal de notificação. Para obter mais informações, consulte [Configurando um canal de notificação](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create). 
3. Clique em **ALERTAS** para navegar para a seção *Alertas*.
2. Procure **[IBM]: Usage Mudança de camada**.
3. Edite o alerta para incluir o canal de notificação.
4. Clique em **Salvar**.



## Como o alerta de plano de serviço é gerado?
{: #pricing_how}

Para ser notificado quando há uma mudança de camada, deve-se ativar o alerta a seguir: **[{{site.data.keyword.IBM_notm}}]: Usage Mudança de camada**

**Nota:** quando você ativa esse alerta, deve-se especificar os canais de notificação nos quais deseja ser notificado.

O uso é calculado como a média do número de nós e as métricas amostrados a cada 10 segundos durante a hora anterior. Pequenas, flutuações de curta duração não estão incluídas. A diferença entre o uso anterior e o atual acontece uma vez por hora.

Os limites definidos são configurados da maneira a seguir:

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [ 21, 50 ]
    Advanced = [51, 100]
  }
  MetricDensity {
    Basic = [0, 200]
    Pro = [ 201, 500 ]
    Advanced = [501, 1000]
}
```
{: screen}

A notificação de alerta é gerada conforme a seguir:
1. A cada hora, se o número de contêineres por nó em uma camada aumentar, um evento customizado será gerado.
2. A condição de alerta verifica quaisquer eventos customizados que informam sobre mudanças no número de contêineres por nó. Se localiza um evento em que o número de contêineres em uma camada aumenta a partir da última vez que o uso foi calculado, ela envia uma notificação.

A frequência do alerta é uma vez a cada hora. Para um nó flutuante, a frequência do alerta é no máximo a cada duas horas.

Observe que o alerta é gerado somente se um nó se move da camada *Basic* para a camada *Pro* ou para a camada *Advanced*. 



### Exemplos
{: #pricing_examples}

** Amostra 1 ** 

Se a contagem média do contêiner for a seguinte: 

| Horas     | Número de contêineres | Descrição                                                                   | Um alerta foi gerado? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10h00    | 18                   | A camada está configurada como **Basic**.                                                     | Não                     |
| 11h00    | 21                   | O número de contêineres está acima da camada *Basic*. A camada é movida para **Pro**.            | Sim                    |
| 12h00    | 19                   | O número de contêineres está abaixo da camada *Basic*. A camada se move de volta para **Basic**.     | Não                    |
| 13h00    | 20                   | Nenhuma mudança de camada. A camada está configurada como **Basic**.                                     | Não                     |
{: caption="Tabela 2. Amostra 1" caption-side="top"} 


** Sample2 **

Se a contagem média do contêiner for a seguinte: 

| Horas     | Número de contêineres | Descrição                                                                   | Um alerta foi gerado? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10h00    | 15                   | A camada está configurada como **Basic**.                                                     | Não                     |
| 11h00    | 19                   | A camada está configurada como **Basic**.                                                     | Não                     |
| 12h00    | 20                   | A camada está configurada como **Basic**.                                                     | Não                    |
| 13h00    | 21                   | O número de contêineres está acima da camada *Basic*. A camada é movida para **Pro**.            | Sim                     |
{: caption="Tabela 3. Amostra 2" caption-side="top"}


** Sample3 **

Se a contagem média do contêiner for a seguinte: 

| Horas     | Número de contêineres | Descrição                                                                   | Um alerta foi gerado? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10h00    | 15                   | A camada está configurada como **Basic**.                                                     | Não                     |
| 11h00    | 20                   | A camada está configurada como **Basic**.                                                     | Não                    |
| 12h00    | 21                   | A camada está configurada como **Basic**.                                                     | Sim                    |
| 13h00    | 20                   | O número de contêineres está de volta para a camada *Basic*. A camada é movida para **Pro**.          | Não                     |
{: caption="Tabela 3. Amostra 3" caption-side="top"}



