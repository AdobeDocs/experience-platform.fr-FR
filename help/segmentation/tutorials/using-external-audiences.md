---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Importation et utilisation de publics externes
description: Suivez ce tutoriel pour apprendre à utiliser des publics externes avec Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 9%

---

# Importation et utilisation de publics externes

Adobe Experience Platform prend en charge la possibilité d’importer une audience externe, qui peut ensuite être utilisée comme composants pour une nouvelle définition de segment. Ce document fournit un didacticiel pour configurer un Experience Platform pour importer et utiliser des publics externes.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des différents [!DNL Adobe Experience Platform] services impliqués dans la création de segments d’audience. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Segmentation Service](../home.md) : vous permet de créer des segments ciblés depuis des données de Real-time Customer Profile.
- [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client. Pour tirer le meilleur parti de la segmentation, assurez-vous que vos données sont assimilées en tant que profils et événements en fonction de [meilleures pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).
- [Jeu de données](../../catalog/datasets/overview.md) : la structure de stockage et de gestion pour la persistance des données dans Experience Platform.
- [Exposition en continu](../../ingestion/streaming-ingestion/overview.md): Comment l’Experience Platform assimile et stocke les données des périphériques côté client et serveur en temps réel.

### Données de segment et métadonnées de segment

Avant de commencer à importer et à utiliser des publics externes, il est important de comprendre la différence entre les données de segment et les métadonnées de segment.

Les données de segment font référence aux profils qui répondent aux critères de qualification de segment et qui font donc partie du public.

Les métadonnées de segment sont des informations sur le segment lui-même, qui comprennent le nom, la description, l’expression (le cas échéant), la date de création, la date de dernière modification et un ID. L’ID lie les métadonnées de segment aux profils individuels qui répondent à la qualification de segment et font partie du public obtenu.

| Données de segment | Métadonnées de segment |
| ------------ | ---------------- |
| Profils répondant aux critères de qualification des segments | Informations sur le segment lui-même |

## Créer un espace de noms d’identité pour le public externe

La première étape pour utiliser des publics externes consiste à créer un espace de noms d’identité. Les espaces de noms d’identité permettent à la plate-forme d’associer l’origine d’un segment.

Pour créer un espace de noms d’identité, suivez les instructions de la section [guide de l&#39;espace de noms d&#39;identité](../../identity-service/namespaces.md#manage-namespaces). Lors de la création de votre espace de noms d’identité, ajoutez les détails source à l’espace de noms d’identité et marquez son [!UICONTROL Type] comme **[!UICONTROL Identificateur de non-personne]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Création d’un schéma pour les métadonnées de segment

Après avoir créé un espace de noms d’identité, vous devez créer un nouveau schéma pour le segment que vous allez créer.

Pour commencer à composer un schéma, commencez par sélectionner **[!UICONTROL Schémas]** sur la barre de navigation de gauche, suivie de la **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l’espace de travail Schémas. À partir de là, sélectionnez **[!UICONTROL Parcourir]** pour afficher une sélection complète des types de schéma disponibles.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Puisque vous créez une définition de segment, qui est une classe prédéfinie, sélectionnez **[!UICONTROL Utiliser une classe existante]**. Sélectionnez ensuite l’option **[!UICONTROL Définition de segment]** , suivi de **[!UICONTROL Affecter une classe]**.

![](../images/tutorials/external-audiences/assign-class.png)

Maintenant que votre schéma a été créé, vous devez spécifier quel champ doit contenir l’ID de segment. Ce champ doit être marqué comme identité principale et affecté aux espaces de noms que vous avez créés précédemment.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Après `_id` comme identité principale, sélectionnez le titre du schéma, suivi de la bascule étiquetée **[!UICONTROL Profil]**. Sélectionner **[!UICONTROL Activer]** pour activer le schéma pour [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Désormais, ce schéma est activé pour le profil, l’identification principale étant affectée à l’espace de noms d’identité autre que l’identité de la personne que vous avez créé. Par conséquent, cela signifie que les métadonnées de segment importées dans la plate-forme à l’aide de ce schéma seront assimilées dans le profil sans être fusionnées avec d’autres données de profil associées aux personnes.

## Création d’un ensemble de données pour le schéma

Après avoir configuré le schéma, vous devez créer un ensemble de données pour les métadonnées de segment.

Pour créer un ensemble de données, suivez les instructions de la section [guide de l&#39;utilisateur dataset](../../catalog/datasets/user-guide.md#create). Vous voudrez suivre le **[!UICONTROL Créer un ensemble de données à partir du schéma]** , à l’aide du schéma que vous avez créé précédemment.

![](../images/tutorials/external-audiences/select-schema.png)

Après avoir créé le jeu de données, suivez les instructions de la section [guide de l&#39;utilisateur dataset](../../catalog/datasets/user-guide.md#enable-profile) pour activer ce jeu de données pour le profil client en temps réel.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configuration et importation des données d’audience

Une fois l&#39;ensemble de données activé, les données peuvent désormais être envoyées vers la plate-forme via l&#39;interface utilisateur ou à l&#39;aide des API Experience Platform. Pour assimiler ces données dans la plate-forme, vous devez créer une connexion de diffusion.

Pour créer une connexion de diffusion en continu, vous pouvez suivre les instructions de l’une des manières suivantes : [Didacticiel sur l’API](../../sources/tutorials/api/create/streaming/http.md) ou [Didacticiel sur l’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md).

Une fois que vous avez créé votre connexion de diffusion en continu, vous avez accès à votre point de terminaison de diffusion unique vers lequel vous pouvez envoyer vos données. Pour savoir comment envoyer des données à ces points de terminaison, lisez le fichier [didacticiel sur la diffusion des données d’enregistrement](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Création de segments à l’aide d’audiences importées

Une fois les publics importés configurés, ils peuvent être utilisés dans le cadre du processus de segmentation. Pour rechercher des publics externes, accédez au Créateur de segments, puis sélectionnez **[!UICONTROL Audiences]** dans le menu **[!UICONTROL Champs]** .

![](../images/tutorials/external-audiences/external-audiences.png)

## Étapes suivantes

Maintenant que vous pouvez utiliser des publics externes dans vos segments, vous pouvez utiliser le créateur de segments pour créer des segments. Pour savoir comment créer des segments, lisez la section [didacticiel sur la création de segments](./create-a-segment.md).
