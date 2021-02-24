---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Application de la conformité de l’utilisation des données aux segments ciblés
topic: didacticiel
translation-type: tm+mt
source-git-commit: 2ca0768c951cf67a775fdfc2c1f9440596d118bf
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 12%

---


# Importation et utilisation d’audiences externes

Adobe Experience Platform prend en charge la possibilité d’importer de l’audience externe, qui peut ensuite être utilisée comme composants pour une nouvelle définition de segment. Ce document fournit un didacticiel pour configurer l&#39;Experience Platform pour importer et utiliser des audiences externes.

## Prise en main

- [Segmentation Service](../home.md) : vous permet de créer des segments ciblés depuis des données de Real-time Customer Profile.
- [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
- [Jeu de données](../../catalog/datasets/overview.md) : la structure de stockage et de gestion pour la persistance des données dans Experience Platform.
- [Ingestion par flux](../../ingestion/streaming-ingestion/overview.md) : méthode d’ingestion et de stockage de données en temps réel dans Experience Platform à partir de périphériques côté client et côté serveur.

## Créer un espace de nommage d&#39;identité pour l&#39;audience externe

La première étape de l&#39;utilisation des audiences externes consiste à créer un espace de nommage d&#39;identité. Les espaces de nommage d’identité permettent à la plate-forme d’associer l’emplacement d’où provient un segment.

Pour créer un espace de nommage d&#39;identité, suivez les instructions du [guide de l&#39;espace de nommage d&#39;identité](../../identity-service/namespaces.md#manage-namespaces). Lors de la création de votre espace de nommage d&#39;identité, ajoutez les détails de la source à l&#39;espace de nommage d&#39;identité et marquez son [!UICONTROL Type] comme **[!UICONTROL identifiant de non-personne]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Création d’un schéma pour les métadonnées de segment

Après avoir créé un espace de nommage d’identité, vous devez créer un nouveau schéma pour le segment que vous allez créer.

Pour commencer à composer un schéma, sélectionnez d’abord **[!UICONTROL Schémas]** dans la barre de navigation de gauche, puis **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l’espace de travail Schémas. À partir de là, sélectionnez **[!UICONTROL Parcourir]** pour afficher une sélection complète des types de Schéma disponibles.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Puisque vous créez une définition de segment, qui est une classe prédéfinie, sélectionnez **[!UICONTROL Utiliser la classe existante]**. Sélectionnez maintenant la classe **[!UICONTROL Définition de segment]**, suivie de la classe **[!UICONTROL Attribuer]**.

![](../images/tutorials/external-audiences/assign-class.png)

Maintenant que votre schéma a été créé, vous devez spécifier le champ qui contiendra l’identifiant du segment. Ce champ doit être marqué comme identité Principale et affecté aux espaces de nommage que vous avez créés précédemment.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Après avoir marqué le champ `_id` en tant qu&#39;identité Principale, sélectionnez le titre du schéma, suivi de la bascule **[!UICONTROL Profil]**. Sélectionnez **[!UICONTROL Activer]** pour activer le schéma pour [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Maintenant, ce schéma est activé pour le Profil, avec l&#39;identification Principale affectée à l&#39;espace de nommage d&#39;identité non-personne que vous avez créé. En conséquence, cela signifie que les métadonnées de segment importées dans la plateforme à l’aide de ce schéma seront ingérées dans le Profil sans être fusionnées avec d’autres données de Profil liées aux personnes.

## Création d’un jeu de données pour le schéma

Après avoir configuré le schéma, vous devez créer un jeu de données pour les métadonnées du segment.

Pour créer un jeu de données, suivez les instructions du [guide de l&#39;utilisateur du jeu de données](../../catalog/datasets/user-guide.md#create). Suivez l&#39;option **[!UICONTROL Créer un jeu de données à partir du schéma]**, en utilisant le schéma que vous avez créé précédemment.

![](../images/tutorials/external-audiences/select-schema.png)

Après avoir créé le jeu de données, continuez à suivre les instructions du [guide de l&#39;utilisateur du jeu de données](../../catalog/datasets/user-guide.md#enable-profile) pour activer ce jeu de données pour le Profil client en temps réel.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configuration et importation des données d’audience

Lorsque le jeu de données est activé, les données peuvent désormais être envoyées dans la plate-forme, soit par l’intermédiaire de l’interface utilisateur, soit à l’aide des API Experience Platform. Pour importer ces données dans Platform, vous devez créer une connexion de flux continu.

Pour créer une connexion en flux continu, vous pouvez suivre les instructions du [didacticiel d’API](../../sources/tutorials/api/create/streaming/http.md) ou du [didacticiel d’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md).

Une fois votre connexion de flux continu créée, vous aurez accès à votre point de terminaison de flux continu unique auquel vous pourrez envoyer vos données. Pour savoir comment envoyer des données à ces points de terminaison, consultez le [didacticiel sur la diffusion en continu des données d&#39;enregistrement](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Création de segments à l’aide d’audiences importées

Une fois les audiences importées configurées, elles peuvent être utilisées dans le cadre du processus de segmentation. Pour rechercher des audiences externes, accédez au Créateur de segments et sélectionnez **[!UICONTROL Audiences]** dans l&#39;onglet **[!UICONTROL Champs]**.

![](../images/tutorials/external-audiences/external-audiences.png)

## Étapes suivantes

Maintenant que vous pouvez utiliser des audiences externes dans vos segments, vous pouvez utiliser le créateur de segments pour créer des segments. Pour savoir comment créer des segments, consultez le [didacticiel sur la création de segments](./create-a-segment.md).