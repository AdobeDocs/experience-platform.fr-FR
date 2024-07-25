---
keywords: Experience Platform;insights;service client;rubriques les plus consultées;informations sur les clients
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Découvrez les informations sur Customer AI
description: Ce document sert de guide pour interagir avec les informations d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 27%

---

# Découvrez des informations avec Customer AI

Customer AI fait partie d’Intelligent Services et permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper les prochaines actions de vos clients. Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème de machine learning, en choisissant un algorithme, une formation ou un déploiement.

Ce document sert de guide pour interagir avec les informations d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.

## Prise en main

Pour utiliser les informations relatives à Customer AI, vous devez avoir à disposition une instance de service dont l’état d’exécution est réussi. Pour créer une instance de service, rendez-vous sur [Configuration d’une instance Customer AI](./configure.md). Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

## Présentation de l’instance de service

Dans l’interface utilisateur de [!DNL Adobe Experience Platform], sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur *Services* apparaît et affiche les services intelligents disponibles. Dans le conteneur de Customer AI, sélectionnez **[!UICONTROL Ouvrir]**.

![Accès à votre instance](../images/insights/navigate-to-service.png)

La page de service de Customer AI s’affiche. Cette page répertorie les instances de service de Customer AI et affiche les informations les concernant, notamment le nom de l’instance, le type de propension, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour.

>[!NOTE]
>
>Seules les instances de service ayant réussi des exécutions de notation ont des insights.

![Création d’une instance](../images/insights/dashboard.png)

Sélectionnez un nom d’instance de service à commencer.

![Création d’une instance](../images/insights/click-the-name.png)

Ensuite, la page des insights de cette instance de service s’affiche avec l’option de sélectionner **[!UICONTROL Latest scores]** ou **[!UICONTROL Performance summary]**. L’onglet par défaut **[!UICONTROL Derniers scores]** fournit des visualisations de vos données. Les visualisations et ce que vous pouvez faire avec ces données sont expliqués plus en détail dans ce guide.

L’onglet **[!UICONTROL Synthèse des performances]** affiche les taux d’attrition ou de conversion réels pour chaque compartiment de propension. Pour en savoir plus, consultez la section sur les [mesures de résumé des performances](#performance-metrics).

![page de configuration](../images/insights/landing_page_insights.png)

## Détails des instances de service

Il existe deux manières d’afficher les détails de l’instance de service : depuis le tableau de bord ou au sein de l’instance de service.

### Tableau de bord des instances de service

Pour afficher un aperçu des détails de l’instance de service dans le tableau de bord, sélectionnez un conteneur d’instance de service, en évitant le lien hypertexte associé au nom. Cela ouvre un rail droit qui fournit des détails supplémentaires. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]** : la sélection de **[!UICONTROL Modifier]** vous permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence de notation de l’instance.
- **[!UICONTROL Clone]** : la sélection de **[!UICONTROL Clone]** copie la configuration de l’instance de service actuellement sélectionnée. Vous pouvez ensuite modifier le workflow pour effectuer des ajustements mineurs et le renommer en nouvelle instance.
- **[!UICONTROL Supprimer]** : vous pouvez supprimer une instance de service, y compris toutes les exécutions historiques.
- **[!UICONTROL Source de données]** : lien vers le jeu de données utilisé par cette instance.
- **[!UICONTROL Fréquence d’exécution]** : fréquence à laquelle une opération de notation a lieu et quand.
- **[!UICONTROL Définition de score]** : aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>En cas d’échec d’une opération de notation, un message d’erreur est fourni. Le message d’erreur est répertorié sous les **détails de la dernière exécution** dans le rail droit, qui est visible uniquement en cas d’exécutions ayant échoué.

![message d’échec d’exécution](../images/insights/failed-run.png)

### Afficher la liste déroulante d’informations supplémentaires

La deuxième façon d’afficher des détails supplémentaires sur une instance de service se trouve sur la page des informations. Sélectionnez **[!UICONTROL Afficher plus]** en haut à droite pour remplir une liste déroulante. Les détails sont répertoriés, tels que la définition du score, la date de création, le type de propension et les jeux de données utilisés. Pour plus d’informations sur l’une des propriétés répertoriées, consultez la page [Configuration d’une instance Customer AI](./configure.md).

![afficher plus](../images/insights/landing-show-more.png)

### Fenêtre contextuelle d’aperçu du jeu de données Customer AI

Si plusieurs jeux de données sont utilisés par Customer AI, un lien hypertexte intitulé **[!UICONTROL Multiple]** suivi du nombre de jeux de données entre crochets `()` est fourni.

![plusieurs jeux de données](../images/insights/insights-multi-datasets.png)

La sélection du lien de plusieurs jeux de données ouvre la fenêtre contextuelle d’aperçu des jeux de données Customer AI. Chaque couleur de l’aperçu représente un jeu de données tel qu’affiché par la clé de couleur située à gauche des colonnes du jeu de données. Dans cet exemple, vous pouvez constater que seul le **jeu de données 1** contient la colonne `PROP1`.

![afficher plus](../images/insights/dataset-preview.png)

### Modification d’une instance

Pour modifier une instance, sélectionnez **[!UICONTROL Edit]** dans le volet de navigation supérieur droit.

![cliquez sur le bouton Modifier](../images/insights/edit-button.png)

La boîte de dialogue de modification s’affiche, vous permettant de modifier le nom, la description, l’état et la fréquence de notation de l’instance. Pour confirmer vos modifications et fermer la boîte de dialogue, sélectionnez **[!UICONTROL Enregistrer]** dans le coin inférieur droit.

![modifier la fenêtre contextuelle](../images/insights/edit-instance.png)

### Actions supplémentaires

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. Sélectionner **[!UICONTROL Autres actions]** ouvre une liste déroulante qui vous permet de sélectionner l’une des opérations suivantes :

- **[!UICONTROL Clone]** : si vous sélectionnez **[!UICONTROL Clone]**, l’instance de service configurée est copiée. Vous pouvez ensuite modifier le workflow pour effectuer des ajustements mineurs et le renommer en nouvelle instance.
- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Accéder aux scores]** : si vous sélectionnez **[!UICONTROL Accéder aux scores]**, une boîte de dialogue s’ouvre. Elle contient un lien vers le tutoriel [ sur le téléchargement des scores pour Customer AI](./download-scores.md). La boîte de dialogue fournit également l’identifiant du jeu de données requis pour effectuer des appels API.
- **[!UICONTROL Afficher l’historique d’exécution]** : fait apparaître une boîte de dialogue contenant une liste des exécutions de notation associées à l’instance de service.

![actions supplémentaires](../images/insights/more-actions.png)

## Résumé des scores {#scoring-summary}

Le résumé de notation affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible. Les compartiments de propension sont déterminés en fonction de la plage de scores : la propension faible est inférieure à 24, la propension moyenne est comprise entre 25 et 74, et la propension élevée est supérieure à 74. Chaque compartiment a une couleur en fonction de la légende.

>[!NOTE]
>
>S’il s’agit d’un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

![résumé de notation](../images/insights/scoring-summary.png)

Vous pouvez survoler n’importe quelle couleur de l’anneau pour afficher des informations supplémentaires, telles qu’un pourcentage et le nombre total de profils appartenant à un compartiment.

![](../images/insights/scoring-ring.png)

## Distribution des scores

La carte **[!UICONTROL Distribution des scores]** vous donne un résumé visuel de la population en fonction du score. Les couleurs que vous voyez dans la carte [!UICONTROL Distribution des scores] représentent le type de score de propension généré. Passez la souris sur l’une des distributions de notation pour obtenir le nombre exact appartenant à cette distribution.

![distribution des scores](../images/insights/distribution-of-scores.png)

## Facteurs d’influence

Une carte est générée pour chaque compartiment de score, présentant les 10 principaux facteurs d’influence pour ce compartiment. Les facteurs d’influence vous donnent des détails supplémentaires sur la raison pour laquelle vos clients appartiennent à différents compartiments de score.

![facteurs d’influence](../images/insights/influential-factors.png)

### Effondrement des facteurs d’influence

Le survol de l’un des principaux facteurs d’influence ventile les données. Vous obtenez une vue d’ensemble des raisons pour lesquelles certains profils appartiennent à un compartiment de propension. Selon le facteur, vous pouvez recevoir des valeurs numériques, catégoriques ou booléennes. L’exemple ci-dessous affiche des valeurs catégoriques par région.

![capture d’écran de drilldown](../images/insights/drilldown.png)

En outre, en utilisant des analyses par analyse, vous pouvez comparer un facteur de distribution s’il se produit dans plusieurs compartiments de propension et créer des segments plus spécifiques avec ces valeurs. L’exemple suivant illustre le premier cas d’utilisation :

![](../images/insights/drilldown-compare.png)

Vous pouvez constater que les profils présentant une faible propension à la conversion ont moins de chance d’avoir effectué une visite récente sur les pages web adobe.com . Le facteur &quot;Jours depuis la dernière visite web&quot; n’a qu’une couverture de 8 % par rapport à 26 % dans les profils de propension moyens. En utilisant ces chiffres, vous pouvez comparer la distribution dans chaque intervalle pour le facteur. Ces informations peuvent être utilisées pour déduire que la récence des visites web n’a pas autant d’influence dans le compartiment à faible propension que dans le compartiment à propension moyenne.

### Création d’un segment

Si vous sélectionnez le bouton **[!UICONTROL Créer un segment]** dans l’un des compartiments de propension faible, moyenne et élevée, vous redirigez vers le créateur de segments.

>[!NOTE]
>
>Le bouton **[!UICONTROL Créer un segment]** n’est disponible que si Real-Time Customer Profile est activé pour le jeu de données. Pour plus d’informations sur l’activation de Real-Time Customer Profile, consultez la [présentation de Real-Time Customer Profile](../../../rtcdp/overview.md).

![Cliquez sur Créer un segment](../images/insights/influential-factors-create-segment.png)

![Création d’un segment](../images/insights/create-segment.png)

Le créateur de segments permet de définir un segment. Lorsque vous sélectionnez **[!UICONTROL Créer un segment]** sur la page Statistiques, Customer AI ajoute automatiquement les informations des compartiments sélectionnés au segment. Pour terminer la création de votre segment, il vous suffit de renseigner les conteneurs **Nom** et **Description** situés dans le rail droit de l’interface utilisateur du créateur de segments. Après avoir donné un nom et une description au segment, sélectionnez **[!UICONTROL Enregistrer]** en haut à droite.

>[!NOTE]
>
>Puisque les scores de propension sont écrits dans le profil individuel, ils sont disponibles dans le créateur de segments comme tout autre attribut de profil. Lorsque vous accédez au créateur de segments pour créer des segments, vous pouvez voir tous les scores de propension sous le Customer AI de votre espace de noms.

![Remplissage de segment](../images/insights/segment-saving.png)

Pour afficher votre nouveau segment dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Segments]** dans le volet de navigation de gauche. La page **[!UICONTROL Parcourir]** apparaît et affiche tous les segments disponibles.

![Tous vos segments](../images/insights/Segments-dashboard.png)

## Performance historique {#historical-performance}

L’onglet **[!UICONTROL Synthèse des performances]** affiche les taux d’attrition ou de conversion réels, séparés dans chacun des compartiments de propension notés par Customer AI.

![Onglet Synthèse des performances](../images/insights/summary_tab.png)

Au départ, seuls les taux prévus (lignes en pointillés) s’affichent. Les taux attendus s’affichent lorsqu’aucune opération de notation n’a eu lieu et que les données ne sont pas encore disponibles. Cependant, une fois qu’une fenêtre de résultat est passée, le taux attendu est remplacé par un taux réel (ligne continue).

Le survol des lignes avec le curseur affiche la date et le taux réel/attendu pour cette journée dans ce compartiment.

![Exemple de compartiment](../images/insights/churn_tab.png)

Vous pouvez filtrer la période pour les taux prévus et réels affichés. Sélectionnez l&#39;**icône de calendrier** ![icône](/help/images/icons/calendar.png) , puis sélectionnez une nouvelle plage de dates. Les résultats de chacun des compartiments sont mis à jour pour s’afficher dans la nouvelle période.

![Sélecteur de date](../images/insights/date_selector.png)

### Taux d’exécution de notation individuels

La moitié inférieure de l’onglet **[!UICONTROL Résumé des performances]** affiche les résultats de chaque opération de notation individuelle. Sélectionnez la date de liste déroulante en haut à droite pour afficher les résultats d’une autre opération de notation.

Selon que vous prédites une perte ou une conversion, le graphique [!UICONTROL Distribution des scores] affiche la distribution des profils générés/convertis et non pas générés/non convertis dans chaque incrément.

![notation individuelle](../images/insights/scoring_tab.png)

## Évaluation de modèles {#model-evaluation}

Outre le suivi des résultats prévus et réels au fil du temps sur l’onglet Performances historiques , les marketeurs disposent d’encore plus de transparence sur la qualité du modèle dans l’onglet Évaluation du modèle . Vous pouvez utiliser les graphiques Effet élévateur et Gains pour déterminer les différences d’utilisation d’un modèle prédictif par rapport au ciblage aléatoire. De plus, vous pouvez déterminer le nombre de résultats positifs capturés à chaque exclusion de score. Cela s’avère utile pour la segmentation et l’alignement du retour sur investissement avec les actions marketing.

### Graphique de l’effet élévateur

![graphique d’effet élévateur](../images/user-guide/lift-chart.png)

Le graphique de l’effet élévateur mesure l’amélioration de l’utilisation d’un modèle prédictif au lieu du ciblage aléatoire.

Les indicateurs de modèle de haute qualité incluent :

- Valeurs d’effet élévateur élevées dans les premiers déciles. Cela signifie que le modèle est doué pour identifier les utilisateurs ayant la plus forte propension à prendre des mesures d’intérêt.
- Valeurs de l’effet élévateur descendant. Cela signifie que les clients ayant des scores plus élevés sont plus susceptibles d’effectuer une action d’intérêt que les personnes ayant des scores plus faibles.

### Graphique des gains

![graphique des gains](../images/user-guide/gains-chart.png)

Le graphique des gains cumulés mesure le pourcentage de résultats positifs capturés par les scores de ciblage supérieurs à un certain seuil. Après avoir trié les clients par score de propension de haut en bas, la population est divisée en déciles : 10 groupes de taille égale. Un modèle parfait capturerait tous les résultats positifs dans les déciles à score le plus élevé. Une méthode de ciblage aléatoire de base capture les résultats positifs proportionnellement à la taille du groupe : le ciblage de 30 % des utilisateurs capturerait 30 % des résultats.

Les indicateurs de modèle de haute qualité incluent :

- Les gains cumulés approchent rapidement les 100 %.
- La courbe des gains cumulés du modèle est plus proche du coin supérieur gauche du graphique.
- Le graphique des gains cumulés peut être utilisé pour déterminer les limites de score pour la segmentation et le ciblage. Par exemple, si le modèle capture 70 % des résultats positifs dans les 2 premiers déciles de score, le ciblage des utilisateurs ayant PercentileScore > 80 devrait capturer environ 70 % des résultats positifs.

### AUC (surface sous la courbe)

L’AUC reflète la force de la relation entre le classement par score et l’occurrence de l’objectif prévu. Un **AUC** de 0.5 signifie que le modèle n’est pas meilleur qu’une estimation aléatoire. Un **AUC** de 1 signifie que le modèle peut parfaitement prédire qui prendra l’action appropriée.

## Étapes suivantes

Ce document décrit les informations fournies par une instance de service Customer AI. Vous pouvez maintenant passer au tutoriel sur le [téléchargement de scores dans Customer AI](./download-scores.md) ou consulter les autres guides proposés sur [Adobe Intelligent Services](../../home.md).

## Ressources supplémentaires

La vidéo suivante explique comment utiliser Customer AI pour afficher la sortie des modèles et des facteurs d’influence.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
