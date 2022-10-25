---
keywords: Experience Platform;accueil;rubriques populaires;
title: Création d’une connexion source Adobe Workfront dans l’interface utilisateur
description: Ce tutoriel décrit les étapes à suivre pour créer une connexion source Adobe Workfront afin d’importer vos données Workfront dans Adobe Experience Platform à l’aide de l’interface utilisateur.
source-git-commit: 99741a3be4d50d1a812e945483c9ed1577a0a999
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 21%

---

# Création d’une connexion source Adobe Workfront dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source Adobe Workfront afin d’importer vos données Workfront dans Adobe Experience Platform à l’aide de l’interface utilisateur.

## Prise en main

>[!IMPORTANT]
>
>Vous devez être configuré en tant qu’administrateur dans Adobe Admin Console pour accéder à la source Workfront.

Ce tutoriel nécessite une compréhension pratique des composants suivants de l’Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sandboxes](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Création d’une connexion source Workfront dans l’interface utilisateur

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Le [!UICONTROL Catalogue] affiche diverses sources pouvant être utilisées pour créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour réduire les sources affichées.

Sous , **[!UICONTROL Adobe des applications]** catégorie, sélectionnez **[!UICONTROL Adobe Workfront]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources avec la source Adobe Workfront mise en surbrillance.](../../../../images/tutorials/create/workfront/catalog.png)

## Sélectionner les données

Le [!UICONTROL Sélectionner des données] s’affiche. Ici, vous devez fournir des valeurs pour votre sous-domaine Workfront et votre Datalane. Votre sous-domaine Workfront est la même URL que celle que vous utilisez pour accéder à votre instance Workfront, par exemple `https://acme.workfront.com/`, tandis que votre jeu de données représente l’environnement de travail que vous souhaitez utiliser.

Une fois que vous avez ajouté votre sous-domaine et votre couche de données, sélectionnez **[!UICONTROL Suivant]**.

![La page de sélection de données avec des valeurs d’espace réservé pour le sous-domaine et le canal de données.](../../../../images/tutorials/create/workfront/select-data.png)

## Fournir des détails sur le flux de données

L’étape de détail du flux de données vous permet de fournir un nom et une description facultative de votre flux de données. Au cours de cette étape, vous pouvez également vous abonner à des alertes pour recevoir des notifications concernant l’état de votre flux de données. Pour plus d’informations sur les alertes, consultez le tutoriel sur [abonnement aux alertes dans l’interface utilisateur des sources](../../alerts.md).

Une fois que vous avez fourni les détails du flux de données et configuré les paramètres d’alerte souhaités, sélectionnez **[!UICONTROL Suivant]**.

![Page de détails du flux de données contenant des informations sur le nom, la description et les notifications d’alerte du flux de données](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Révision

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]**: Affiche le type de source, le chemin d’accès approprié du fichier source choisi et la quantité de colonnes qu’il contient.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et accorder un certain temps pour la création du flux de données.

![Page de révision résumant les informations de connexion.](../../../../images/tutorials/create/workfront/review.png)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur la source Workfront.

### Schéma d’événement de modification Workfront

Les données Workfront dans Platform sont représentées sous la forme de données d’enregistrement de série temporelle, où chaque ligne des données comporte un horodatage qui s’affiche lorsque l’événement s’est produit et les attributs liés à cet événement.

Lors de la configuration, un schéma appelé Événements de changement Workfront à partir du flux est créé.

| Champ de schéma | Description |
| --- | --- |
| `timestamp` | Heure à laquelle l’événement sélectionné s’est produit. L’horodatage est représenté dans le fuseau horaire de GTM. |
| `_workfront.objectType` | Type d’objet. Les valeurs disponibles peuvent inclure `project`, `task`, `portfolio`, etc., selon l’objet modifié ou créé. |
| `_workfront.objectID` | Identifiant qui correspond au type d’objet. |
| `_workfront.created` | Cette valeur est définie sur `1` si l’événement représente une création d’objet. |
| `_workfront.deleted` | Cette valeur est définie sur `1` si l’objet est supprimé. |
| `_worfkront.updated` | Cette valeur est définie sur `1` si l’objet est mis à jour. |
| `_workfront.completed` | Cette valeur est définie sur `1` si l’objet est marqué comme terminé. |
| `_workfront.parentObjectType` | (Facultatif) Type d’objet qui correspond au parent de l’objet. |
| `_workfront.parentID` | L’identifiant de l’objet parent. |
| `_workfront.customData` | Mappage de tous les champs et valeurs de formulaire personnalisés renseignés lors de l’événement. |

>[!IMPORTANT]
>
>Seuls les attributs qui ont été modifiés ou créés dans le cadre d’un événement sont renseignés. Par exemple, si vous modifiez uniquement le nom de l’objet, les seuls champs qui seront renseignés sont les suivants :<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Étapes suivantes

En suivant ce tutoriel, vous avez maintenant créé un flux de données pour importer vos données de Workfront vers Experience Platform. Vous pouvez désormais utiliser des services tels que [Query Service](../../../../../query-service/home.md) pour exécuter une analyse plus approfondie de vos données. Pour plus d’informations sur Workfront, reportez-vous à la section [Présentation de Workfront](../../../../connectors/adobe-applications/workfront.md).