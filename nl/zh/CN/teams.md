---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

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

# 使用团队
{: #teams}

{{site.data.keyword.mon_full_notm}} 实例的管理员或管理者可以创建、删除、添加成员以及更改该实例中团队的作用域。
{:shortdesc} 

{{site.data.keyword.mon_full_notm}} 实例的管理员或管理者必须先切换到*监视操作*团队，然后才能创建团队并管理现有团队。
{: tip}

## 创建团队
{: #teams_create}

要创建团队，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**监视操作**。然后，选择**设置**。

3. 选择**团队**。这将显示现有团队的列表。

4. 单击**添加团队**。这将显示团队配置页面。

5. 配置团队详细信息。 

    * 选择颜色。

    * 输入团队的名称。

    * [可选] 输入此团队的描述。

    * [可选] 如果希望此团队成为新用户的缺省团队，请设置**缺省团队**参数。

    * 设置**缺省入口点**以指定在 Web UI 中每次用户登录时打开的视图。有效的入口点为：*探索*视图、*仪表板*视图、*事件*视图、*警报*视图和*设置*视图。缺省情况下，已设置*探索*视图。

6. 配置团队作用域。 

    * [可选] 设置**作用域**以指定团队成员有权访问的数据级别。有效值为*主机*和*容器*。如果此参数设置为*主机*，那么成员可以查看所有主机级别和容器级别的信息。如果此参数设置为*容器*，那么成员只能查看容器级别的信息。

    * 设置**作用域**以限制用户可以查看的数据。可以通过为度量值指定表达式来设置一个或多个条件。缺省情况下，作用域设置为*所有位置*。
	
    * [可选] 启用或禁用 **Sysdig 捕获**。选中此框以允许此团队执行 Sysdig 捕获。捕获文件仅可供此团队的成员查看。**注：** 捕获包含主机上每个容器的详细信息，与团队的作用域无关。

    * [可选] 启用或禁用**基础架构事件**。选中此框以允许成员查看每个用户和 Sysdig 代理程序中的所有定制基础架构事件。未选中时，用户可以查看专门向此团队发送的基础架构事件。 

6. 向团队添加成员。单击**分配用户**。搜索用户并添加该用户。



## 更改团队的作用域
{: #teams_scope}

要更改可供团队成员查看的数据的作用域，请完成以下步骤： 

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**监视操作**。然后，选择**设置**。

3. 选择**团队**。这将显示现有团队的列表。

4. 确定并选择团队。这将显示该团队的详细信息。

5. 在*可视性*部分中更改配置详细信息。

6. 单击**保存**。 


## 向团队添加用户
{: #teams_users}

要向团队添加成员，请完成以下步骤： 

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**监视操作**。然后，选择**设置**。

3. 选择**团队**。这将显示现有团队的列表。

4. 确定并选择团队。这将显示该团队的详细信息。

5. 单击*团队用户*部分中的**分配用户**。

6. 单击**保存**。 


## 删除团队
{: #teams_delete}

无法删除缺省团队**监视操作**。 

要删除团队，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**监视操作**。然后，选择**设置**。

3. 选择**团队**。这将显示现有团队的列表。

4. 确定并选择要删除的团队。这将显示该团队的详细信息。

5. 单击**删除团队**。

**注：**删除团队时，仅属于此团队的用户会被移至缺省团队。



