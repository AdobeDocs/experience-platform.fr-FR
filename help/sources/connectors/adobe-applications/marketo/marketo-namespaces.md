---
keywords: Experience Platform ; accueil ; rubriques populaires ; connecteur source Marketo ; espaces de nommage ; schémas
solution: Experience Platform
title: Espaces de nommage Marketo
topic-legacy: overview
description: Ce document présente un aperçu des espaces de nommage personnalisés requis lors de la création d'un connecteur source Marketo Engage.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
translation-type: tm+mt
source-git-commit: 8dd7b1724f3de12bf6a3a1b77ee8050fd1a9eaf3
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 14%

---

# (bêta) [!DNL Marketo Engage] espaces de nommage et schémas

>[!IMPORTANT]
>
>La source [!DNL Marketo Engage] est actuellement en version bêta. La fonction et la documentation sont des sujets de modification.

Le présent document fournit des informations sur la configuration sous-jacente des espaces de nommage et schémas B2B utilisés avec [!DNL Marketo Engage] (ci-après dénommés &quot;[!DNL Marketo]&quot;). Ce document fournit également des détails sur la configuration de votre utilitaire d&#39;automatisation Postman nécessaire à la génération d&#39;[!DNL Marketo] espaces de nommage et schémas B2B.

## Configuration de l’utilitaire de génération automatique d’espace de nommage et de schéma [!DNL Marketo]

La première étape de l&#39;utilisation de l&#39;utilitaire de génération automatique d&#39;espace de nommage et de schéma [!DNL Marketo] consiste à configurer votre console de développement de plate-forme et votre environnement [!DNL Postman].

- Vous pouvez télécharger la collecte et l&#39;environnement des utilitaires de génération automatique d&#39;espace de nommage et de schéma à partir de ce [référentiel GitHub](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility).
- Pour plus d&#39;informations sur l&#39;utilisation des API de plateforme, y compris sur la manière de collecter des valeurs pour les en-têtes requis et de lire des exemples d&#39;appels d&#39;API, consultez le guide [Prise en main des API de plateforme](../../../../landing/api-guide.md).
- Pour plus d&#39;informations sur la génération de vos informations d&#39;identification pour les API de plateformes, consultez le didacticiel [authentification et accès aux API d&#39;Experience Platform](../../../../landing/api-authentication.md).
- Pour plus d&#39;informations sur la configuration de [!DNL Postman] pour les API de plateformes, consultez le didacticiel sur [la configuration de la console de développement et  [!DNL Postman]](../../../../landing/postman.md).

Avec une console de développement de plate-forme et [!DNL Postman] configurée, vous pouvez maintenant début d&#39;appliquer les valeurs d&#39;environnement appropriées à votre environnement [!DNL Postman].

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur le remplissage de votre environnement [!DNL Postman] :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificateur unique utilisé pour générer votre `{ACCESS_TOKEN}`. Consultez le didacticiel sur [l&#39;authentification et l&#39;accès aux API Experience Platform](../../../../landing/api-authentication.md) pour savoir comment récupérer votre `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Le JSON Web Token (JWT) est un jeu d’informations d’identification d’authentification utilisé pour générer votre {ACCESS_TOKEN}. Consultez le didacticiel sur [l&#39;authentification et l&#39;accès aux API Experience Platform](../../../../landing/api-authentication.md) pour savoir comment générer votre `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificateur unique utilisé pour authentifier les appels aux API Experience Platform. Consultez le didacticiel sur [l&#39;authentification et l&#39;accès aux API Experience Platform](../../../../landing/api-authentication.md) pour savoir comment récupérer votre `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour terminer les appels aux API Experience Platform. Consultez le didacticiel sur [l&#39;authentification et l&#39;accès aux API Experience Platform](../../../../landing/api-authentication.md) pour savoir comment récupérer votre `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | En ce qui concerne [!DNL Marketo], cette valeur est fixe et toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le conteneur `global` contient tous les Adobes standard et les partenaires Experience Platform fournis par des classes, des groupes de champs de schéma, des types de données et des schémas. En ce qui concerne [!DNL Marketo], cette valeur est fixe et toujours définie sur `global`. | `global` |
| `PRIVATE_KEY` | Informations d’identification utilisées pour authentifier votre instance [!DNL Postman] auprès des API Experience Platform. Consultez le didacticiel sur la configuration de la console de développement et [la configuration de la console de développement et  [!DNL Postman]](../../../../landing/postman.md) pour savoir comment récupérer votre {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour l’intégration à l’Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit le cadre d&#39;authentification aux services d&#39;Adobe. En ce qui concerne [!DNL Marketo], cette valeur est fixe et toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entité corporative qui peut posséder ou mettre sous licence des produits et services et autoriser l&#39;accès à ses membres. Consultez le didacticiel sur [la configuration de la console de développement et  [!DNL Postman]](../../../../landing/postman.md) pour savoir comment récupérer vos `{IMS_ORG}` informations. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition sandbox virtuelle que vous utilisez. | `prod` |
| `TENANT_ID` | ID utilisé pour vous assurer que les ressources que vous créez sont correctement espacées dans l’espace de noms et qu’elles sont contenues dans votre organisation IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Point de terminaison d’URL auquel vous appelez l’API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | ID unique de votre compte [!DNL Marketo]. Consultez le didacticiel sur l&#39;[authentification de votre  [!DNL Marketo] instance](./marketo-auth.md) pour savoir comment récupérer votre `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | ID d&#39;organisation de votre compte [!DNL Salesforce]. Consultez le [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) suivant pour plus d&#39;informations sur l&#39;acquisition de votre [!DNL Salesforce] ID d&#39;organisation. | `00D4W000000FgYJUA0` |
| `msd_org_id` | ID d&#39;organisation de votre compte [!DNL Dynamics]. Consultez le [[!DNL Microsoft Dynamics] guide](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) suivant pour plus d&#39;informations sur l&#39;acquisition de votre [!DNL Dynamics] ID d&#39;organisation. | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Valeur booléenne qui indique si vous êtes abonné à [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Valeur booléenne qui indique si vous êtes abonné à [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] espaces de nommage

Les espaces de noms d’identité sont des composants d’[[!DNL Identity Service]](../../../../identity-service/home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte.

Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Un nouvel espace de nommage personnalisé est requis pour chaque nouvelle combinaison d&#39;instance et de jeu de données [!DNL Marketo]. Par exemple, un connecteur source [!DNL Marketo] ingérant le jeu de données `programs` nécessite son propre espace de nommage personnalisé et un autre connecteur source Marketo ingérant le même jeu de données nécessite également son propre nouvel espace de nommage personnalisé. Pour plus d&#39;informations, consultez la [présentation des espaces de nommage](../../../../identity-service/namespaces.md).

L&#39;espace de nommage [!DNL Marketo] est utilisé dans l&#39;identité Principale de l&#39;entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de nommage [!DNL Marketo].

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom d’affichage | Symbole d’identité | Type d’identité | Type d’émetteur | Type d&#39;entité émetteur | Exemple d&#39;identifiant Munchkin |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | généré automatiquement | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | généré automatiquement | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | généré automatiquement | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | généré automatiquement | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | généré automatiquement | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | généré automatiquement | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | généré automatiquement | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | généré automatiquement | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | généré automatiquement | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] espaces de nommage

Si vous êtes abonné à l&#39;intégration [!DNL Salesforce], l&#39;espace de nommage [!DNL Salesforce] est utilisé dans l&#39;identité secondaire de l&#39;entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de nommage [!DNL Salesforce].

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom d’affichage | Symbole d’identité | Type d’identité | Type d’émetteur | Type d&#39;entité émetteur | [!DNL Salesforce] Exemple d’identifiant d’organisation d’abonnement |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] espaces de nommage

Si vous êtes abonné à l&#39;intégration [!DNL Dynamics], l&#39;espace de nommage [!DNL Dynamics] est utilisé comme identité secondaire de l&#39;entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de nommage [!DNL Dynamics].

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom d’affichage | Symbole d’identité | Type d’identité | Type d’émetteur | Type d&#39;entité émetteur | [!DNL Dynamics] Exemple d’identifiant d’organisation d’abonnement |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | généré automatiquement | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | généré automatiquement | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | généré automatiquement | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | généré automatiquement | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | généré automatiquement | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | généré automatiquement | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] schémas

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d&#39;une classe de base et de groupes de champs de schéma nuls ou plus.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](../../../../xdm/schema/composition.md).

Le tableau suivant contient des informations sur la configuration sous-jacente des schémas [!DNL Marketo].

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom du schéma | Classe de base | Groupes de champs | [!DNL Profile] dans le Schéma | Identité Principal | Espace de nommage d&#39;identité Principal | Identité Secondaire | Espace de nommage d&#39;identité Secondaire | Relation | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | Compte professionnel XDM | Détails du compte d&#39;entreprise XDM | Activé | `accountID` dans la classe de base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` dans le groupe de champs Détails du compte professionnel XDM</li><li>Type : un à un</li><li>Schéma de référence : `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | XDM Individual Profile | <ul><li>Détails sur les personnes d&#39;affaires XDM</li><li>Composants professionnels XDM</li><li>IdentityMap</li></ul> | Activé | `personID` dans la classe de base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` du groupe de champs Détails sur la personne active XDM</li><li>`workEmail.address` du groupe de champs Détails sur la personne active XDM</li><li>`identityMap` du groupe de champs Carte d’identité</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-mail</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` du groupe de champs Composants professionnels de XDM</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriété de destination : `accountID`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | Opportunité commerciale XDM | Détails des opportunités commerciales XDM | Activé | `opportunityID` dans la classe de base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriété de destination : `accountID`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Opportunités</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | Relation de personne avec une opportunité commerciale XDM | Aucun | Activé | `opportunityPersonID` dans la classe de base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Première relation<ul><li>`personID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriété de destination : `personID`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Opportunités</li></ul>Deuxième relation<ul><li>`opportunityID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Propriété de destination : `opportunityID`</li><li>Nom de la relation à partir du schéma actuel : Opportunité</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM Business Campaign | Détails de XDM Business Campaign | Activé | `campaignID` dans la classe de base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | Membre XDM Business Campaign | Détails des membres XDM Business Campaign | Activé | `campaignMemberID` dans la classe de base | `marketo_program_member_{MUNCHKIN_ID}` | Aucun | Aucun | Première relation<ul><li>`personID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Personne Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriété de destination : `personID`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Programmes</li></ul>Deuxième relation<ul><li>`campaignID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_program_{MUNCHKIN_ID}`</li><li>Propriété de destination : `campaignID`</li><li>Nom de la relation à partir du schéma actuel : Programme</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM Business Marketing Liste | Aucun | Activé | `marketingListID` dans la classe de base | `marketo_static_list_{MUNCHKIN_ID}` | Aucun | Aucun | Aucun | La Liste statique n&#39;est pas synchronisée à partir de [!DNL Salesforce] et n&#39;a donc pas d&#39;identité secondaire. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | Membres de XDM Business Marketing Liste | Aucun | Activé | `marketingListMemberID` dans la classe de base | `marketo_static_list_member_{MUNCHKIN_ID}` | Aucun | Aucun | Première relation<ul><li>`personID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriété de destination : `personID`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Listes</li></ul>Deuxième relation<ul><li>`marketingListID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Propriété de destination : `marketingListID`</li><li>Nom de la relation à partir du schéma actuel : Liste</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> | Le membre de liste statique n&#39;est pas synchronisé à partir de [!DNL Salesforce] et ne possède donc pas d&#39;identité secondaire. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | Compte professionnel XDM | Détails du compte d&#39;entreprise XDM | Activé | `accountID` dans la classe de base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` dans le groupe de champs Détails du compte professionnel XDM</li><li>Type : un à un</li><li>Schéma de référence : `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Activité `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>Visiter la page Web</li><li>Nouvelle piste</li><li>Convertir la piste</li><li>Ajouter à la Liste</li><li>Supprimer de la Liste</li><li>Ajouter à l&#39;opportunité</li><li>Supprimer de l&#39;opportunité</li><li>Formulaire rempli</li><li>Clics sur les liens</li><li>Courrier électronique livré</li><li>Courrier électronique ouvert</li><li>Courrier électronique cliqué</li><li>Courrier indésirable</li><li>Courrier indésirable renvoyé par courriel</li><li>Courrier électronique sans abonnement</li><li>Score modifié</li><li>Opportunité mise à jour</li><li>Etat de la progression Campaign modifié</li><li>Identifiant de personne</li><li>URL Web Marketo | Activé | `personID` du groupe de champs Identifiant de personne | `marketo_person_{MUNCHKIN_ID}` | Aucun | Aucun | Première relation<ul><li>`listOperations.listID` field</li><li>Type : un à un</li><li>Schéma de référence : `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Deuxième relation<ul><li>`opportunityEvent.opportunityID` field</li><li>Type : un à un</li><li>Schéma de référence : `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Troisième relation<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Type : un à un</li><li>Schéma de référence : `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Espace de noms: `marketo_program_{MUNCHKIN_ID}`</li></ul> | L&#39;identité Principale du schéma `[!DNL Marketo] Activity {MUNCHKIN_ID}` est `personID`, ce qui est identique à l&#39;identité Principale du schéma `[!DNL Marketo] Person {MUNCHKIN_ID}`. |

{style=&quot;table-layout:auto&quot;}

## Étapes suivantes

Pour savoir comment connecter vos données [!DNL Marketo] à la plate-forme, consultez le didacticiel sur la [création d&#39;un connecteur source Marketo dans l&#39;interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
