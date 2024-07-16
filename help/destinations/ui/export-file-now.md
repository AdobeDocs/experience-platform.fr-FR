---
title: (Version bêta) Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur Experience Platform
type: Tutorial
description: Découvrez comment exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur de l’Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 64833e29d062225bc774a14ae60b102b293bb5c4
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 21%

---

# (Version bêta) Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur Experience Platform

>[!IMPORTANT]
>
>L’option **[!UICONTROL Exporter le fichier maintenant]** de Adobe Experience Platform se trouve actuellement dans Beta. La documentation et les fonctionnalités peuvent changer.
>Contactez votre représentant Adobe pour accéder à cette fonctionnalité.

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

## Vue d&#39;ensemble de l’**[!UICONTROL export de fichier maintenant]**  {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exporter le fichier maintenant"
>abstract="Sélectionnez ce contrôle pour livrer une exportation complète de fichiers en plus des exportations précédemment programmées. L&#39;exportation du fichier est déclenchée immédiatement et récupère les derniers résultats des exécutions de segmentation d&#39;Experience Platform."

Cet article explique comment utiliser l’interface utilisateur de l’Experience Platform pour exporter des fichiers à la demande vers des destinations par lots telles que des destinations de [stockage dans le cloud](/help/destinations/catalog/cloud-storage/overview.md) et de [ marketing par e-mail](/help/destinations/catalog/email-marketing/overview.md).

Le contrôle **[!UICONTROL Export de fichier now]** permet d&#39;exporter un fichier complet sans interrompre le planning d&#39;export actuel d&#39;une audience précédemment planifiée. Cet export s&#39;effectue en plus des exports précédemment programmés et ne modifie pas la fréquence d&#39;export de l&#39;audience. L&#39;exportation du fichier est déclenchée immédiatement et récupère les derniers résultats des exécutions de segmentation d&#39;Experience Platform.

Vous pouvez également utiliser les API Experience Platform à cet effet. Lisez comment [activer des audiences à la demande vers des destinations par lot via l’API d’activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Conditions préalables {#prerequisites}

Pour exporter des fichiers à la demande vers des destinations par lot, [ doit être connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Comment exporter des fichiers à la demande {#how-to-export-files-on-demand}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, sélectionnez l’onglet **[!UICONTROL Parcourir]** et le symbole de filtre pour afficher les connexions existantes aux destinations par lots de votre choix.

   ![Image mettant en surbrillance la manière d’accéder à l’onglet de navigation et de filtrer les flux de données existants.](../assets/ui/activate-on-demand/browse-tab.png)

2. Sélectionnez la connexion de destination souhaitée pour inspecter le flux de données existant vers la destination.

   ![Image mettant en surbrillance un flux de données filtré.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Sélectionnez l’onglet **[!UICONTROL Données d’activation]** et sélectionnez les audiences pour lesquelles vous souhaitez exporter des fichiers à la demande, puis sélectionnez le contrôle **[!UICONTROL Exporter le fichier maintenant]** afin de déclencher une exportation unique qui diffusera un fichier pour chaque audience sélectionnée vers votre destination de lot.

   ![Image mettant en surbrillance le bouton Exporter le fichier maintenant.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Sélectionnez **[!UICONTROL Oui]** pour confirmer et déclencher l’exportation du fichier.

   ![Image montrant la boîte de dialogue de confirmation de l&#39;export du fichier maintenant.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Un message de confirmation s&#39;affiche, vous indiquant que l&#39;export du fichier a démarré.

   ![Image montrant la confirmation de l’activation ad hoc réussie.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Vous pouvez également basculer vers l’onglet **[!UICONTROL Exécution du flux de données]** pour confirmer que l’exportation du fichier a démarré.

## Considérations {#considerations}

Gardez à l’esprit les points suivants lorsque vous utilisez le contrôle **[!UICONTROL Export file now]** :

* **[!UICONTROL L’export de fichier maintenant]** fonctionne uniquement pour les audiences dont le planning dans le flux de données d’activation par lots chevauche la date actuelle. Cela inclut les audiences avec des plannings qui n’ont pas de date de fin (fréquence d’exportation de **[!UICONTROL Once]**) ou dont la date de fin n’a pas encore été dépassée.
* Lors de l’ajout d’une audience à un flux de données existant, attendez au moins 15 minutes avant d’utiliser le contrôle **[!UICONTROL Exporter le fichier maintenant]**.
* Si vous modifiez la stratégie de fusion d’une audience ou si vous créez une audience qui utilise une nouvelle stratégie de fusion, patientez 24 heures jusqu’à l’utilisation du contrôle **[!UICONTROL Export file now]**.

## Messages d’erreur de l’interface utilisateur {#ui-error-messages}

Lors de l&#39;utilisation du contrôle **[!UICONTROL Export file now]** , il se peut que vous rencontriez l&#39;un des messages d&#39;erreur répertoriés ci-dessous. Consultez le tableau pour savoir comment y remédier lorsqu’il s’affiche.

| Message d’erreur | Résolution |
|---------|----------|
| Exécutez déjà pour l&#39;audience `segment ID` de la commande `dataflow ID` avec l&#39;identifiant d&#39;exécution `flow run ID` | Ce message d’erreur indique qu’un flux d’activation ad hoc est actuellement en cours pour une audience. Attendez que la tâche se termine avant de déclencher à nouveau la tâche d’activation. |
| Les audiences `<segment name>` ne font pas partie de ce flux de données ou ne font pas partie de la plage de planification ! | Ce message d’erreur indique que les audiences que vous avez sélectionnées pour activer ne sont pas mappées au flux de données ou que le planning d’activation configuré pour les audiences a expiré ou n’a pas encore commencé. Vérifiez si l’audience est bien mappée au flux de données et que le planning d’activation de l’audience chevauche la date actuelle. |

## Informations connexes {#related-information}

* [Activation des audiences vers des destinations par lots à la demande à l’aide des API Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md)
