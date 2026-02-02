---
title: Présentation D’Oracle Eloqua (V2) Source
description: Découvrez comment connecter Oracle Eloqua à Adobe Experience Platform.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 2%

---

# Présentation de la source [!DNL Oracle Eloqua] (V2)

>[!IMPORTANT]
>
>La source [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md) d’origine a été abandonnée en janvier 2026. Aucune migration n’est disponible pour cette source obsolète et vous devez réimplémenter vos données à l’aide de la nouvelle source [!DNL Oracle Eloqua] (V2).

[!DNL Oracle Eloqua] est une puissante plateforme d’automatisation du marketing de niveau entreprise conçue pour aider les organisations, principalement dans l’espace B2B, à automatiser et à personnaliser le processus complexe de gestion des prospects et d’orchestration des parcours d’acheteurs. Il sert de hub central où les équipes marketing peuvent définir, déployer et mesurer des campagnes sophistiquées sur plusieurs canaux numériques, afin de s&#39;assurer que les prospects reçoivent le contenu approprié au moment précis où ils sont le plus engagés. Les objets pris en charge pour l’ingestion via [!DNL Eloqua] sont **Contacts**, **Comptes**, **Campagnes** et **Activités**. Une fois l’ingestion initiale terminée, toutes les données modifiées sont importées à l’aide d’un processus incrémentiel planifié.

Vous pouvez utiliser la source de [!DNL Eloqua] pour connecter votre compte [!DNL Eloqua] à Adobe Experience Platform. Lisez la documentation ci-dessous pour savoir comment commencer.

## Exemples de cas d’utilisation {#use-case-examples}

Vous trouverez ci-dessous un tableau décrivant les objets marketing pris en charge par l’intégration d’[!DNL Eloqua] (V2) à Adobe Experience Platform. Pour chaque objet, vous trouverez une description ainsi que des exemples de cas d’utilisation pour illustrer comment l’intégration des données [!DNL Eloqua] à Real-Time CDP peut améliorer l’efficacité marketing et les résultats des campagnes.

| Objet | Description | Exemples de cas d’utilisation |
| --- | --- | --- |
| Contacts | Ingérez des données de contact (telles que le nom, l’adresse e-mail, le numéro de téléphone et l’intitulé de la fonction) dans Real-Time CDP pour créer des profils client détaillés et unifiés qui consolident toutes les interactions et tous les engagements avec chaque contact individuel. | **Optimisation des campagnes :** en intégrant les données de contact de [!DNL Eloqua], votre équipe marketing peut identifier les prospects hautement prioritaires en fonction des activités récentes telles que les ouvertures d’e-mail, les envois de formulaire et les enregistrements d’événement. Real-Time CDP fournit une vue à 360° du comportement de chaque contact sur les e-mails, les sites web et d’autres points de contact marketing, ce qui permet aux équipes marketing d’adapter les campagnes et d’optimiser les messages pour un meilleur engagement et une meilleure conversion. |
| Comptes | Ingérez des données au niveau du compte (telles que le nom de la société, le secteur, la taille de la société, le chiffre d’affaires, l’emplacement) pour créer des stratégies de marketing basé sur les comptes (ABM) dans Real-Time CDP et permettez à votre équipe de cibler et d’impliquer les organisations appropriées avec les messages pertinents. | **Campagnes ABM :** l’intégration des données de compte d’[!DNL Eloqua] permet de créer des campagnes ABM ciblées. Par exemple, une société de logiciels pourrait utiliser les données des comptes pour segmenter et envoyer des campagnes par e-mail personnalisées aux décideurs des entreprises du secteur financier, afin de promouvoir de nouvelles solutions adaptées à leur secteur. |
| Campagnes | Ingérez des données de campagne (telles que les noms de campagne, les types, les objectifs, les mesures de performances telles que les taux d’ouverture et les taux de clics) dans le Real-Time CDP pour suivre et optimiser les performances de la campagne sur plusieurs canaux. Utilisez ces données pour mesurer le retour sur investissement et affiner vos stratégies. | **Attribution cross-canal :** si [!DNL Eloqua] envoie des données de campagne à Real-Time CDP, les équipes marketing peuvent afficher les performances des campagnes sur différents canaux (e-mail, médias sociaux, publicités, etc.), en attribuant les conversions aux points de contact appropriés et en affinant les stratégies futures en fonction de cette insight. |
| Activités | Ingérez des données d’activité (telles que les ouvertures d’e-mail, les clics, les visites de site web, les envois de formulaire, l’assiduité au webinaire) pour suivre le comportement en temps réel et les contacts sur différents canaux, créant ainsi des opportunités d’engagement personnalisé en temps réel. | **Formation en temps réel :** en intégrant les données d’activité de [!DNL Eloqua], Real-Time CDP peut envoyer des e-mails personnalisés ou des notifications aux équipes commerciales lorsqu’un contact consulte du contenu (par exemple en téléchargeant un livre blanc ou en cliquant sur un lien d’e-mail), ce qui permet un suivi en temps opportun et de meilleures opportunités de conversion. |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Lisez les sections ci-dessous pour connaître les conditions préalables à la configuration que vous devez remplir avant de pouvoir connecter votre source à Experience Platform.

### Configuration de l’application pour l’authentification

Suivez les étapes ci-dessous pour savoir comment configurer votre compte [!DNL Eloqua] et vous connecter à Experience Platform à l’aide de l’authentification de base.

Pour commencer, connectez-vous à votre instance [!DNL Eloqua] en tant qu’administrateur (ou en tant qu’utilisateur autorisé à créer des utilisateurs, des groupes de sécurité et des applications).

![Mon tableau de bord Eloqua.](../../images/tutorials/create/eloqua/admin.png)

Accédez à **Paramètres** > **Extensions de Platform** > **Développeur d’App Cloud** > **Créer une application**. Fournissez des détails sur votre application, notamment son nom, sa description, son icône et l’URL de rappel OAuth. Lorsque vous avez terminé, cliquez sur **Enregistrer**.

![Panneau App Developer et bouton Créer une application dans le tableau de bord Eloqua.](../../images/tutorials/create/eloqua/create-app.png)

| Propriété | Description |
| --- | --- |
| Nom | Nom de votre application. |
| Description | Brève description de votre application. |
| Icône | URL de l’icône. |
| URL de rappel OAuth | L’URL vers laquelle les utilisateurs doivent être redirigés après l’installation de l’application et l’authentification à l’aide de [!DNL Eloqua]. |

![Fenêtre Créer une application dans Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

Une fois votre application créée, accédez à [!DNL Authentication to Eloqua] et récupérez les **Identifiant client** et **Secret client** à partir de l’application nouvellement créée. Ces valeurs seront utilisées ultérieurement lors de la connexion à Experience Platform.

![Identifiant client et secret client dans Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

Les groupes de sécurité permettent aux administrateurs de contrôler les niveaux d’accès des utilisateurs aux ressources, fonctionnalités, interfaces, etc. Pour créer un groupe de sécurité, accédez à **Paramètres** > **Utilisateurs**. Sélectionnez ensuite l’onglet **Groupe** dans le panneau de gauche, puis sélectionnez **Créer un groupe de sécurité**.

![Le tableau de bord de gestion des utilisateurs dans Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Utilisez la fenêtre **[!DNL Security Group Overview]** pour attribuer un nom et un acronyme à votre groupe de sécurité. Une fois créée, accédez à [!DNL Action Permissions] , ajoutez l’autorisation API [!DNL Consume] dans la liste et sélectionnez **Enregistrer**.

![Fenêtre de présentation du groupe de sécurité dans Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![Fenêtre de sélection pour l’API de consommation](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>[!DNL Consume]’API est une autorisation requise, mais vous pouvez ajouter d’autres autorisations en fonction de votre utilisation de l’application.

Pour ingérer des données de campagne, accédez à l’interface **Modifier l’utilisateur** et ajoutez des [!DNL Guided Campaigns] au groupe de sécurité sélectionné.

![Ajout du groupe de sécurité avec les campagnes guidées.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

Vous pouvez éventuellement créer un utilisateur supplémentaire et l’ajouter à un groupe de sécurité. Pour obtenir des instructions détaillées, consultez la documentation [!DNL Eloqua] sur [création d’un utilisateur](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) et [affectation d’un utilisateur à un groupe de sécurité](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de [!DNL Eloqua] connecter à Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| Identifiant client | Identifiant exposé publiquement utilisé par [!DNL Eloqua] pour identifier votre compte lors de l’autorisation d’accès à Experience Platform. |
| Secret client | Clé confidentielle connue uniquement de l’application cliente et du serveur d’autorisation. Cette clé est requise avec l’identifiant client pour authentifier votre compte. |
| Nom d’utilisateur | Nom d’utilisateur associé à votre compte [!DNL Eloqua]. Il est utilisé pour vérifier et autoriser votre accès. Le nom d’utilisateur suit le format `CompanyName\Username`. |
| Mot de passe | Mot de passe associé à votre compte [!DNL Eloqua]. Avec votre nom d&#39;utilisateur, il permet d&#39;accéder à votre environnement Eloqua. |
| Point d’entrée de base | Préfixe de l’URI de base d’authentification pour [!DNL Eloqua]. Le point d’entrée de base ne doit pas inclure `http://` ni `https://` lors de l’authentification. |

## Guide de mappage des [!DNL Eloqua]

>[!NOTE]
>
>Voici les champs delta utilisés en interne pour le chargement incrémentiel des données :
>
>- **Contacts :** `C_DateModified`
>- **Comptes:** `M_DateModified`
>- **Activité:** `CreatedAt`
>- **Objets personnalisés :** `UpdatedAt`
>- **Campaign:** `updatedAt`

Les tableaux suivants fournissent des mappages détaillés entre les champs source [!DNL Eloqua] et leurs champs de destination Modèle de données d’expérience (XDM) correspondants dans Experience Platform. Chaque ligne décrit la logique de transformation, si le champ est immuable, et fournit des notes supplémentaires pour vous aider à comprendre comment vos données [!DNL Eloqua] seront ingérées et structurées dans Experience Platform.

### Comptes

| Colonne Eloqua Source | Chemin de destination XDM | Remarques |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Ce champ est toujours défini sur la valeur fixe « Eloqua ». |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Le connecteur ne peut pas détecter automatiquement votre identifiant d’instance CRM. Vous devez remplacer manuellement `${CRM_INSTANCE_ID}` par votre ID d’instance CRM réel, soit votre ID d’instance Salesforce, soit votre ID d’instance Dynamics. Lors de l’ingestion, si `M_SFDCAccountID` est présent, le connecteur génère la clé externe à l’aide de cette valeur et ajoute des `\@CRM_INSTANCE_ID.Salesforce`. Si ce champ est vide, le connecteur utilise `M_MSCRMAccountID` et ajoute `\@CRM_INSTANCE_ID.Dynamics` à la place. Si les deux champs sont vides, ce champ est défini sur null. |

{style="table-layout:auto"}

### Activités

| Colonne Eloqua Source | Chemin de destination XDM | Remarques |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Ce champ est toujours défini sur la valeur fixe « Eloqua ». |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | En fonction de l’ActivityType, la valeur de l’eventType Experience Platform correspondante est renseignée. Pour les activités externes, il n’existe aucun eventType dans Experience Platform. Vous pouvez modifier ce mappage pour gérer d’autres types. |
| `ActivityDate` | date et heure | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Campagnes

| Colonne Eloqua Source | Chemin de destination XDM | Remarques |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Ce champ est toujours défini sur la valeur fixe « Eloqua ». |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Contacts

| Colonne Eloqua Source | Chemin de destination XDM | Remarques |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Ce champ est toujours défini sur la valeur fixe « Eloqua ». |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | Le `SOURCE_INSTANCE_ID` sera automatiquement remplacé par le connecteur . |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Si l’instance [!DNL Eloqua] est synchronisée avec Salesforce, conservez ce mappage. Sinon, supprimez-le. Le connecteur ne permettant pas de déterminer CRM_INSTANCE_ID, vous devez remplacer ${CRM_INSTANCE_ID} par votre ID d’instance Salesforce synchronisé. Ce même mappage s’applique à personComponents et extSourceSystemAudit. Conservez donc les deux. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Si l’instance [!DNL Eloqua] est synchronisée avec Dynamics, conservez ce mappage. Sinon, supprimez-le. Le connecteur ne permettant pas de déterminer CRM_INSTANCE_ID, vous devez remplacer ${CRM_INSTANCE_ID} par votre ID d’instance Dynamics synchronisé. Ce même mappage s’applique à personComponents et extSourceSystemAudit. Conservez donc les deux. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Si l’instance [!DNL Eloqua] est synchronisée avec Salesforce, conservez ce mappage. Sinon, supprimez-le. Le connecteur ne permettant pas de déterminer CRM_INSTANCE_ID, vous devez remplacer ${CRM_INSTANCE_ID} par votre ID d’instance Salesforce synchronisé. Ce même mappage s’applique à personComponents et extSourceSystemAudit. Conservez donc les deux. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Si l’instance [!DNL Eloqua] est synchronisée avec Dynamics, conservez ce mappage. Sinon, supprimez-le. Le connecteur ne permettant pas de déterminer CRM_INSTANCE_ID, vous devez remplacer ${CRM_INSTANCE_ID} par votre ID d’instance Dynamics synchronisé. Ce même mappage s’applique à personComponents et extSourceSystemAudit. Conservez donc les deux. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | Le connecteur ne permettant pas de déterminer l’ID de l’instance CRM_INSTANCE_ID, vous devez remplacer ${CRM_INSTANCE_ID} par votre ID d’instance CRM synchronisé, soit l’ID d’instance Salesforce, soit l’ID d’instance Dynamics. Ce même mappage s’applique à la fois à b2b.accountKey et à personComponents.sourceAccountKey. Conservez donc les deux. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | Le connecteur ne permettant pas de déterminer l’ID de l’instance CRM_INSTANCE_ID, vous devez remplacer ${CRM_INSTANCE_ID} par votre ID d’instance CRM synchronisé, soit l’ID d’instance Salesforce, soit l’ID d’instance Dynamics. Ce même mappage s’applique à la fois à b2b.accountKey et à personComponents.sourceAccountKey. Conservez donc les deux. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Référence de mapping du type d’activité

| Eloqua ActivityType | EventType XDM |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | passer en l’état |

{style="table-layout:auto"}

### Espaces réservés de variable

Les modèles de mappage utilisent les espaces réservés de variable suivants, qui sont remplacés une fois un flux de données exécuté :

| Espace réservé | Description | Utilisation |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | ID unique de l’instance source Eloqua | Utilisé dans les clés sources |
| `${CRM_INSTANCE_ID}` | ID unique du système CRM (Salesforce/Dynamics) | Utilisé dans les clés externes |

## Connexion de [!DNL Eloqua] à Experience Platform

Continuez pour configurer votre connexion source [!DNL Eloqua] dans Experience Platform. Pour obtenir un guide détaillé sur la configuration de la connexion via l’interface utilisateur, reportez-vous au [tutoriel ici](../../tutorials/ui/create/marketing-automation/eloqua.md). Lisez ce tutoriel pour en savoir plus sur la connexion de votre compte [!DNL Eloqua], la sélection des données, le mappage des champs, la planification des ingestions et la surveillance des flux de données.

