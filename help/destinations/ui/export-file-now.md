---
title: Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur d’Experience Platform
type: Tutorial
description: Découvrez comment exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur d’Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: d3bd76f5b36b6a6afcb67fe923eb8e4f3d7a9415
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 16%

---


# Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur d’Experience Platform

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

## Vue d&#39;ensemble de l’**[!UICONTROL export de fichier maintenant]**  {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exporter le fichier maintenant"
>abstract="Sélectionnez ce contrôle pour livrer un export de fichiers complet en plus des exports planifiés précédemment. L&#39;exportation du fichier est déclenchée immédiatement et récupère les derniers résultats des exécutions de segmentation d&#39;Experience Platform."

Cet article explique comment utiliser l’interface utilisateur d’Experience Platform pour exporter des fichiers à la demande vers des destinations par lots telles que [espace de stockage dans le cloud](/help/destinations/catalog/cloud-storage/overview.md) et [marketing par e-mail](/help/destinations/catalog/email-marketing/overview.md).

Le contrôle **[!UICONTROL Exporter le fichier maintenant]** vous permet d’exporter un fichier complet sans interrompre le planning d’exportation actuel d’une audience précédemment planifiée. Cette exportation s’ajoute aux exportations précédemment planifiées. Elle ne modifie pas la fréquence d’exportation de l’audience. L&#39;exportation du fichier est déclenchée immédiatement et récupère les derniers résultats des exécutions de segmentation d&#39;Experience Platform.

Vous pouvez également utiliser les API d’Experience Platform à cet effet. Découvrez comment [activer des audiences à la demande vers des destinations par lots via l’API d’activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Conditions préalables {#prerequisites}

Pour exporter des fichiers à la demande vers des destinations par lots, vous devez avoir réussi [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Exporter des fichiers à la demande {#how-to-export-files-on-demand}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, sélectionnez l’onglet **[!UICONTROL Parcourir]** et le symbole de filtre pour afficher les connexions existantes aux destinations par lots de votre choix.

   ![Image mettant en surbrillance comment accéder à l’onglet de navigation et filtrer les flux de données existants.](../assets/ui/activate-on-demand/browse-tab.png)

2. Sélectionnez la connexion de destination souhaitée pour inspecter le flux de données existant vers la destination.

   ![Image mettant en surbrillance un flux de données filtré.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Sélectionnez l’onglet **[!UICONTROL Données d’activation]**, sélectionnez les audiences pour lesquelles vous souhaitez exporter des fichiers à la demande et sélectionnez le contrôle **[!UICONTROL Exporter le fichier maintenant]** pour déclencher une exportation unique qui diffusera un fichier pour chaque audience sélectionnée vers votre destination par lots.

   ![Image mettant en surbrillance le bouton Exporter le fichier maintenant.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Sélectionnez **[!UICONTROL Oui]** pour confirmer et déclencher l’exportation du fichier.

   ![Image illustrant la boîte de dialogue de confirmation Exporter le fichier maintenant.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Un message de confirmation s’affiche, vous informant que l’exportation du fichier a commencé.

   ![Image montrant la confirmation de la réussite de l’activation ad hoc.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Vous pouvez également passer à l’onglet **[!UICONTROL Exécutions de flux de données]** pour confirmer que l’exportation du fichier a démarré.

## Considérations {#considerations}

Gardez à l’esprit les points suivants lors de l’utilisation du contrôle **[!UICONTROL Exporter le fichier maintenant]** :

* Le **[!UICONTROL Exporter le fichier maintenant]** fonctionne uniquement pour les audiences dont le planning du flux de données d’activation par lots chevauche la date actuelle. Cela inclut les audiences avec des plannings qui n’ont pas de date de fin (fréquence d’exportation de **[!UICONTROL Une fois]**) ou pour lesquelles la date de fin n’est pas encore passée.
* Lors de l’ajout d’une audience à un flux de données existant, attendez au moins **une heure** avant d’utiliser le contrôle **[!UICONTROL Exporter le fichier maintenant]**.
* Si vous modifiez la politique de fusion d’une audience ou si vous créez une audience qui utilise une nouvelle politique de fusion, attendez 24 heures avant d’utiliser le contrôle **[!UICONTROL Exporter le fichier maintenant]**.

## Messages d’erreur de l’interface utilisateur {#ui-error-messages}

Lors de l’utilisation du contrôle **[!UICONTROL Exporter le fichier maintenant]**, vous pouvez rencontrer l’un des messages d’erreur répertoriés ci-dessous. Consultez le tableau pour comprendre comment y remédier lorsqu’ils apparaissent.

| Message d’erreur | Résolution |
|---------|----------|
| Exécution déjà en cours pour l’audience `segment ID` pour la commande `dataflow ID` avec l’ID d’exécution `flow run ID` | Ce message d’erreur indique qu’un flux d’activation ad hoc est actuellement en cours pour une audience. Attendez que le traitement se termine avant de déclencher à nouveau le traitement d’activation. |
| Les audiences `<segment name>` ne font pas partie de ce flux de données ou sont hors plage de planification. | Ce message d’erreur indique que les audiences que vous avez sélectionnées pour activation ne sont pas mappées au flux de données ou que le planning d’activation configuré pour les audiences a expiré ou n’a pas encore commencé. Vérifiez si l’audience est bien mappée au flux de données et que le planning d’activation de l’audience chevauche la date actuelle. |

## Informations connexes {#related-information}

* [Activer des audiences vers des destinations par lots à la demande à l’aide des API Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md)
