---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
source-git-commit: b6f4c79df79ae20b8051b69ef34dd255df193454
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 39%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 octobre 2021**

## Mises à jour de l’Experience Platform

Mises à jour de l’Experience Platform.

### Interface utilisateur {#ui}

L’interface utilisateur a été mise à jour avec les modifications suivantes :

| Fonctionnalité | Description |
| --- | --- |
| Thème sombre | Utilisez le sélecteur de thème sombre pour passer d’un thème clair à un thème sombre dans l’interface de Platform. Le commutateur se trouve dans le profil utilisateur sous le nom d’utilisateur et l’adresse électronique. |
| Activer/désactiver la navigation à gauche | Utilisez le bouton de navigation amélioré situé en haut de l’en-tête de l’application pour afficher ou masquer le menu affichant les fonctionnalités de votre Experience Platform. Le système mémorise votre dernière sélection et ne vous montre que les fonctionnalités auxquelles vous avez accès. |
| Accès à la visibilité | La barre de navigation de gauche affiche uniquement les fonctionnalités auxquelles vous avez accès. Dans les versions précédentes de Adobe Experience Platform, les éléments indisponibles étaient visibles, même si vous ne pouviez pas y accéder. |

Voir [Guide de l’interface utilisateur de Platform](../../landing/ui-guide.md) pour en savoir plus.

## Mises à jour des fonctionnalités existantes

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [Sources](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| fonction `contains_key` | Le `contains_key` a été introduite. Vous pouvez ainsi vérifier si l’objet existe dans la source. Cette fonction remplace la fonction `is_set` , désormais obsolète. |
| Messages d’erreur | Messages d’erreur renvoyés par la variable `/mappingSets/preview` Les points de terminaison dans l’API Data Prep sont désormais cohérents avec les messages d’erreur générés lors de l’exécution. |

Voir [[!DNL Data Prep] aperçu](../../data-prep/home.md) pour en savoir plus sur ce service.

### Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de la source [!DNL Amazon S3] | Vous pouvez désormais utiliser la variable `s3SessionToken` pour connecter votre [!DNL Amazon S3] compte vers Platform à l’aide d’informations d’identification de sécurité temporaires. Ce jeton vous permet de fournir un accès temporaire à court terme à votre [!DNL Amazon S3] aux utilisateurs dans des environnements non approuvés. Pour plus d’informations, voir la [[!DNL Amazon S3] documentation ](../../sources/connectors/cloud-storage/s3.md#prerequisites). |
| [!DNL Generic REST API] (version bêta) | Vous pouvez désormais créer une [!DNL Generic REST API] connexion source à l’aide de la fonction [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) pour importer des données d’une application REST générique vers Platform. Pour plus d’informations, consultez la [[!DNL Generic REST API] présentation](../../sources/connectors/protocols/generic-rest.md). |
| [!DNL Zoho CRM] (version bêta) | Vous pouvez désormais créer une [!DNL Zoho CRM] connexion source à l’aide de la fonction [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) ou le [interface utilisateur](../../sources/tutorials/ui/create/crm/zoho.md) pour importer des données de [!DNL Zoho CRM] compte à Platform. Pour plus d’informations, consultez la [[!DNL Zoho CRM] présentation](../../sources/connectors/crm/zoho.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
