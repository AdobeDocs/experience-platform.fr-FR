---
keywords: Experience Platform ; accueil ; rubriques populaires ; connecteur source Marketo ; espaces de nommage ; schémas
solution: Experience Platform
title: 'Espaces de nommage Marketo '
topic: aperçu
description: Ce document présente un aperçu des espaces de nommage personnalisés requis lors de la création d'un connecteur source Marketo Engage.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 16%

---


# (bêta) [!DNL Marketo Engage] espaces de nommage et schémas

>[!IMPORTANT]
>
>La source [!DNL Marketo Engage] est actuellement en version bêta. La fonction et la documentation sont des sujets de modification.

Le présent document fournit des informations sur la configuration sous-jacente des espaces de nommage et schémas B2B utilisés avec [!DNL Marketo Engage] (ci-après dénommés &quot;[!DNL Marketo]&quot;). Ce document fournit également des détails sur la configuration de votre utilitaire d&#39;automatisation Postman nécessaire à la génération d&#39;[!DNL Marketo] espaces de nommage et schémas B2B.

## Conditions préalables

Avant de pouvoir générer vos espaces de nommage et schémas B2B, vous devez d&#39;abord configurer votre console de développement de plate-forme et votre environnement [!DNL Postman]. Pour plus d&#39;informations, consultez le didacticiel sur la configuration de [la console de développement et  [!DNL Postman]](../../../../landing/postman.md).

Avec une console de développement de plate-forme et une configuration [!DNL Postman], appliquez les variables suivantes à votre environnement [!DNL Marketo] :

| Variable Environnement | Exemple de valeur | Notes |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Pour plus d’informations, consultez le didacticiel sur l’[authentification de votre  [!DNL Marketo] instance](./marketo-auth.md). |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Consultez le [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) suivant pour plus d&#39;informations sur l&#39;acquisition de l&#39;ID d&#39;organisation. |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Consultez le [[!DNL Microsoft Dynamics] guide](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) suivant pour plus d&#39;informations sur l&#39;acquisition de l&#39;ID d&#39;organisation. |
| `has_abm` | `false` | Cette valeur est définie sur `true` si vous êtes abonné à Marketing basé sur le compte. |
| `has_msi` | `false` | Cette valeur est définie sur `true` si vous êtes abonné à [!DNL Marketo Sales Insight]. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] espaces de nommage

Les espaces de noms d’identité sont des composants d’[[!DNL Identity Service]](../../../../identity-service/home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte.

Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Un nouvel espace de nommage personnalisé est requis pour chaque nouvelle combinaison d&#39;instance et de jeu de données [!DNL Marketo]. Par exemple, un connecteur source [!DNL Marketo] ingérant le jeu de données `programs` nécessite son propre espace de nommage personnalisé et un autre connecteur source Marketo ingérant le même jeu de données nécessite également son propre nouvel espace de nommage personnalisé. Pour plus d&#39;informations, consultez la [présentation des espaces de nommage](../../../../identity-service/namespaces.md).

L&#39;espace de nommage [!DNL Marketo] est utilisé dans l&#39;identité Principale de l&#39;entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de nommage [!DNL Marketo].

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

| Nom d’affichage | Symbole d’identité | Type d’identité | Type d’émetteur | Type d&#39;entité émetteur | [!DNL Salesforce] Exemple d’identifiant d’organisation d’abonnement |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | généré automatiquement | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] espaces de nommage

Si vous êtes abonné à l&#39;intégration [!DNL Dynamics], l&#39;espace de nommage [!DNL Dynamics] est utilisé comme identité secondaire de l&#39;entité.

Le tableau suivant contient des informations sur la configuration sous-jacente des espaces de nommage [!DNL Dynamics].

| Nom d’affichage | Symbole d’identité | Type d’identité | Type d’émetteur | Type d&#39;entité émetteur | [!DNL Salesforce] Exemple d’identifiant d’organisation d’abonnement |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | généré automatiquement | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | généré automatiquement | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | généré automatiquement | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | généré automatiquement | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | généré automatiquement | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | généré automatiquement | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] schémas

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs mixins.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](../../../../xdm/schema/composition.md).

Le tableau suivant contient des informations sur la configuration sous-jacente des schémas [!DNL Marketo].

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Nom du schéma | Classe de base | Mixins | Identité Principal | Espace de nommage d&#39;identité Principal | Identité Secondaire | Espace de nommage d&#39;identité Secondaire | Relation | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Société {MUNCHKIN_ID} | Compte professionnel XDM | Détails du compte d&#39;entreprise XDM | `accountID` dans la classe de base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` dans le mixage des détails du compte professionnel XDM</li><li>Type : un à un</li><li>Schéma de référence : Société Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Personne {MUNCHKIN_ID} | XDM Individual Profile | <ul><li>Détails sur les personnes d&#39;affaires XDM</li><li>Composants professionnels XDM</li></ul> | `personID` dans la classe de base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` mixage des détails concernant les personnes d&#39;affaires XDM</li><li>`workEmail.address` mixage des détails concernant les personnes d&#39;affaires XDM</li><li>`identityMap` du mixin Carte d’identité</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-mail</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` mixage des composants professionnels de XDM</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Société Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriété de destination : `accountID`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| [!DNL Marketo] Opportunité {MUNCHKIN_ID} | Opportunité commerciale XDM | Détails des opportunités commerciales XDM | `opportunityID` dans la classe de base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Société Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriété de destination : `accountID`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation à partir du schéma de référence : Opportunités</li></ul> |
| [!DNL Marketo] Rôle de contact d&#39;opportunité {MUNCHKIN_ID} | Relation de personne avec une opportunité commerciale XDM | Aucun | `opportunityPersonID` dans la classe de base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Première relation<ul><li>`personID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Personne Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriété de destination : `personID`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Opportunités</li></ul>Deuxième relation<ul><li>`opportunityID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Opportunité Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Propriété de destination : `opportunityID`</li><li>Nom de la relation à partir du schéma actuel : Opportunité</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| [!DNL Marketo] Programme {MUNCHKIN_ID} | XDM Business Campaign | Détails de XDM Business Campaign | `campaignID` dans la classe de base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Membre du programme {MUNCHKIN_ID} | Membre XDM Business Campaign | Détails des membres XDM Business Campaign | `campaignMemberID` dans la classe de base | `marketo_program_member_{MUNCHKIN_ID}` | Aucun | Aucun | Première relation<ul><li>`personID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Personne Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriété de destination : `personID`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Programmes</li></ul>Deuxième relation<ul><li>`campaignID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Programme Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_program_{MUNCHKIN_ID}`</li><li>Propriété de destination : campaignID</li><li>Nom de la relation à partir du schéma actuel : Programme</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| [!DNL Marketo] Liste statique {MUNCHKIN_ID} | XDM Business Marketing Liste | Aucun | `marketingListID` dans la classe de base | `marketo_static_list_{MUNCHKIN_ID}` | Aucun | Aucun | Aucun | La Liste statique n&#39;est pas synchronisée à partir de [!DNL Salesforce] et ne possède donc pas d&#39;identité secondaire |
| [!DNL Marketo] Membre de Liste statique {MUNCHKIN_ID} | Membres de XDM Business Marketing Liste | Aucun | `marketingListMemberID` dans la classe de base | `marketo_static_list_member_{MUNCHKIN_ID}` | Aucun | Aucun | Première relation<ul><li>`personID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Personne Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriété de destination : `personID`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Listes</li></ul>Deuxième relation<ul><li>`marketingListID` dans la classe de base</li><li>Type : Plusieurs à un</li><li>Schéma de référence : Liste statique Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Propriété de destination : `marketingListID`</li><li>Nom de la relation à partir du schéma actuel : Liste</li><li>Nom de la relation à partir du schéma de référence : Personnes</li></ul> |
| [!DNL Marketo] Compte nommé {MUNCHKIN_ID} | Compte professionnel XDM | Détails du compte d&#39;entreprise XDM | `accountID` dans la classe de base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` dans la classe de base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` dans le mixage des détails du compte professionnel XDM</li><li>Type : un à un</li><li>Schéma de référence : Compte Marketo nommé {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Activité {MUNCHKIN ID} | Événement d’expérience XDM | <ul><li>Visiter la page Web</li><li>Nouvelle piste</li><li>Convertir la piste</li><li>Ajouter à la Liste</li><li>Supprimer de la Liste</li><li>Ajouter à l&#39;opportunité</li><li>Supprimer de l&#39;opportunité</li><li>Formulaire rempli</li><li>Clics sur les liens</li><li>Courrier électronique livré</li><li>Courrier électronique ouvert</li><li>Courrier électronique cliqué</li><li>Courrier indésirable</li><li>Courrier indésirable renvoyé par courriel</li><li>Courrier électronique sans abonnement</li><li>Score modifié</li><li>Opportunité mise à jour</li><li>Etat de la progression Campaign modifié</li><li>Identifiant de personne</li><li>URL Web Marketo | `personID` du mixin d&#39;identification de personne | marketo_person_{MUNCHKIN_ID} | Aucun | Aucun | Première relation<ul><li>`listOperations.listID` field</li><li>Type : un à un</li><li>Schéma de référence : Liste statique Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Deuxième relation<ul><li>`opportunityEvent.opportunityID` field</li><li>Type : un à un</li><li>Schéma de référence : Opportunité Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Troisième relation<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Type : un à un</li><li>Schéma de référence : Programme Marketo {MUNCHKIN_ID}</li><li>Espace de noms: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Tous les schémas sont activés pour [!DNL Real-time Customer Profile]

## Étapes suivantes

Pour savoir comment connecter vos données [!DNL Marketo] à la plate-forme, consultez le didacticiel sur la [création d&#39;un connecteur source Marketo dans l&#39;interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).