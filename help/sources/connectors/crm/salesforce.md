---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma crm;crm;CRM;Salesforce;Salesforce
solution: Experience Platform
title: Présentation du connecteur source Salesforce
description: Découvrez comment connecter Salesforce à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 21%

---

# Connecteur [!DNL Salesforce]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers de gestion de la relation client (CRM). La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL Salesforce].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Mappage des champs à partir de [!DNL Salesforce] vers XDM

Pour établir une connexion source entre [!DNL Salesforce] et Platform, [!DNL Salesforce] les champs de données source doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Platform.

Pour plus d’informations sur les règles de mappage de champs entre les [!DNL Salesforce] jeux de données et plateforme :

- [Contacts](../adobe-applications/mapping/salesforce.md#contact)
- [Prospects](../adobe-applications/mapping/salesforce.md#lead)
- [Comptes](../adobe-applications/mapping/salesforce.md#account)
- [Opportunités](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rôles de contact d’opportunité](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagnes](../adobe-applications/mapping/salesforce.md#campaign)
- [Membres de la campagne](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relation de contact de compte](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configurez les [!DNL Salesforce] Utilitaire de génération automatique d’espace de noms et de schémas

Pour utiliser la variable [!DNL Salesforce] source dans le cadre de [!DNL B2B-CDP], vous devez d’abord configurer une [!DNL Postman] pour générer automatiquement votre [!DNL Salesforce] espaces de noms et schémas. La documentation suivante fournit des informations supplémentaires sur la configuration de la variable [!DNL Postman] utility :

- Vous pouvez télécharger la collection et l’environnement de génération automatique de l’espace de noms et du schéma à partir de ce [Référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Pour plus d’informations sur l’utilisation des API Platform, y compris sur la manière de rassembler des valeurs pour les en-têtes requis et de lire des exemples d’appels API, consultez le guide sur [Prise en main des API Platform](../../../landing/api-guide.md).
- Pour plus d’informations sur la génération de vos informations d’identification pour les API Platform, consultez le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md).
- Pour plus d’informations sur la configuration [!DNL Postman] pour les API Platform, consultez le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md).

Avec une console de développement Platform et [!DNL Postman] configuré. vous pouvez maintenant commencer à appliquer les valeurs d’environnement appropriées à votre [!DNL Postman] environnement.

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur le remplissage de vos [!DNL Postman] environnement :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identifiant unique utilisé pour générer votre `{ACCESS_TOKEN}`. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Le jeton Web JSON (JWT) est un identifiant d’authentification utilisé pour générer votre {ACCESS_TOKEN}. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour plus d’informations sur la manière de générer votre `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identifiant unique utilisé pour authentifier les appels vers les API Experience Platform. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour terminer les appels vers les API Experience Platform. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le `global` conteneur contient toutes les classes fournies par les Adobes standard et les partenaires Experience Platform, les groupes de champs de schéma, les types de données et les schémas. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur `global`. | `global` |
| `PRIVATE_KEY` | Informations d’identification utilisées pour authentifier vos [!DNL Postman] aux API Experience Platform. Consultez le tutoriel sur la configuration de Developer Console et [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la manière de récupérer votre {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour l’intégration à Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit la structure d’authentification des services Adobe. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Personne morale pouvant posséder ou accorder une licence pour des produits et des services et permettre l’accès à ses membres. Voir le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la manière de récupérer votre `{ORG_ID}` informations. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition d’environnement de test virtuel que vous utilisez. | `prod` |
| `TENANT_ID` | Identifiant utilisé pour vous assurer que les ressources que vous créez sont correctement placées dans l’espace de noms et qu’elles sont contenues dans votre organisation IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Le point de terminaison d’URL vers lequel vous effectuez des appels d’API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | L’identifiant unique de votre [!DNL Marketo] compte . Voir le tutoriel sur [vous authentifier [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) pour plus d’informations sur la manière de récupérer votre `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | L’ID d’organisation de votre [!DNL Salesforce] compte . Voir ce qui suit : [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) pour plus d’informations sur l’acquisition de [!DNL Salesforce] ID d’organisation. | `00D4W000000FgYJUA0` |
| `has_abm` | Une valeur boolean qui indique si vous êtes abonné à [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Une valeur boolean qui indique si vous êtes abonné à [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Exécution des scripts

Avec votre [!DNL Postman] configuration de la collection et de l’environnement, vous pouvez désormais exécuter le script via la [!DNL Postman] .

Dans le [!DNL Postman] , sélectionnez le dossier racine de l’utilitaire de génération automatique, puis sélectionnez **[!DNL Run]** dans l’en-tête supérieur.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Le [!DNL Runner] s’affiche. À partir de là, assurez-vous que toutes les cases à cocher sont sélectionnées, puis sélectionnez **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Une requête réussie crée les espaces de noms et les schémas B2B conformément aux spécifications bêta.

## Connecter [!DNL Salesforce] à Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Salesforce] à Platform à l’aide d’API ou de l’interface utilisateur :

- [Création d’une connexion de base Salesforce à l’aide de l’API Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

## Connecter [!DNL Salesforce] à Platform à l’aide de l’interface utilisateur

- [Création d’une connexion source Salesforce dans l’interface utilisateur](../../tutorials/ui/create/crm/salesforce.md)
- [Créer un flux de données pour une connexion CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
