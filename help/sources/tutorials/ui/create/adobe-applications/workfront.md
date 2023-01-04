---
keywords: Experience Platform;accueil;rubriques populaires;
title: (Version bêta) Créer une connexion source Adobe Workfront dans l’interface utilisateur
description: Ce tutoriel décrit les étapes à suivre pour créer une connexion source Adobe Workfront afin d’importer vos données Workfront dans Adobe Experience Platform à l’aide de l’interface utilisateur.
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 97%

---

# (Version bêta) Créer une connexion source Adobe Workfront dans l’interface utilisateur

>[!NOTE]
>
>La source Adobe Workfront est en version bêta. Voir la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta. 

Ce tutoriel décrit les étapes à suivre pour créer une connexion source Adobe Workfront afin d’importer vos données Workfront dans Adobe Experience Platform à l’aide de l’interface utilisateur.

## Prise en main

>[!IMPORTANT]
>
>Vous devez être configuré en tant qu’administrateur dans Adobe Admin Console pour accéder à la source Workfront.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Profil client en temps réel](../../../../../profile/home.md): Fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Créer une connexion source Workfront dans l’interface utilisateur

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pouvant être utilisées pour créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour réduire les sources affichées.

Dans la catégorie des **[!UICONTROL Applications Adobe]**, sélectionnez **[!UICONTROL Adobe Workfront]**, puis **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources avec la source Adobe Workfront mise en surbrillance.](../../../../images/tutorials/create/workfront/catalog.png)

## Sélectionner les données

L’étape [!UICONTROL Sélectionner des données] apparaît. Ici, vous devez fournir des valeurs pour votre sous-domaine Workfront et votre Datalane. Votre sous-domaine Workfront a la même URL que celle que vous utilisez pour accéder à votre instance Workfront, par exemple `https://acme.workfront.com/`, tandis que votre Datalane représente l’environnement Workfront que vous souhaitez utiliser.

Une fois que vous avez ajouté votre sous-domaine et votre Datalane, sélectionnez **[!UICONTROL Suivant]**.

![La page de sélection des données avec des valeurs d’espace réservé pour le sous-domaine et le Datalane.](../../../../images/tutorials/create/workfront/select-data.png)

## Fournir des détails sur le flux de données

L’étape Détails du flux de données vous permet de fournir un nom et une description facultative pour votre flux de données. Au cours de cette étape, vous pouvez également vous abonner à des alertes pour recevoir des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le tutoriel sur l’[abonnement aux alertes pour les sources dans l’interface utilisateur](../../alerts.md).

Une fois que vous avez fourni les détails du flux de données et configuré les paramètres d’alerte souhaités, sélectionnez **[!UICONTROL Suivant]**.

![Page de détails du flux de données contenant des informations sur le nom, la description du flux de connées et les notifications d’alerte](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Révision

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![Page de vérification résumant les informations de connexion.](../../../../images/tutorials/create/workfront/review.png)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur la source Workfront.

### Schéma Événement de changement Workfront

Les données Workfront dans Platform sont représentées sous la forme de données d’enregistrement de série temporelle, où chaque ligne des données comporte une date et une heure du moment où l’événement s’est produit et les attributs associés à cet événement.

Lors de la configuration, un schéma appelé Événements de changement Workfront à partir du flux est créé.

| Champ de schéma | Description |
| --- | --- |
| `timestamp` | Heure à laquelle l’événement sélectionné s’est produit. La date et l’heure sont indiquées dans le fuseau horaire GMT. |
| `_workfront.objectType` | Le type d’objet. Les valeurs disponibles peuvent inclure `project`, `task`, `portfolio`, etc., selon l’objet modifié ou créé. |
| `_workfront.objectID` | Identifiant qui correspond au type d’objet. |
| `_workfront.created` | Cette valeur est définie sur `1` si l’événement représente une création d’objet. |
| `_workfront.deleted` | Cette valeur est définie sur `1` si l’objet est supprimé. |
| `_worfkront.updated` | Cette valeur est définie sur `1` si l’objet est mis à jour. |
| `_workfront.completed` | Cette valeur est définie sur `1` si l’objet est marqué comme terminé. |
| `_workfront.parentObjectType` | (Facultatif) Type d’objet qui correspond au parent de l’objet. |
| `_workfront.parentID` | Identifiant de l’objet parent. |
| `_workfront.customData` | Mappage de tous les champs et valeurs de formulaire personnalisés renseignés lors de l’événement. |

>[!IMPORTANT]
>
>Seuls les attributs qui ont été modifiés ou créés dans le cadre d’un événement sont renseignés. Par exemple, si vous modifiez uniquement le nom de l’objet, alors seuls les champs suivants seront renseignés :<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Étapes suivantes

En suivant ce tutoriel, vous avez à présent créé un flux de données pour importer vos données de Workfront vers Experience Platform. Vous pouvez désormais utiliser des services tels que [Query Service](../../../../../query-service/home.md) pour exécuter une analyse plus approfondie de vos données. Pour plus d’informations sur Workfront, reportez-vous à la section [Présentation de Workfront](../../../../connectors/adobe-applications/workfront.md).
