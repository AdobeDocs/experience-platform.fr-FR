---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Import et utilisation d'audiences externes
description: Suivez ce tutoriel pour découvrir comment utiliser des audiences externes avec Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 82aa38c7bce05faeea5a9f42d0d86776737e04be
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 9%

---

# Import et utilisation d&#39;audiences externes

Adobe Experience Platform prend en charge la possibilité d’importer une audience externe, qui peut ensuite être utilisée comme composants pour une nouvelle définition de segment. Ce document fournit un tutoriel sur la configuration de l’Experience Platform pour importer et utiliser des audiences externes.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des différents services [!DNL Adobe Experience Platform] impliqués dans la création de segments d’audience. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Segmentation Service](../home.md) : vous permet de créer des segments ciblés depuis des données de Real-time Customer Profile.
- [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
- [Jeu de données](../../catalog/datasets/overview.md) : la structure de stockage et de gestion pour la persistance des données dans Experience Platform.
- [Ingestion par flux](../../ingestion/streaming-ingestion/overview.md) : Comment Experience Platform ingère et stocke des données à partir de périphériques côté client et côté serveur en temps réel.

### Données de segment par rapport aux métadonnées de segment

Avant de commencer à importer et utiliser des audiences externes, il est important de comprendre la différence entre les données de segment et les métadonnées de segment.

Les données de segment font référence aux profils qui répondent aux critères de qualification du segment et qui font donc partie de l’audience.

Les métadonnées de segment sont des informations sur le segment lui-même, qui incluent le nom, la description, l’expression (le cas échéant), la date de création, la date de dernière modification et un identifiant. L’ID lie les métadonnées du segment aux profils individuels qui répondent à la qualification du segment et qui font partie de l’audience résultante.

| Données de segment | Métadonnées de segment |
| ------------ | ---------------- |
| Profils qui répondent à la qualification des segments | Informations sur le segment lui-même |

## Création d’un espace de noms d’identité pour l’audience externe

La première étape de l’utilisation d’audiences externes consiste à créer un espace de noms d’identité. Les espaces de noms d’identité permettent à Platform d’associer l’origine d’un segment.

Pour créer un espace de noms d’identité, suivez les instructions du [guide sur l’espace de noms d’identité](../../identity-service/namespaces.md#manage-namespaces). Lors de la création de votre espace de noms d’identité, ajoutez les détails sources à l’espace de noms d’identité et marquez son [!UICONTROL Type] comme **[!UICONTROL Identifiant de non-personne]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Création d’un schéma pour les métadonnées de segment

Après avoir créé un espace de noms d’identité, vous devez créer un nouveau schéma pour le segment que vous allez créer.

Pour commencer à composer un schéma, sélectionnez d’abord **[!UICONTROL Schémas]** dans la barre de navigation de gauche, puis cliquez sur **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l’espace de travail des schémas. À partir de là, sélectionnez **[!UICONTROL Parcourir]** pour afficher une sélection complète des types de schémas disponibles.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Puisque vous créez une définition de segment, qui est une classe prédéfinie, sélectionnez **[!UICONTROL Utiliser la classe existante]**. Sélectionnez maintenant la classe **[!UICONTROL Définition de segment]**, suivie de **[!UICONTROL Attribuer la classe]**.

![](../images/tutorials/external-audiences/assign-class.png)

Maintenant que votre schéma a été créé, vous devez spécifier le champ qui contiendra l’identifiant du segment. Ce champ doit être marqué comme identité Principale et affecté aux espaces de noms que vous avez précédemment créés.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Après avoir marqué le champ `_id` comme identité Principale, sélectionnez le titre du schéma, suivi du bouton d’activation/désactivation **[!UICONTROL Profil]**. Sélectionnez **[!UICONTROL Activer]** pour activer le schéma pour [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Désormais, ce schéma est activé pour Profile, avec la Principale identification affectée à l’espace de noms d’identité non-personne que vous avez créé. Par conséquent, cela signifie que les métadonnées de segment importées dans Platform à l’aide de ce schéma seront ingérées dans Profile sans être fusionnées avec d’autres données de profil liées aux personnes.

## Création d’un jeu de données pour le schéma

Après avoir configuré le schéma, vous devez créer un jeu de données pour les métadonnées de segment.

Pour créer un jeu de données, suivez les instructions du [guide d’utilisation du jeu de données](../../catalog/datasets/user-guide.md#create). Vous souhaiterez suivre l’option **[!UICONTROL Créer un jeu de données à partir du schéma]**, à l’aide du schéma que vous avez créé précédemment.

![](../images/tutorials/external-audiences/select-schema.png)

Après avoir créé le jeu de données, continuez à suivre les instructions du [guide d’utilisation du jeu de données](../../catalog/datasets/user-guide.md#enable-profile) pour activer ce jeu de données pour Real-time Customer Profile.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configuration et importation des données d’audience

Une fois le jeu de données activé, les données peuvent désormais être envoyées vers Platform soit par le biais de l’interface utilisateur, soit à l’aide des API Experience Platform. Pour ingérer ces données dans Platform, vous devez créer une connexion en continu.

Pour créer une connexion en continu, vous pouvez suivre les instructions du [tutoriel sur l’API](../../sources/tutorials/api/create/streaming/http.md) ou du [tutoriel sur l’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md).

Une fois que vous avez créé votre connexion en continu, vous avez accès à votre point de terminaison de diffusion en continu unique auquel vous pouvez envoyer vos données. Pour savoir comment envoyer des données à ces points de terminaison, consultez le [tutoriel sur la diffusion en continu des données d’enregistrement](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Création de segments à l’aide d’audiences importées

Une fois les audiences importées configurées, elles peuvent être utilisées dans le cadre du processus de segmentation. Pour rechercher des audiences externes, accédez au créateur de segments, puis sélectionnez l’onglet **[!UICONTROL Audiences]** dans la section **[!UICONTROL Champs]** .

![](../images/tutorials/external-audiences/external-audiences.png)

## Étapes suivantes

Maintenant que vous pouvez utiliser des audiences externes dans vos segments, vous pouvez utiliser le créateur de segments pour créer des segments. Pour savoir comment créer des segments, consultez le [tutoriel sur la création de segments](./create-a-segment.md).
