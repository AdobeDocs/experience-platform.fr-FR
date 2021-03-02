---
keywords: destinations ; destination ; page des détails des destinations ; page des détails des destinations ; page des détails des destinations
title: Détails de la destination de la vue
description: 'La page de détails d’une destination individuelle offre un aperçu des détails de la destination, tels que le nom de destination, l’identifiant, les segments mappés à la destination et les commandes permettant de modifier l’activation, d’activer et de désactiver le flux de données. '
seo-description: 'La page de détails d’une destination individuelle offre un aperçu des détails de la destination, tels que le nom de destination, l’identifiant, les segments mappés à la destination et les commandes permettant de modifier l’activation, d’activer et de désactiver le flux de données. '
translation-type: tm+mt
source-git-commit: 9305936ca1e73821b2fe948ff1a17a7168840cba
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 15%

---


# Détails de la destination de la vue

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez vue et surveiller les attributs et les activités de vos destinations. Ces détails comprennent le nom et l’ID de la destination, les contrôles permettant d’activer ou de désactiver les destinations, etc. Les détails des destinations par lot incluent également des mesures pour les enregistrements de profil activés et un historique des exécutions de flux de données.

>[!NOTE]
>
>La page Détails des destinations fait partie de l&#39;espace de travail [!UICONTROL Destinations] dans l&#39;interface utilisateur de la plate-forme. Pour plus d&#39;informations, consultez la présentation de l&#39;espace de travail [[!UICONTROL Destinations]](./destinations-workspace.md).

Dans l&#39;espace de travail **[!UICONTROL Destinations]** de l&#39;interface utilisateur de la plate-forme, accédez à l&#39;onglet **[!UICONTROL Parcourir]** et sélectionnez le nom d&#39;une destination que vous souhaitez vue.

![](../assets/ui/details-page/select-destination.png)

La page de détails de la destination s’affiche, avec les commandes disponibles. Si vous visualisez les détails d’une destination par lot, un tableau de bord de contrôle s’affiche également.

![](../assets/ui/details-page/details.png)

De plus, dans l’onglet Parcourir, vous pouvez choisir de supprimer le flux de données sélectionné en sélectionnant l’icône ![corbeille](../assets/ui/details-page/trash-icon.png). Tout segment activé sur une destination est démappé avant la suppression du flux de données.

![](../assets/ui/details-page/delete-flow.png)

## Rail droit

Le rail droit affiche les informations de base sur la destination.

![](../assets/ui/details-page/right-rail.png)

Le tableau suivant couvre les contrôles et les détails fournis par le rail droit :

| Article de rail droit | Description |
| --- | --- |
| [!UICONTROL Activer] | Sélectionnez ce contrôle pour modifier les segments mappés à la destination. Pour plus d&#39;informations, consultez le guide sur l&#39;[activation de segments vers une destination](./activate-destinations.md). |
| [!UICONTROL Supprimer] | Vous permet de supprimer ce flux de données et de démapper les segments qui ont été activés auparavant, le cas échéant. |
| [!UICONTROL Nom de destination] | Ce champ peut être modifié afin de mettre à jour le nom de la destination. |
| [!UICONTROL Description] | Ce champ peut être modifié pour mettre à jour ou ajouter une description facultative à la destination. |
| [!UICONTROL Destination] | Représente la plateforme de destination vers laquelle les audiences sont envoyées. Pour plus d&#39;informations, consultez le [catalogue de destinations](../catalog/overview.md). |
| [!UICONTROL État] | Indique si la destination est activée ou désactivée. |
| [!UICONTROL Actions marketing] | Indique les actions marketing (cas d’utilisation) qui s’appliquent à cette destination à des fins de gouvernance des données. |
| [!UICONTROL Catégorie] | Indique le type de destination. Pour plus d&#39;informations, consultez le [catalogue de destinations](../catalog/overview.md). |
| [!UICONTROL Type de connexion] | Indique le formulaire sous lequel vos audiences sont envoyées à la destination. Les valeurs possibles sont &quot;[!UICONTROL Cookie]&quot; et &quot;[!UICONTROL Profil-based]&quot;. |
| [!UICONTROL Fréquence] | Indique la fréquence d’envoi des audiences vers la destination. Les valeurs possibles sont &quot;[!UICONTROL Streaming]&quot; et &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identité] | Représente l’espace de nommage d’identité accepté par la destination, par exemple `GAID`, `IDFA` ou `email`. Pour plus d&#39;informations sur les espaces de nommage d&#39;identité acceptés, consultez la [présentation de l&#39;espace de nommage d&#39;identité](../../identity-service/namespaces.md). |
| [!UICONTROL Créé par] | Indique l’utilisateur qui a créé cette destination. |
| [!UICONTROL Créé] | Indique la date UTC au moment de la création de cette destination. |

## [!UICONTROL Activé]/ Désactivé

Vous pouvez utiliser la bascule **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour début et suspendre toutes les exportations de données vers la destination.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Exécutions de flux de données]

L&#39;onglet [!UICONTROL Flux de données] fournit des données de mesure sur vos flux de données s&#39;exécutant vers des destinations de lot. Une liste d’exécutions individuelles et de leurs mesures particulières s’affiche, ainsi que les totaux suivants pour les enregistrements de profil :

* **[!UICONTROL Enregistrements de profil activés]** : Nombre total d&#39;enregistrements de profil créés ou mis à jour pour l&#39;activation.
* **[!UICONTROL Enregistrements de profil ignorés]** : Nombre total d’enregistrements de profil qui sont ignorés pour activation en fonction des sorties de profil ou des attributs manquants.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Les exécutions de flux de données sont générées en fonction de la fréquence de planification du flux de données de destination. Une exécution de flux de données distincte est effectuée pour chaque stratégie de fusion appliquée à un segment.

Pour vue les détails d&#39;une exécution de flux de données particulière, sélectionnez l&#39;heure de début de l&#39;exécution dans la liste. La page Détails d&#39;une série de flux de données contient des informations supplémentaires, telles que la taille des données traitées et la liste de toute erreur survenue avec des détails pour les diagnostics d&#39;erreur.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Données d’Activation] {#activation-data}

L&#39;onglet [!UICONTROL Données d&#39;Activation] affiche une liste de segments qui ont été mappés à la destination, y compris leur date de début et leur date de fin (le cas échéant). Pour vue les détails d’un segment particulier, sélectionnez son nom dans la liste.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Pour plus d&#39;informations sur l&#39;exploration de la page de détails d&#39;un segment, consultez la [Présentation de l&#39;interface utilisateur de segmentation](../../segmentation/ui/overview.md#segment-details).

## Étapes suivantes

Ce document couvrait les fonctionnalités de la page des détails de destination. Pour plus d&#39;informations sur la gestion des destinations dans l&#39;interface utilisateur, consultez la présentation de l&#39;espace de travail [[!UICONTROL Destinations]](./destinations-workspace.md).