---
title: Présentation du connecteur Source Salesforce
description: Découvrez comment connecter Salesforce à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 20%

---

# [!DNL Salesforce]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers de gestion de la relation client (CRM). La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL Salesforce].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Mappage de champs de [!DNL Salesforce] à XDM

Pour établir une connexion source entre [!DNL Salesforce] et Platform, les champs de données source [!DNL Salesforce] doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Platform.

Pour plus d’informations sur les règles de mappage de champs entre les jeux de données [!DNL Salesforce] et Platform, reportez-vous à la section suivante :

- [Contacts](../adobe-applications/mapping/salesforce.md#contact)
- [Prospects](../adobe-applications/mapping/salesforce.md#lead)
- [Comptes](../adobe-applications/mapping/salesforce.md#account)
- [Opportunités](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rôles de contact d’opportunité](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagnes](../adobe-applications/mapping/salesforce.md#campaign)
- [Personnes membres de campagne](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relation de contact de compte](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configuration de l’espace de noms [!DNL Salesforce] et de l’utilitaire de génération automatique de schéma

Pour utiliser la source [!DNL Salesforce] dans le cadre de [!DNL B2B-CDP], vous devez d’abord configurer un utilitaire [!DNL Postman] afin de générer automatiquement vos espaces de noms et schémas [!DNL Salesforce]. La documentation suivante fournit des informations supplémentaires sur la configuration de l’utilitaire [!DNL Postman] :

- Vous pouvez télécharger l’espace de noms et l’environnement de génération automatique de schémas à partir de ce [référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Pour plus d’informations sur l’utilisation des API Platform, y compris sur la manière de rassembler des valeurs pour les en-têtes requis et de lire des exemples d’appels API, consultez le guide de [prise en main des API Platform](../../../landing/api-guide.md).
- Pour plus d’informations sur la génération de vos informations d’identification pour les API Platform, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md).
- Pour plus d’informations sur la configuration de [!DNL Postman] pour les API Platform, consultez le tutoriel sur la [configuration de la console de développement et [!DNL Postman]](../../../landing/postman.md).

Avec une console de développement Platform et [!DNL Postman] configurée, vous pouvez maintenant commencer à appliquer les valeurs d’environnement appropriées à votre environnement [!DNL Postman].

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur le remplissage de votre environnement [!DNL Postman] :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identifiant unique utilisé pour générer votre `{ACCESS_TOKEN}`. Pour plus d’informations sur la récupération de votre `{CLIENT_SECRET}`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) . | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Le jeton Web JSON (JWT) est un identifiant d’authentification utilisé pour générer votre {ACCESS_TOKEN}. Pour plus d’informations sur la génération de votre `{JWT_TOKEN}`, consultez le tutoriel sur l’ [authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md) . | `{JWT_TOKEN}` |
| `API_KEY` | Identifiant unique utilisé pour authentifier les appels vers les API Experience Platform. Pour plus d’informations sur la récupération de votre `{API_KEY}`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour terminer les appels vers les API Experience Platform. Pour plus d’informations sur la récupération de votre `{ACCESS_TOKEN}`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) . | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Concernant [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le conteneur `global` contient toutes les classes d’Adobe standard et de partenaire Experience Platform fournies, les groupes de champs de schéma, les types de données et les schémas. Concernant [!DNL Marketo], cette valeur est fixe et est toujours définie sur `global`. | `global` |
| `PRIVATE_KEY` | Informations d’identification utilisées pour authentifier votre instance [!DNL Postman] auprès des API Experience Platform. Consultez le tutoriel sur la configuration de Developer Console et la [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la récupération de votre {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour l’intégration à Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit la structure d’authentification des services Adobe. Concernant [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Personne morale pouvant posséder ou accorder une licence pour des produits et des services et permettre l’accès à ses membres. Consultez le tutoriel sur la [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la récupération de vos informations `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition d’environnement de test virtuel que vous utilisez. | `prod` |
| `TENANT_ID` | Identifiant utilisé pour vous assurer que les ressources que vous créez sont des espaces de noms corrects et qu’ils sont contenus dans votre organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Le point de terminaison d’URL vers lequel vous effectuez des appels d’API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | L’identifiant unique de votre compte [!DNL Marketo]. Consultez le tutoriel sur [l’authentification de votre  [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) pour plus d’informations sur la manière de récupérer votre `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | ID d’organisation de votre compte [!DNL Salesforce]. Pour plus d’informations sur l’acquisition de votre ID d’organisation [!DNL Salesforce], consultez le [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) suivant. | `00D4W000000FgYJUA0` |
| `has_abm` | Une valeur boolean qui indique si vous êtes abonné à [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Une valeur boolean qui indique si vous êtes abonné à [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Exécution des scripts

Avec votre collection [!DNL Postman] et votre environnement configuré, vous pouvez désormais exécuter le script via l’interface [!DNL Postman].

Dans l’interface [!DNL Postman], sélectionnez le dossier racine de l’utilitaire de génération automatique, puis sélectionnez **[!DNL Run]** dans l’en-tête supérieur.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

L’interface [!DNL Runner] s’affiche. À partir de là, assurez-vous que toutes les cases à cocher sont sélectionnées, puis sélectionnez **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Une requête réussie crée les espaces de noms et les schémas B2B conformément aux spécifications bêta.

## Connecter [!DNL Salesforce] à Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Salesforce] à Platform à l’aide d’API ou de l’interface utilisateur :

- [Création d’une connexion de base Salesforce à l’aide de l’API Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

## Connecter [!DNL Salesforce] à Platform à l’aide de l’interface utilisateur

- [Créer une connexion source Salesforce dans l’interface utilisateur](../../tutorials/ui/create/crm/salesforce.md)
- [Créer un flux de données pour une connexion CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
