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


# Otorgar permisos a un usuario
{: #grant_permissions}

En {{site.data.keyword.Bluemix}}, puede asignar uno o varios roles a los usuarios. Estos roles definen qué tareas están habilitadas para dicho usuario para trabajar con el servicio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

Para otorgar permisos a un usuario y que trabaje con métricas, debe añadir una política para dicho usuario que describe las acciones que puede realizar con el servicio {{site.data.keyword.monitoringshort}} en la cuenta. Solo los propietarios de cuentas pueden asignar políticas individuales para los usuarios.


## Asignar una política IAM a un usuario mediante la IU de IBM Cloud 
{: #assign_policy_ui}

Complete los pasos siguientes para otorgar permisos a un usuario para trabajar con el servicio {{site.data.keyword.monitoringshort}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

    Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

4. Pulse **Asignar política de servicio**.

5. Especifique la información sobre la política. La tabla siguiente lista los campos necesarios u opcionales para definir una política: 

    <table>
	  <caption>Lista de campos para configurar una política IAM.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valor</th>
		<th>Estado</th>
	  </tr>
	  <tr>
	    <td>Servicio</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>Obligatorio</td>
	  </tr>
	  <tr>
	    <td>Roles</td>
		<td>Seleccione uno o varios roles de IAM. <br>Los roles válidos son: *administrador*, *operador*, *editor*, y *visor*. <br>Para obtener más información sobre las acciones que están permitidas por rol, consulte [Roles de IAM](/docs/services/cloud-monitoring/security_ov.html#iam_roles).</td>
		<td>Obligatorio</td>
	  </tr>
	  <tr>
	    <td>Regiones</td>
		<td>Puede especificar las regiones en las que se otorgará acceso al usuario para trabajar con métricas. Seleccione **Especificar el contexto de servicio opcional**. A continuación, añada una o más regiones individualmente, o seleccione **Todas las regiones actuales** para otorgar acceso a todas las regiones.</td>
		<td>Opcional</td>
	  </tr>
	</table>
	
6. Pulse **Asignar política**.
	
La política que configure es aplicable a las regiones seleccionadas. 

## Asignación de una política IAM a un usuario mediante la línea de mandatos
{: #assign_policy_commandline}

Complete los pasos siguientes para otorgar acceso a un usuario para ver las métricas mediante la línea de mandatos:

1. (Requisito previo) Instalar la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
   
   Si la CLI está instalada, continúe en el paso siguiente.
	
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Obtenga el ID de cuenta. 

    Ejecute el mandato siguiente para obtener el ID de cuenta:

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	Una lista de cuentas en las que se visualiza los GUID.
	
	Exporte el ID de la cuenta con la que desea otorgar permisos a un usuario. Configure una variable de shell como, por ejemplo, `$acct_id`:
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. Obtenga el ID de {{site.data.keyword.IBM_notm}} del usuario al que desea otorgar permisos.

    1. Visualice los usuarios que están asociados con la cuenta. Ejecute el mandato siguiente:
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. Obtenga el GUID del usuario. **Nota: Este paso debe completarlo el usuario al que tiene previsto otorgar permisos.**
	
	    Por ejemplo, solicite al usuario que ejecute los mandatos siguientes para obtener su ID de usuario:
		
		Obtenga la señal de IAM. Para obtener más información, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli).

        Obtenga los datos de la señal de IAM que se encuentran entre los dos primeros puntos en la señal de IAM. Exporte los datos a una variable de shell como `$user_data`. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Ejecute el mandato siguiente, por ejemplo, para obtener el ID de usuario. Este mandato utiliza jq en este ejemplo para descodificar la información en texto con formato de JSON:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		La salida de la ejecución de este mandato es la siguiente:
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Envíe el ID de usuario, que es el valor del campo *id*, al propietario de cuenta. 
		
	3. Exporte el ID de usuario en una variable de shell como `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Invite el usuario a la cuenta si no es un miembro. Para obtener más información, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

    Por ejemplo, ejecute el mandato siguiente para invitar al usuario xxx@yyy.com a la cuenta zzz@ggg.com:
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Cree un nombre de archivo de política. 

    Por ejemplo, utilice la plantilla siguiente para otorgar permisos en la región EE.UU. sur:
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Nombre del archivo de política: `policy.json`
	
5. Obtenga la señal de IAM para su ID de usuario.

    Para obtener más información, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli).

    Exporte la señal de IAM a una variable de shell como, por ejemplo, `$iam_token`:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Otorgue los permisos de usuario para trabajar con el servicio {{site.data.keyword.monitoringshort}}. 

   Ejecute el siguiente mandato cURL para otorgar permisos en la región EE.UU. sur:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Ejecute el siguiente mandato cURL para otorgar permisos en la región Reino Unido:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## Otorgar un rol de CF a un usuario mediante la IU de IBM Cloud 
{: #grant_permissions_ui_space}


Para trabajar con métricas en el dominio de espacio o en el dominio de organización, un usuario debe tener un rol de Cloud Foundry (CF) asignado a {{site.data.keyword.Bluemix_notm}}. Un rol de CF describe las acciones que el usuario puede realizar con el servicio {{site.data.keyword.monitoringshort}} en un espacio o en una organización. 

Complete los pasos siguientes para otorgar permisos a un usuario para trabajar con el servicio {{site.data.keyword.monitoringshort}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

    Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

4. Pulse **Asignar organización**.

5. Especifique la información sobre la política. La tabla siguiente lista los campos necesarios u opcionales para definir una política: 

    <table>
	  <caption>Lista de campos para configurar una política de CF.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valor</th>
	  </tr>
	  <tr>
	    <td>Organización</td>
		<td>Seleccione una organización de la lista.</td>
	  </tr>
	  <tr>
	    <td>Roles de la organización</td>
		<td>Seleccione **Sin rol de organización**. Sin embargo, si el usuario tiene un rol organizativo, elija un rol de organización de la lista. <br>Los valores válidos son: **Gestor de facturación**, **Auditor**, **Gestor**</td>
	  </tr>
	  <tr>
	    <td>Región</td>
		<td>Seleccione una región de la lista. <br>Los valores válidos son: **Todas las regiones actuales**, **EE.UU. sur**, **Reino Unido**</td>
	  </tr>
	  <tr>
	    <td>Espacio</td>
		<td>De forma predeterminada, **Todos los espacios actuales** está predefinido cuando el campo *Región* se establece en **Todas las regiones actuales**. Para otorgar permiso a un espacio individual, seleccione una región específica y, a continuación, elija un espacio de la lista.</td>
	  </tr>
	  <tr>
	    <td>Roles de espacio</td>
		<td>Seleccione un rol de espacio de la lista. <br>Los valores válidos son: **Gestor**, **Auditor**, **Desarrollador** y **Sin rol de espacio**. Para obtener más información, consulte [Roles de Cloud Foundry](/docs/services/cloud-monitoring/security_ov.html#bmx_roles).</td>
	  </tr>
	</table>
	
6. Pulse **Asignar política**.
	
La política que configure es aplicable a las regiones seleccionadas. 


