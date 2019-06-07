---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# {{site.data.keyword.cloud_notm}} でのユーザー・アクセスの管理
{: #iam}

{{site.data.keyword.iamlong}} (IAM) を使用すると、ユーザーを安全に認証し、{{site.data.keyword.cloud_notm}} ですべてのクラウド・リソースへのアクセスを一貫して制御できます。 
{:shortdesc}

**ご使用のアカウント内の {{site.data.keyword.mon_full_notm}} サービスにアクセスするすべてのユーザーには、IAM ユーザー役割が定義されたアクセス・ポリシーを割り当てる必要があります。** そのポリシーによって、選択したサービスまたはインスタンスのコンテキスト内でユーザーが実行できるアクションが決まります。 許可されるアクションは、サービス上で実行できる操作としてカスタマイズされて定義されます。 その後、操作は IAM ユーザー役割にマップされます。

*ポリシー* により、さまざまなレベルでアクセス権限を付与できます。 以下のようなオプションがあります。 

* アカウント内のすべての IAM 対応サービスに対するアクセス権限
* アカウント内の単一地域内のサービスのすべてのインスタンスに対するアクセス権限
* アカウント内の個別のサービス・インスタンスに対するアクセス権限
* リソース・グループのコンテキスト内のサービスのすべてのインスタンスに対するアクセス権限
* リソース・グループのコンテキスト内の単一の地域のサービスのすべてのインスタンスに対するアクセス権限
* リソース・グループのコンテキスト内のすべての IAM 対応サービスに対するアクセス権限

*役割* によって、ユーザーまたは serviceID が実行できるアクションが定義されます。 {{site.data.keyword.cloud_notm}} の役割には、さまざまなタイプがあります。
* *プラットフォーム管理役割* により、ユーザーはプラットフォーム・レベルでサービス・リソースに対するタスクを実行できます。例えば、サービスに対するユーザー・アクセス権限の割り当て、サービス ID の作成または削除、インスタンスの作成、他のユーザーへのサービスのポリシーの割り当て、アプリケーションへのインスタンスのバインドなどを実行できます。
* *サービス・アクセスの役割* は、サービスの API を呼び出すためのさまざまなレベルの権限をユーザーに割り当てることを可能にします。

**一連のユーザーとサービス ID を、IAM 権限を簡単に管理できるように単一のエンティティーに編成するには、**アクセス・グループ*を使用します。** 個々のユーザーまたはサービス ID ごとに同じアクセス権限を複数回割り当てるのではなく、単一のポリシーをグループに割り当てることができます。
{: tip}


## アクセス・グループを使用してアクセス権限の管理
{: #iam_groups}

アクセス・グループを使用してアクセス権限の管理やユーザーへの新しいアクセス権限の割り当てを行うには、アカウント所有者であるか、アカウント内のすべての ID およびアクセス対応サービスの管理者またはエディターであるか、または、IAM アクセス・グループ・サービスに割り当てられた管理者またはエディターである必要があります。 

{{site.data.keyword.cloud_notm}} でアクセス・グループを管理するには、以下のいずれかのアクションを選択します。

* [アクセス・グループを作成](/docs/iam?topic=iam-groups#create_ag)します。
* [アクセス権をグループに割り当て](/docs/iam?topic=iam-groups#access_ag)ます。


## ユーザーにポリシーを直接割り当ててアクセス権を管理する
{: #iam_users}

IAM ポリシーを使用して、アクセス権限の管理またはユーザーの新規アクセス権限の割り当てを行うには、アカウント所有者であるか、アカウント内のすべてのサービスの管理者であるか、または、特定のサービスまたはサービス・インスタンスの管理者である必要があります。 

{{site.data.keyword.cloud_notm}} で IAM ポリシーを管理するには、以下のいずれかのアクションを選択します。

* ユーザーの権限を変更するには、[既存のアクセス権限の編集](/docs/iam?topic=iam-iammanidaccser#edit_existing)を参照してください。
* ユーザーに権限を付与するには、[新しいアクセス権限の割り当て](/docs/iam?topic=iam-iammanidaccser#assign_new_access)を参照してください。
* 権限を取り消すには、[アクセス権限の削除](/docs/iam?topic=iam-iammanidaccser#removing_access)を参照してください。
* ユーザーの権限を確認するには、[割り当てられたアクセス権限の確認](/docs/iam?topic=iam-iammanidaccser#review_your_access)を参照してください。


## {{site.data.keyword.cloud_notm}} プラットフォームの役割
{: #iam_platform}

以下の表を使用して、以下のプラットフォーム・アクションを実行できるように {{site.data.keyword.cloud_notm}} のユーザーに付与できるプラットフォーム役割を特定します。

| プラットフォーム・アクション                                                        | {{site.data.keyword.cloud_notm}} プラットフォームの役割    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `他のアカウント・メンバーに、サービスを処理するためのアクセス権限を付与します`           | 管理者                                        | 
| `サービス・インスタンスをプロビジョンします`                                          | 管理者</br>エディター                            | 
| `サービス・インスタンスを削除します`                                             | 管理者</br>エディター                            | 
| `サービス ID を作成します`                                                   | 管理者</br>エディター                            |
| `サービス・インスタンスの詳細を表示します`                                    | 管理者 </br>エディター </br>オペレーター </br>ビューアー  | 
| `「プログラム識別情報モニタリング (Observability Monitoring)」ダッシュボードでサービス・インスタンスを表示します`      | 管理者 </br>エディター </br>オペレーター </br>ビューアー  | 
{: caption="表 1. IAM ユーザーの役割とアクション" caption-side="top"}



## Sysdig の役割
{: #iam_sysdig_roles}

以下の表は、Sysdig の役割と役割ごとのアクションを示しています。

| アクション                                                                    | Sysdig の役割                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Reset the Sysdig access key`                                              | 管理者                                                |
| `Manage users`                                                             | 管理者                                                |
| `Create, configure, and delete teams`                                      | 管理者                                                |
| `Configure and remove notifications channels`                              | 管理者                                                | 
| `Configure and remove Sysdig agents`                                       | 管理者                                                |
| `Create, delete, and edit content in the Sysdig web UI`                    | 管理</br>ユーザー                         |  
| `View metrics through the Sysdig Web UI`                                   | 管理</br>ユーザー                         |  
| `Create and delete alerts`                                                 | 管理</br>ユーザー                         | 
| `Create and delete captures`                                               | 管理</br>ユーザー                         |   
{: caption="表 2. Sysdig の役割とアクション" caption-side="top"}


## Sysdig の役割の {{site.data.keyword.cloud_notm}} の役割へのマップ
{: #iam_sysdig}

以下の表で、{{site.data.keyword.cloud_notm}} の役割の Sysdig の役割へのマップを確認してください。

| 役割のタイプ        | 役割               | Sysdig の役割                | 説明                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| プラットフォームの役割       | 管理者      | 管理者                      | ユーザーに Sysdig 管理者権限を付与します。   | 
| サービス役割        | 管理者            | 管理者                      | ユーザーに Sysdig 管理者権限を付与します。   | 
| サービス役割        | ライター             | ユーザー                       | ユーザーに Sysdig ユーザー権限を付与します。    |
| サービス役割        | リーダー             |                            | 権限は付与されません。                 |
{: caption="表 3. Sysdig の役割" caption-side="top"}


