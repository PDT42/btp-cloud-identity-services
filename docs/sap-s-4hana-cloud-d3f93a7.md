<!-- loiod3f93a7870c341c0993cd733ed9e9b3a -->

# SAP S/4HANA Cloud

Follow this procedure to set up SAP S/4HANA Cloud as a source system.



<a name="loiod3f93a7870c341c0993cd733ed9e9b3a__prereq_tcl_444_kfb"/>

## Prerequisites

To establish the connection between Identity Provisioning and SAP S/4HANA Cloud, you need to set up the communication \(user, system and arrangement\) on SAP S/4HANA Cloud. You have the option to do it either now, as a prerequisite, or while configuring SAP S/4HANA Cloud as a source system, as described in step 3.



## Context

SAP S/4HANA Cloud is a complete enterprise resource planning \(ERP\) system with built-in intelligent technologies and advanced analytics.

You can use Identity Provisioning to configure SAP S/4HANA Cloud as a source system where you can read entities from and provision them to target systems of your choice. This scenario supports reading **business users** \(Employee, Contingent Worker\), **user assignments**, and **business roles** \(which are considered as *groups*\).



## Procedure

1.  Access the Identity Provisioning UI.

    -   [Access Identity Provisioning UI of Bundle Tenants](https://help.sap.com/viewer/f48e822d6d484fa5ade7dda78b64d9f5/Cloud/en-US/7ab5884ffbc44461a57622d2f633e57c.html "Access the Identity Provisioning UI when the service is bundled as part of an SAP cloud solution's license.") :arrow_upper_right:
    -   [Access Identity Provisioning UI of Standalone Tenants](https://help.sap.com/viewer/f48e822d6d484fa5ade7dda78b64d9f5/Cloud/en-US/61fd82ed48ab42b2bc74626926c1722c.html "Access the Identity Provisioning user interface as a standalone product.") :arrow_upper_right:

2.  Sign in to the administration console of SAP Cloud Identity Services and navigate to *Identity Provisioning* \> *Source Systems*.

3.  Add *SAP S/4HANA Cloud* as a source system. For more information, see [Add New Systems](Operation-Guide/add-new-systems-bd214dc.md).

4.  Set up the communication between Identity Provisioning and SAP S/4HANA Cloud and configure your authentication method \(basic or certificate-based\).

    > ### Note:  
    > We recommend that you use certificate-based authentication.

    1.  In your newly added SAP S/4HANA source system, select the *Certificate* tab and choose *Generate* \> *Download*, as described in [Generate and Manage Certificates for Outbound Connection](https://help.sap.com/docs/IDENTITY_PROVISIONING/f48e822d6d484fa5ade7dda78b64d9f5/76867db8ce534becbfc08b050695df8e.html?version=Cloud).

        Skip step **a.** if you want to use basic authentication.

        The next steps are performed in SAP S/4HANA backend system and are relevant for both basic and certificate-based authentication.

    2.  [Create a communication user](https://help.sap.com/viewer/0f69f8fb28ac4bf48d2b57b9637e81fa/Latest/en-US/0377adea0401467f939827242c1f4014.html) and provide the respective credentials.

        For basic authentication, provide *User Name* and *Password*.

        For certificate-based authentication, upload the certificate you have generated in the Identity Provisioning UI on the previous step.

    3.  [Create a communication system](https://help.sap.com/viewer/0f69f8fb28ac4bf48d2b57b9637e81fa/Latest/en-US/1bfe32ae08074b7186e375ab425fb114.html) and assign the created user to the communication system.

        For your Identity Provisioning scenario, provide *System ID*, *System Name* and *Host Name*.

    4.  [Create a communication arrangement](https://help.sap.com/viewer/0f69f8fb28ac4bf48d2b57b9637e81fa/Latest/en-US/a0771f6765f54e1c8193ad8582a32edb.html) with the created system.

        For your Identity Provisioning scenario, choose *Scenario ID* SAP\_COM\_0193 \(SAP Cloud Identity Provisioning Integration\).

        > ### Note:  
        > The communication scenario *SAP\_COM\_0193* is enhanced to support the User UUID attribute which is generated by Identity Authentication at user creation.
        > 
        > The User UUID is universally unique identifier. This attribute is immutable and unique across technology layers, such as user interface, APIs, and security tokens, as well as across products and lines of business contributing to a business process in the Intelligent Enterprise.


5.  Choose the *Properties* tab to configure the connection settings for your system.

    > ### Note:  
    > If your tenant is running on SAP BTP, Neo environment, you can create a [connectivity destination](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/72696d6d06c0490394ac3069da600278.html) in your subaccount in the SAP BTP cockpit, and then select it from the *Destination Name* combo box in your Identity Provisioning User Interface.
    > 
    > If one and the same property exists both in the cockpit and in the *Properties* tab, the value set in the *Properties* tab is considered with higher priority.
    > 
    > We recommend that you use the *Properties* tab. Use a connectivity destination only if you need to reuse one and the same configuration for multiple provisioning systems.

    **Mandatory Properties**


    <table>
    <tr>
    <th valign="top">

    Property Name
    
    </th>
    <th valign="top">

    Description & Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    `Type`
    
    </td>
    <td valign="top">
    
    Enter: *HTTP*
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `URL`
    
    </td>
    <td valign="top">
    
    Enter the SAP S/4HANA Cloud API URL.

    You can find the correct URL in the *API-URL* field of the communication arrangement set up for communication scenario SAP\_COM\_0193.

    For example: `https://my123456-api.s4hana.ondemand.com`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `ProxyType`
    
    </td>
    <td valign="top">
    
    Enter: *Internet*
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `Authentication`
    
    </td>
    <td valign="top">
    
    Enter your authentication method:

    -   *BasicAuthentication*

    -   *ClientCertificateAuthentication*



    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `User`
    
    </td>
    <td valign="top">
    
    Valid if *BasicAuthentication* is configured as authentication method.

    Enter the *User Name* from the communication arrangement.

    > ### Restriction:  
    > Do not use special symbol '**,**' \(comma\) as it is not supported.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `Password`
    
    </td>
    <td valign="top">
    
    \(Credential\) Valid if *BasicAuthentication* is configured as authentication method.

    Enter the *Password* for the user name from the communication arrangement.

    > ### Restriction:  
    > Do not use special symbol '**,**' \(comma\) as it is not supported.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `s4hana.cloud.skip.read.archived`
    
    </td>
    <td valign="top">
    
    In the event of archived \(disabled\) entities in a source SAP S/4HANA Cloud system, choose whether the provisioning jobs to continue reading such entities or to skip them.

    This property is enabled by default. If you want to always read disabled entities, set the property to **false**, or delete it.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `ips.date.variable.format`
    
    </td>
    <td valign="top">
    
    *yyyy-MM-dd*
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `s4hana.cloud.api.version`
    
    </td>
    <td valign="top">
    
    The version of the system API you use.

    Version *1* means your SAP S/4HANA Cloud system uses *SAP\_COM\_0193* communication arrangement.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    \(Optional\) `s4hana.cloud.roles.filter`
    
    </td>
    <td valign="top">
    
    Enter OData filtering for reading roles in the S/4HANA system.

    To learn what criteria you can use, see: [OData URI Conventions](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/) → **4.5 Filter System Query Option**
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    \(Optional\) `s4hana.cloud.roles.page.size`
    
    </td>
    <td valign="top">
    
    Indicate how many business roles \(considered as *groups*\) per page to be read from your SAP S/4HANA Cloud system.

    The value must be an integer number.
    
    </td>
    </tr>
    </table>
    
    To learn what additional properties are relevant to this system, see [List of Properties](list-of-properties-d6f3577.md). You can use the main search, or filter properties by the *Name* or *System Type* columns.

    Exemplary destination:


    <table>
    <tr>
    <td valign="top">
    
    `Type`=*HTTP*

    `Authentication`=*BasicAuthentication*

    `ProxyType`=*Internet*

    `URL`=*https://my1234567-api.s4hana.ondemand.com*

    `User`=*MyS4HANAuser*

    `Password`=\*\*\*\*\*\*\*\*\*\*\*\*

    `s4hana.cloud.api.version`=*1*

    `ips.date.variable.format`=*yyyy-MM-dd*

    `s4hana.cloud.skip.read.archived`=*true*

    `s4hana.cloud.roles.filter`=*startswith\(ID, 'EMPLOYEE\_LEVEL\_3'\) eq true*

    `s4hana.cloud.roles.page.size`=*30*
    
    </td>
    </tr>
    </table>
    
6.  \(Optional\) Configure the transformations.

    Transformations are used to map the user attributes from the data model of the source system to the data model of the target system, and the other way around. The Identity Provisioning offers a default transformation for the *SAP S/4HANA Cloud* source system, whose settings are displayed under the *Transformations* tab after saving its initial configuration.

    You can change the default transformation mapping rules depending on your setup of entities in your SAP S/4HANA Cloud. For more information, see:

    [Manage Transformations](Operation-Guide/manage-transformations-2d0fbe5.md)

    [SAP S/4HANA Cloud API: Business User](https://help.sap.com/viewer/f1531d40f450474dbf95f0404cb62007/latest/en-US/640fb5fa26664a7486de073b1882405c.html)

    **Default transformation:**

    > ### Code Syntax:  
    > ```
    > {
    >   "user": {
    >     "condition": "($.user.validityPeriod.startDate <= '${currentDate}') && ($.user.validityPeriod.endDate > '${currentDate}')",
    >     "mappings": [
    >       {
    >         "sourcePath": "$.personID",
    >         "targetVariable": "entityIdSourceSystem"
    >       },
    >       {
    >         "sourcePath": "$.personalInformation.firstName",
    >         "targetPath": "$.name.givenName",
    >         "optional": true
    >       },
    >       {
    >         "sourcePath": "$.personalInformation.lastName",
    >         "targetPath": "$.name.familyName",
    >         "optional": true
    >       },
    >       {
    >         "sourcePath": "$.personalInformation.middleName",
    >         "targetPath": "$.name.middleName",
    >         "optional": true
    >       },
    >       {
    >         "sourcePath": "$.personalInformation.personFullName",
    >         "targetPath": "$.name.formatted",
    >         "optional": true
    >       },
    >       {
    >         "sourcePath": "$.user.userName",
    >         "targetPath": "$.userName",
    >         "optional": true,
    >         "correlationAttribute": true
    >       },
    >       {
    >         "constant": true,
    >         "targetPath": "$.active"
    >       },
    >       {
    >         "condition": "$.user.lockedIndicator == 'true'",
    >         "constant": false,
    >         "targetPath": "$.active",
    >         "optional": true
    >       },
    >       {
    >         "sourcePath": "$.workplaceInformation.emailAddress",
    >         "targetPath": "$.emails[0].value",
    >         "optional": true,
    >         "correlationAttribute": true
    >       },
    >       {
    >         "sourcePath": "$.user.logonLanguageCode",
    >         "optional": true,
    >         "targetPath": "$.locale"
    >       },
    >       {
    >         "sourcePath": "$.PersonExternalID",
    >         "optional": true,
    >         "correlationAttribute": true
    >       },
    >       {
    >         "sourcePath": "$.user.globalUserID",
    >         "optional": true,
    >         "targetPath": "$['urn:ietf:params:scim:schemas:extension:sap:2.0:User']['userUuid']"
    >       },
    >       {
    >         "sourcePath": "$.user.role",
    >         "targetPath": "$.groups",
    >         "preserveArrayWithSingleElement": true,
    >         "functions": [
    >           {
    >             "condition": "'%s4hana.cloud.roles.prefix%' !== 'null'",
    >             "function": "concatString",
    >             "applyOnElements": true,
    >             "prefix": "%s4hana.cloud.roles.prefix%",
    >             "applyOnAttribute": "roleName",
    >             "assignToAttribute": "display"
    >           },
    >           {
    >             "condition": "'%s4hana.cloud.roles.prefix%' === 'null'",
    >             "function": "concatString",
    >             "applyOnElements": true,
    >             "prefix": "",
    >             "applyOnAttribute": "roleName",
    >             "assignToAttribute": "display"
    >           },
    >           {
    >             "function": "concatString",
    >             "applyOnElements": true,
    >             "prefix": "",
    >             "applyOnAttribute": "roleName",
    >             "assignToAttribute": "value"
    >           }
    >         ]
    >       },
    >       {
    >         "type": "remove",
    >         "targetPath": "$.groups[*].roleName"
    >       },
    >       {
    >         "type": "valueMapping",
    >         "sourcePaths": [
    >           "$.user.timeZoneCode"
    >         ],
    >         "targetPath": "$.timezone",
    >         "defaultValue": "Europe/Berlin",
    >         "valueMappings": [
    >           {
    >             "key": [
    >               "WDFT"
    >             ],
    >             "mappedValue": "Europe/Berlin"
    >           },
    >           {
    >             "key": [
    >               "ISRAEL"
    >             ],
    >             "mappedValue": "Asia/Jerusalem"
    >           },
    >           {
    >             "key": [
    >               "RUS03"
    >             ],
    >             "mappedValue": "Europe/Moscow"
    >           },
    >           {
    >             "key": [
    >               "AUSNSW"
    >             ],
    >             "mappedValue": "Australia/Sydney"
    >           },
    >           {
    >             "key": [
    >               "UTC+4"
    >             ],
    >             "mappedValue": "Asia/Dubai"
    >           },
    >           {
    >             "key": [
    >               "BRAZIL"
    >             ],
    >             "mappedValue": "America/Sao_Paulo"
    >           },
    >           {
    >             "key": [
    >               "BRZLEA"
    >             ],
    >             "mappedValue": "America/Sao_Paulo"
    >           },
    >           {
    >             "key": [
    >               "MSTNO"
    >             ],
    >             "mappedValue": "America/Phoenix"
    >           },
    >           {
    >             "key": [
    >               "EST"
    >             ],
    >             "mappedValue": "America/New_York"
    >           },
    >           {
    >             "key": [
    >               "UTC"
    >             ],
    >             "mappedValue": "Etc/UTC"
    >           },
    >           {
    >             "key": [
    >               "UTC+3"
    >             ],
    >             "mappedValue": "Asia/Riyadh"
    >           },
    >           {
    >             "key": [
    >               "EST_"
    >             ],
    >             "mappedValue": "America/Toronto"
    >           },
    >           {
    >             "key": [
    >               "UTC+8"
    >             ],
    >             "mappedValue": "Asia/Shanghai"
    >           },
    >           {
    >             "key": [
    >               "JAPAN"
    >             ],
    >             "mappedValue": "Asia/Tokyo"
    >           }
    >         ]
    >       },
    >       {
    >         "type": "valueMapping",
    >         "sourcePaths": [
    >           "$.businessPartnerRoleCode"
    >         ],
    >         "targetPath": "$.userType",
    >         "defaultValue": "Employee",
    >         "valueMappings": [
    >           {
    >             "key": [
    >               "BUP003"
    >             ],
    >             "mappedValue": "Employee"
    >           },
    >           {
    >             "key": [
    >               "BBP005"
    >             ],
    >             "mappedValue": "Contingent Worker"
    >           }
    >         ]
    >       }
    >     ]
    >   },
    >   "group": {
    >     "mappings": [
    >       {
    >         "sourcePath": "$.ID",
    >         "targetPath": "$.displayName",
    >         "targetVariable": "entityIdSourceSystem",
    >         "functions": [
    >           {
    >             "condition": "'%s4hana.cloud.roles.prefix%' !== 'null'",
    >             "function": "concatString",
    >             "prefix": "%s4hana.cloud.roles.prefix%"
    >           }
    >         ]
    >       },
    >       {
    >         "constant": "urn:ietf:params:scim:schemas:core:2.0:Group",
    >         "targetPath": "$.schemas[0]"
    >       },
    >       {
    >         "sourcePath": "$.to_BusinessUserAssignment.results",
    >         "optional": true,
    >         "preserveArrayWithSingleElement": true,
    >         "targetPath": "$.members"
    >       },
    >       {
    >         "type": "remove",
    >         "targetPath": "$.members[*].__metadata"
    >       },
    >       {
    >         "type": "remove",
    >         "targetPath": "$.members[*].UserName"
    >       },
    >       {
    >         "type": "rename",
    >         "constant": "value",
    >         "targetPath": "$.members[*].PersonID"
    >       },
    >       {
    >         "constant": "User",
    >         "targetPath": "$.members[*].type"
    >       }
    >     ]
    >   }
    > }
    > ```

    By default, Identity Provisioning reads group IDs and members. If you want the service to also read group descriptions, you can add an extra mapping to the *"group"* resource. To learn how, see [Guided Answers: Business Role Description](https://ga.support.sap.com/dtp/viewer/#/tree/2065/actions/26547:29111:29114:27412:39660:40191).

7.  Now, add a target system to provision users and groups into it. Choose from: [Target Systems](target-systems-ab3f641.md)




<a name="loiod3f93a7870c341c0993cd733ed9e9b3a__postreq_vgg_5qj_p1b"/>

## Next Steps

-   Before starting a provisioning job, you can first subscribe for e-mail notifications from the source system you use in your scenario. This way, you will be notified by e-mail about eventual failed entities during the jobs. For more information, see [Manage Job Notifications](Monitoring-and-Reporting/manage-job-notifications-d055bc2.md).
-   Now, start an identity provisioning job. For more information, see [Monitor Provisioning Job Logs](Monitoring-and-Reporting/monitor-provisioning-job-logs-e5b5176.md).

**Related Information**  


[SAP S/4HANA Cloud Documentation](https://help.sap.com/viewer/9d794cbd48c648bc8a176e422772de7e/latest/en-US/7af7b8541486ed05e10000000a4450e5.html)
