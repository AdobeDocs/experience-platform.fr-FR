---
keywords: Experience Platform;insights;customer ai;popular topics
solution: Experience Platform
title: Découverte d’insights avec Customer AI
topic: Discovering insights
description: Customer AI fait partie d’Intelligent Services et permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper les prochaines actions de vos clients. Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 89%

---


# Découverte d’insights avec Customer AI

Customer AI fait partie d’Intelligent Services et permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper les prochaines actions de vos clients. Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.

Ce document sert de guide pour interagir avec les insights d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.

## Prise en main

Pour utiliser les insights relatifs à Customer AI, vous devez avoir à disposition une instance de service dont l’état d’exécution est réussi. Pour créer une instance de service, consultez [Configuration d’une instance](./configure.md)d’API client. Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

## Présentation de l’instance de service

In the [!DNL Adobe Experience Platform] UI, click **[!UICONTROL Services]** in the left navigation. Le navigateur *Services* apparaît et affiche les services intelligents disponibles. Dans le conteneur de Customer AI, cliquez sur **[!UICONTROL Ouvrir]**.

![Accès à votre instance](../images/insights/navigate-to-service.png)

La page de service de Customer AI s’affiche. Cette page répertorie les instances de service de Customer AI et affiche les informations les concernant, notamment le nom de l’instance, le type de propension, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour.

>[!NOTE]
>
>Seules les instances de service ayant réussi des exécutions de notation ont des insights.

![Création d’une instance](../images/insights/dashboard.png)

Cliquez sur le nom d’une instance de service pour commencer.

![Création d’une instance](../images/insights/click-the-name.png)

Ensuite, la page d’insights de cette instance de service apparaît, proposant des visualisations de vos données. Les visualisations et ce que vous pouvez faire avec ces données sont expliqués plus en détail dans ce guide.

![page de configuration](../images/insights/landing-page.png)


### Détails des instances de service

Il existe deux façons d’afficher les détails d’une instance de service. La première est issue du tableau de bord, la seconde de l’instance de service.

Pour afficher les détails depuis le tableau de bord, cliquez sur un conteneur d’instance de service en évitant le lien hypertexte associé au nom. Cela permet d’ouvrir un rail droit qui fournit des détails supplémentaires, tels que la description, la fréquence de notation, l’objectif de prévision et la population admissible. De plus, vous pouvez modifier et supprimer l’instance en cliquant sur **[!UICONTROL Modifier]** ou **[!UICONTROL Supprimer]**.

![rail droit](../images/insights/success-run.png)

>[!NOTE]
>
>En cas d’échec d’une exécution de notation, vous recevez un message d’erreur. Le message d’erreur est répertorié sous les *détails de la dernière exécution* dans le rail droit, qui est visible uniquement en cas d’exécutions ayant échoué.

![message d’échec d’exécution](../images/insights/failed-run.png)

La deuxième façon d’afficher des détails supplémentaires sur une instance de service se trouve sur la page des insights. Vous pouvez cliquer sur **[!UICONTROL Afficher plus]** en haut à droite pour remplir une liste déroulante. Les détails y sont répertoriés, tels que la définition du score, la date de création et le type de propension. For more information on any of the properties listed, please visit [Configuring a Customer AI instance](./configure.md).

![afficher plus](../images/insights/landing-show-more.png)

![afficher plus](../images/insights/show-more.png)

### Modification d’une instance

Pour modifier une instance, cliquez sur **[!UICONTROL Modifier]** dans la navigation en haut à droite.

![cliquez sur le bouton Modifier](../images/insights/edit-button.png)

La boîte de dialogue de modification s’affiche et vous permet de modifier la *description* et la *fréquence de notation* de l’instance. Pour confirmer vos modifications et fermer la boîte de dialogue, cliquez sur **[!UICONTROL Modifier]** dans le coin en bas à droite.

![modifier la fenêtre contextuelle](../images/insights/edit-instance.png)

### Actions supplémentaires

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. Cliquer sur **[!UICONTROL Actions supplémentaires]** ouvre un menu déroulant qui vous permet de sélection l’une des opérations suivantes :

- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Accéder aux scores]** : en cliquant sur *Accéder aux scores*, vous ouvrez une boîte de dialogue contenant un lien vers le tutoriel sur le [téléchargement des scores pour Customer AI](./download-scores.md). La boîte de dialogue fournit également l’identifiant de jeu de données requis pour effectuer des appels d’API.
- **[!UICONTROL Afficher l’historique d’exécution]** : fait apparaître une boîte de dialogue contenant une liste des exécutions de notation associées à l’instance de service.

![actions supplémentaires](../images/insights/more-actions.png)

## Résumé de notation {#scoring-summary}

Le résumé de notation affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible. Les compartiments de propension sont déterminés en fonction de la plage de scores : la propension faible est inférieure à 24, la propension moyenne est comprise entre 25 et 74, et la propension élevée est supérieure à 74. Chaque compartiment a une couleur en fonction de la légende.

>[!NOTE]
>
>S’il s’agit d’un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

![résumé de notation](../images/insights/scoring-summary.png)

## Distribution des scores

La carte *Distribution des scores* vous donne un résumé visuel de la population en fonction du score. Les couleurs présentes sur la carte *Distribution des scores* représentent le type de score de propension généré.

![distribution des scores](../images/insights/distribution-of-scores.png)

## Facteurs d’influence

Une carte est générée pour chaque compartiment de score, présentant les 10 principaux facteurs d’influence pour ce compartiment. Les facteurs d’influence vous donnent des détails supplémentaires sur la raison pour laquelle vos clients appartiennent à différents compartiments de score.

![facteurs d’influence](../images/insights/influential-factors.png)

### Création d’un segment

Cliquer sur le bouton **[!UICONTROL Créer un segment]** dans l’un des compartiments de propension faible, moyenne ou élevée vous redirige vers le créateur de segments.

>[!NOTE]
>
>Le bouton **[!UICONTROL Créer un segment]** n’est disponible que si le Profil client en temps réel est activé pour le jeu de données. Pour plus d’informations sur la façon d’activer le Profil client en temps réel, consultez la présentation [du Profil client en temps](../../../rtcdp/overview.md)réel.

![Cliquez sur Créer un segment](../images/insights/influential-factors-create-segment.png)

![Création d’un segment](../images/insights/create-segment.png)

Le créateur de segments permet de définir un segment. Lorsque vous sélectionnez **[!UICONTROL Créer un segment]** dans la page Statistiques, l’API du client ajoute automatiquement les informations de regroupement sélectionnées au segment. Pour terminer la création de votre segment, il vous suffit de renseigner les conteneurs *Nom* et *Description* situés dans le rail droit de l’interface utilisateur du créateur de segments. Après avoir donné un nom et une description au segment, cliquez sur **[!UICONTROL Enregistrer]** en haut à droite.

>[!NOTE]
>
>Puisque les scores de propension sont écrits dans chaque profil individuel, ils sont disponibles dans le créateur de segments comme tout autre attribut de profil. Lorsque vous accédez au créateur de segments pour créer des segments, vous pouvez voir tous les scores de propension sous le Customer AI de votre espace de noms.

![Remplissage de segment](../images/insights/segment-saving.png)

Pour afficher le nouveau segment dans l’interface utilisateur de Platform, cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche. La page *Parcourir* apparaît et affiche tous les segments disponibles.

![Tous vos segments](../images/insights/Segments-dashboard.png)

## Étapes suivantes

Ce document décrit les insights fournis par une instance de service Customer AI. Vous pouvez maintenant passer au tutoriel sur le [téléchargement de scores dans Customer AI](./download-scores.md) ou consulter les autres guides proposés sur [Adobe Intelligent Services](../../home.md).

## Ressources supplémentaires

La vidéo suivante explique comment utiliser l’IA du client pour visualiser la sortie des modèles et des facteurs influents.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)