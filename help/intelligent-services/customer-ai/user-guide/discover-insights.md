---
keywords: Experience Platform ; informations ; assistance client ; rubriques populaires ; informations client
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Découvrez des informations sur l'intelligence artificielle des clients
topic-legacy: Discovering insights
description: Ce document sert de guide pour interagir avec les insights d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 45%

---

# Découvrez des informations sur l&#39;intelligence artificielle des clients

Customer AI fait partie d’Intelligent Services et permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper les prochaines actions de vos clients. Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.

Ce document sert de guide pour interagir avec les insights d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.

## Prise en main

Pour utiliser les insights relatifs à Customer AI, vous devez avoir à disposition une instance de service dont l’état d’exécution est réussi. Pour créer une instance de service, rendez-vous sur [Configuration d’une instance d’API client](./configure.md). Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

## Présentation de l’instance de service

Dans l&#39;interface utilisateur [!DNL Adobe Experience Platform], cliquez sur **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur *Services* apparaît et affiche les services intelligents disponibles. Dans le conteneur de Customer AI, cliquez sur **[!UICONTROL Ouvrir]**.

![Accès à votre instance](../images/insights/navigate-to-service.png)

La page de service de Customer AI s’affiche. Cette page répertorie les instances de service de Customer AI et affiche les informations les concernant, notamment le nom de l’instance, le type de propension, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour.

>[!NOTE]
>
>Seules les instances de service ayant réussi des exécutions de notation ont des insights.

![Création d’une instance](../images/insights/dashboard.png)

Sélectionnez un nom d’instance de service à commencer.

![Création d’une instance](../images/insights/click-the-name.png)

Ensuite, la page d’informations de cette instance de service s’affiche avec l’option de sélectionner **[!UICONTROL scores les plus récents]** ou **[!UICONTROL Résumé des performances]**. L’onglet par défaut **[!UICONTROL Derniers scores]** fournit des visualisations de vos données. Les visualisations et ce que vous pouvez faire avec ces données sont expliqués plus en détail dans ce guide.

L&#39;onglet **[!UICONTROL Récapitulatif des performances]** affiche le ou les taux de conversion réels de chaque intervalle de propension. Pour en savoir plus, consultez la section [mesures récapitulatives de performances](#performance-metrics).

![page de configuration](../images/insights/landing_page_insights.png)

### Détails des instances de service

Il existe deux façons de vue des détails de l’instance de service : du tableau de bord ou dans l’instance de service.

Pour vue une vue d’ensemble des détails de l’instance de service dans le tableau de bord, sélectionnez un conteneur d’instance de service, en évitant l’hyperlien associé au nom. Ceci ouvre un rail droit qui fournit des détails supplémentaires. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]** : Le fait de sélectionner  **** Modifier vous permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence d’évaluation de l’instance.
- **[!UICONTROL Cloner]** : La sélection de  **** Clonecopies copie l’instance de service actuellement sélectionnée configurée. Vous pouvez ensuite modifier le processus pour effectuer des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]** : Vous pouvez supprimer une instance de service, y compris les exécutions historiques.
- **[!UICONTROL Source]** de données : Lien vers le jeu de données utilisé par cette instance.
- **[!UICONTROL Fréquence]** d&#39;exécution : Fréquence d’une série de notes et quand.
- **[!UICONTROL Définition]** de note : Aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>En cas d’échec d’une exécution de notation, vous recevez un message d’erreur. Le message d’erreur est répertorié sous les **détails de la dernière exécution** dans le rail droit, qui est visible uniquement en cas d’exécutions ayant échoué.

![message d’échec d’exécution](../images/insights/failed-run.png)

La deuxième façon d’afficher des détails supplémentaires sur une instance de service se trouve sur la page des insights. Vous pouvez cliquer sur **[!UICONTROL Afficher plus]** en haut à droite pour remplir une liste déroulante. Les détails y sont répertoriés, tels que la définition du score, la date de création et le type de propension. Pour plus d&#39;informations sur l&#39;une des propriétés répertoriées, consultez la page [Configuration d&#39;une instance d&#39;IA client](./configure.md).

![afficher plus](../images/insights/landing-show-more.png)

![afficher plus](../images/insights/show-more.png)

### Modification d’une instance

Pour modifier une instance, cliquez sur **[!UICONTROL Modifier]** dans la navigation en haut à droite.

![cliquez sur le bouton Modifier](../images/insights/edit-button.png)

La boîte de dialogue Modifier s’affiche, vous permettant de modifier le nom, la description, l’état et la fréquence de notation de l’instance. Pour confirmer vos modifications et fermer la boîte de dialogue, sélectionnez **[!UICONTROL Enregistrer]** dans le coin inférieur droit.

![modifier la fenêtre contextuelle](../images/insights/edit-instance.png)

### Actions supplémentaires

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. Cliquer sur **[!UICONTROL Actions supplémentaires]** ouvre un menu déroulant qui vous permet de sélection l’une des opérations suivantes :

- **[!UICONTROL Cloner]** : La sélection de  **** Clonecopies permet de copier l’instance de service configurée. Vous pouvez ensuite modifier le processus pour effectuer des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Scores]** d&#39;accès : La sélection des  **[!UICONTROL scores]** d&#39;accès ouvre une boîte de dialogue fournissant un lien vers les scores de  [téléchargement du didacticiel d&#39;](./download-scores.md) API du client. La boîte de dialogue fournit également l&#39;ID de jeu de données requis pour effectuer des appels d&#39;API.
- **[!UICONTROL Afficher l’historique d’exécution]** : fait apparaître une boîte de dialogue contenant une liste des exécutions de notation associées à l’instance de service.

![actions supplémentaires](../images/insights/more-actions.png)

## Récapitulatif des notes {#scoring-summary}

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

Si vous sélectionnez le bouton **[!UICONTROL Créer un segment]** dans l’un des compartiments pour une propension faible, moyenne et élevée, vous redirigez vers le créateur de segments.

>[!NOTE]
>
>Le bouton **[!UICONTROL Créer un segment]** n&#39;est disponible que si le Profil client en temps réel est activé pour le jeu de données. Pour plus d’informations sur la façon d’activer le Profil client en temps réel, consultez la [Présentation du Profil client en temps réel](../../../rtcdp/overview.md).

![Cliquez sur Créer un segment](../images/insights/influential-factors-create-segment.png)

![Création d’un segment](../images/insights/create-segment.png)

Le créateur de segments permet de définir un segment. Lors de la sélection de **[!UICONTROL Créer un segment]** dans la page Statistiques, l’API du client ajoute automatiquement les informations des intervalles sélectionnés au segment. Pour terminer la création de votre segment, il vous suffit de renseigner les conteneurs *Nom* et *Description* situés dans le rail droit de l’interface utilisateur du créateur de segments. Après avoir donné un nom et une description au segment, cliquez sur **[!UICONTROL Enregistrer]** en haut à droite.

>[!NOTE]
>
>Puisque les scores de propension sont écrits dans chaque profil individuel, ils sont disponibles dans le créateur de segments comme tout autre attribut de profil. Lorsque vous accédez au créateur de segments pour créer des segments, vous pouvez voir tous les scores de propension sous le Customer AI de votre espace de noms.

![Remplissage de segment](../images/insights/segment-saving.png)

Pour afficher le nouveau segment dans l’interface utilisateur de Platform, cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche. La page **[!UICONTROL Parcourir]** apparaît et affiche tous les segments disponibles.

![Tous vos segments](../images/insights/Segments-dashboard.png)

## Mesures de synthèse des performances {#performance-metrics}

L&#39;onglet **[!UICONTROL Résumé des performances]** affiche le ou les taux de conversion réels, séparés en chacun des intervalles de propension notés par l&#39;IA du client.

![Onglet Résumé des performances](../images/insights/summary_tab.png)

Au départ, seuls les taux prévus (lignes en pointillé) s’affichent. Les taux attendus s’affichent lorsqu’une série de notes n’a pas eu lieu et que les données ne sont pas encore disponibles. Cependant, une fois qu&#39;une fenêtre de résultats est passée, le taux attendu est remplacé par un taux réel (ligne solide).

Le survol des lignes affiche la date et le taux réel/attendu pour cette journée dans cette corbeille.

![Exemple de compartiment](../images/insights/churn_tab.png)

Vous pouvez filtrer la période pour les taux prévus et réels affichés. Sélectionnez l&#39;icône **calendrier** ![icône](../images/insights/calendar_icon.png)puis sélectionnez une nouvelle plage de dates. Les résultats de chacun des intervalles sont mis à jour pour s’afficher dans la nouvelle plage de dates.

![Sélecteur de date](../images/insights/date_selector.png)

### Taux d&#39;exécution de notation individuels

La moitié inférieure de l&#39;onglet **[!UICONTROL Résumé des performances]** affiche les résultats de chaque série de notes individuelle. Sélectionnez la date de liste déroulante dans l’angle supérieur droit pour afficher les résultats d’une autre série de scores.

Selon que vous prédites une génération ou une conversion, le graphique [!UICONTROL Répartition des scores] affiche la distribution des profils générés/convertis et non générés/non convertis à chaque incrément.

![score individuel](../images/insights/scoring_tab.png)

## Étapes suivantes

Ce document décrit les insights fournis par une instance de service Customer AI. Vous pouvez maintenant passer au tutoriel sur le [téléchargement de scores dans Customer AI](./download-scores.md) ou consulter les autres guides proposés sur [Adobe Intelligent Services](../../home.md).

## Ressources supplémentaires

La vidéo suivante explique comment utiliser l’IA du client pour visualiser la sortie des modèles et des facteurs influents.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
