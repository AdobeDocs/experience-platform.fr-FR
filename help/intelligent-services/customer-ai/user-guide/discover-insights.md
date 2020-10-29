---
keywords: Experience Platform;insights;customer ai;popular topics;customer ai insights
solution: Experience Platform
title: Découverte d’insights avec Customer AI
topic: Discovering insights
description: Ce document sert de guide pour interagir avec les insights d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.
translation-type: tm+mt
source-git-commit: 0b92346065b7c9615d8aef4c9b13c84e0383b4b9
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 55%

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

Il existe deux façons de vue des détails de l’instance de service : du tableau de bord ou dans l’instance de service.

Pour vue une vue d’ensemble des détails de l’instance de service dans le tableau de bord, sélectionnez un conteneur d’instance de service, en évitant l’hyperlien associé au nom. Ceci ouvre un rail droit qui fournit des détails supplémentaires. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]**: La sélection de **[!UICONTROL Modifier]** vous permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence d’évaluation de l’instance.
- **[!UICONTROL Cloner]**: Lorsque vous sélectionnez **[!UICONTROL Cloner]** , l’instance de service sélectionnée est copiée. Vous pouvez ensuite modifier le processus pour effectuer des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]**: Vous pouvez supprimer une instance de service, y compris les exécutions historiques.
- **[!UICONTROL Source]** de données : Lien vers le jeu de données utilisé par cette instance.
- **[!UICONTROL Fréquence]** d&#39;exécution : Fréquence d’une série de notes et quand.
- **[!UICONTROL Définition]** de note : Aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>En cas d’échec d’une exécution de notation, vous recevez un message d’erreur. Le message d’erreur est répertorié sous les **détails de la dernière exécution** dans le rail droit, qui est visible uniquement en cas d’exécutions ayant échoué.

![message d’échec d’exécution](../images/insights/failed-run.png)

La deuxième façon d’afficher des détails supplémentaires sur une instance de service se trouve sur la page des insights. Vous pouvez cliquer sur **[!UICONTROL Afficher plus]** en haut à droite pour remplir une liste déroulante. Les détails y sont répertoriés, tels que la définition du score, la date de création et le type de propension. For more information on any of the properties listed, please visit [Configuring a Customer AI instance](./configure.md).

![afficher plus](../images/insights/landing-show-more.png)

![afficher plus](../images/insights/show-more.png)

### Modification d’une instance

Pour modifier une instance, cliquez sur **[!UICONTROL Modifier]** dans la navigation en haut à droite.

![cliquez sur le bouton Modifier](../images/insights/edit-button.png)

La boîte de dialogue Modifier s’affiche, vous permettant de modifier le nom, la description, l’état et la fréquence de notation de l’instance. To confirm your changes and close the dialog, select **[!UICONTROL Save]** in the bottom-right corner.

![modifier la fenêtre contextuelle](../images/insights/edit-instance.png)

### Actions supplémentaires

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. Cliquer sur **[!UICONTROL Actions supplémentaires]** ouvre un menu déroulant qui vous permet de sélection l’une des opérations suivantes :

- **[!UICONTROL Cloner]**: Si vous sélectionnez **[!UICONTROL Cloner]** , l’instance de service configurée est copiée. Vous pouvez ensuite modifier le processus pour effectuer des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Scores]** d&#39;accès : La sélection de scores **** Access ouvre une boîte de dialogue fournissant un lien vers les scores de [téléchargement du didacticiel d’API](./download-scores.md) client. Elle fournit également l’ID de jeu de données requis pour effectuer des appels d’API.
- **[!UICONTROL Afficher l’historique d’exécution]** : fait apparaître une boîte de dialogue contenant une liste des exécutions de notation associées à l’instance de service.

![actions supplémentaires](../images/insights/more-actions.png)

## Scoring summary {#scoring-summary}

Le résumé du score affiche le nombre total de profils marqués et les classe en compartiments contenant une propension élevée, moyenne et faible. Les compartiments de propension sont déterminés en fonction de la plage de scores : la propension faible est inférieure à 24, la propension moyenne est comprise entre 25 et 74, et la propension élevée est supérieure à 74. Chaque compartiment a une couleur en fonction de la légende.

>[!NOTE]
>
>S’il s’agit d’un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

![résumé de notation](../images/insights/scoring-summary.png)

Vous pouvez placer le pointeur de la souris sur n’importe quelle couleur de l’anneau pour vue d’autres informations, telles qu’un pourcentage et le nombre total de profils appartenant à un compartiment.

![](../images/insights/scoring-ring.png)

## Distribution des scores

La carte **[!UICONTROL Distribution des scores]** vous donne un résumé visuel de la population en fonction du score. Les couleurs présentes sur la carte [!UICONTROL Distribution des scores] représentent le type de score de propension généré. Le survol de l’une des distributions de score fournit le nombre exact qui appartient à cette distribution.

![distribution des scores](../images/insights/distribution-of-scores.png)

## Facteurs d’influence

Une carte est générée pour chaque compartiment de score, présentant les 10 principaux facteurs d’influence pour ce compartiment. Les facteurs d’influence vous donnent des détails supplémentaires sur la raison pour laquelle vos clients appartiennent à différents compartiments de score.

![facteurs d’influence](../images/insights/influential-factors.png)

### Pertes de facteurs influents

Le survol de l’un des principaux facteurs influents ventile les données. Vous obtenez un aperçu des raisons pour lesquelles certains profils appartiennent à un regroupement de propension. Selon le facteur, vous pouvez recevoir des valeurs numériques, catégoriques ou booléennes. L&#39;exemple ci-dessous affiche les valeurs catégoriques par région.

![capture d&#39;écran de la liste déroulante](../images/insights/drilldown.png)

En outre, en utilisant des analyses, vous pouvez comparer un facteur de distribution s’il se produit dans plusieurs groupes de propension et créer des segments plus spécifiques avec ces valeurs. L’exemple suivant illustre le premier cas d’utilisation :

![](../images/insights/drilldown-compare.png)

Vous pouvez constater que les profils ayant une faible propension à la conversion sont moins susceptibles d’avoir effectué une visite récente sur les pages Web adobe.com. Le facteur &quot;Jours depuis la dernière visite Web&quot; ne couvre que 8 %, contre 26 % dans les profils à tendance moyenne. A l’aide de ces chiffres, vous pouvez comparer la distribution dans chaque intervalle du facteur. Ces informations peuvent être utilisées pour déduire que la récence des visites sur le Web n&#39;a pas autant d&#39;influence dans le compartiment à faible propension que dans le compartiment à moyenne propension.

### Création d’un segment

Selecting the **[!UICONTROL Create Segment]** button in any of the buckets for low, medium, and high propensity redirects you to the segment builder.

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

Pour afficher le nouveau segment dans l’interface utilisateur de Platform, cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche. La page **[!UICONTROL Parcourir]** apparaît et affiche tous les segments disponibles.

![Tous vos segments](../images/insights/Segments-dashboard.png)

## Étapes suivantes

Ce document décrit les insights fournis par une instance de service Customer AI. Vous pouvez maintenant passer au tutoriel sur le [téléchargement de scores dans Customer AI](./download-scores.md) ou consulter les autres guides proposés sur [Adobe Intelligent Services](../../home.md).

## Ressources supplémentaires

La vidéo suivante explique comment utiliser l’IA du client pour visualiser la sortie des modèles et des facteurs influents.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)