---
title: Notes de mise à jour d’octobre 2021 d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2021 pour Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 79%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 octobre 2021**

## Mises à jour vers Experience Platform

Mises à jour vers Experience Platform.

### Interface utilisateur {#ui}

L’interface utilisateur a été mise à jour avec les modifications suivantes :

| Fonctionnalité | Description |
| --- | --- |
| Thème sombre | Utilisez le sélecteur de thème sombre pour basculer entre les thèmes clairs et sombres dans l’interface d’Experience Platform. Le commutateur se trouve dans le profil utilisateur sous le nom d’utilisateur et l’e-mail.  |
| Activer/désactiver le volet de navigation de gauche | Utilisez le bouton de navigation amélioré situé en haut de l’en-tête de l’application pour afficher ou masquer le menu affichant les fonctionnalités de votre Experience Platform. Le système mémorise votre dernière sélection et ne vous montre que les fonctionnalités auxquelles vous avez accès.  |
| Accès à la visibilité | La barre de navigation de gauche affiche uniquement les fonctionnalités auxquelles vous avez accès. Dans les versions précédentes d’Adobe Experience Platform, les éléments indisponibles étaient visibles, même si vous ne pouviez pas y accéder.  |

Consultez le [Guide de l’interface utilisateur d’Experience Platform](../../landing/ui-guide.md) pour en savoir plus.

## Mises à jour des fonctionnalités existantes

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [Sources](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| fonction `contains_key` | La fonction `contains_key` a été introduite. Vous pouvez ainsi vérifier si l’objet existe dans la source. Cette fonction remplace la fonction `is_set`, désormais obsolète.  |
| Messages d’erreur | Les messages d’erreur renvoyés par le point de d’entrée `/mappingSets/preview` de l’API Data Prep sont désormais cohérents avec les messages d’erreur générés lors de l’exécution.  |

Voir la [[!DNL Data Prep] présentation](../../data-prep/home.md) pour en savoir plus sur ce service.

### Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de la source [!DNL Amazon S3] | Vous pouvez désormais utiliser le paramètre `s3SessionToken` pour connecter votre compte [!DNL Amazon S3] à Experience Platform à l’aide d’informations d’identification de sécurité temporaires. Ce jeton vous permet de fournir un accès temporaire à court terme à vos ressources [!DNL Amazon S3] à des utilisateurs dans des environnements non approuvés. Pour plus d’informations, consultez la [[!DNL Amazon S3] documentation](../../sources/connectors/cloud-storage/s3.md#prerequisites). |
| [!DNL Generic REST API] (version bêta) | Vous pouvez désormais créer une connexion source [!DNL Generic REST API] à l’aide de l’API [[!DNL Flow Service]  ](../../sources/tutorials/api/create/protocols/generic-rest.md) pour importer des données d’une application REST générique vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Generic REST API] présentation](../../sources/connectors/protocols/generic-rest.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
