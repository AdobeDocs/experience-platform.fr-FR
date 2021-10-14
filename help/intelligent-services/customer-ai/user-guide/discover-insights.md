---
keywords: Experience Platform;insights;service client;rubriques les plus consultées;informations sur les clients
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Découvrez les informations sur Customer AI
topic-legacy: Discovering insights
description: Ce document sert de guide pour interagir avec les insights d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 45%

---

# Découvrez des informations avec Customer AI

Customer AI fait partie d’Intelligent Services et permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper les prochaines actions de vos clients. Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.

Ce document sert de guide pour interagir avec les insights d’instance de service dans l’interface utilisateur d’Intelligent Services Customer AI.

## Prise en main

Pour utiliser les insights relatifs à Customer AI, vous devez avoir à disposition une instance de service dont l’état d’exécution est réussi. Pour créer une instance de service, rendez-vous sur [Configuration d’une instance Customer AI](./configure.md). Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

## Présentation de l’instance de service

Dans l’interface utilisateur [!DNL Adobe Experience Platform], cliquez sur **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur *Services* apparaît et affiche les services intelligents disponibles. Dans le conteneur de Customer AI, cliquez sur **[!UICONTROL Ouvrir]**.

![Accès à votre instance](../images/insights/navigate-to-service.png)

La page de service de Customer AI s’affiche. Cette page répertorie les instances de service de Customer AI et affiche les informations les concernant, notamment le nom de l’instance, le type de propension, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour.

>[!NOTE]
>
>Seules les instances de service ayant réussi des exécutions de notation ont des insights.

![Création d’une instance](../images/insights/dashboard.png)

Sélectionnez un nom d’instance de service à commencer.

![Création d’une instance](../images/insights/click-the-name.png)

Ensuite, la page d’informations de cette instance de service s’affiche avec l’option permettant de sélectionner **[!UICONTROL Derniers scores]** ou **[!UICONTROL Synthèse des performances]**. L’onglet par défaut **[!UICONTROL Derniers scores]** fournit des visualisations de vos données. Les visualisations et ce que vous pouvez faire avec ces données sont expliqués plus en détail dans ce guide.

L’onglet **[!UICONTROL Résumé des performances]** indique les taux de perte ou de conversion réels pour chaque intervalle de propension. Pour en savoir plus, consultez la section sur les [mesures de résumé des performances](#performance-metrics).

![page de configuration](../images/insights/landing_page_insights.png)

### Détails des instances de service

Il existe deux façons d’afficher les détails de l’instance de service : depuis le tableau de bord ou au sein de l’instance de service.

Pour afficher un aperçu des détails de l’instance de service dans le tableau de bord, sélectionnez un conteneur d’instance de service, en évitant le lien hypertexte associé au nom. Cela ouvre un rail droit qui fournit des détails supplémentaires. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]** : Sélectionnez  **** Editer pour modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence de notation de l’instance.
- **[!UICONTROL Cloner]** : Sélectionnez  **** Clonecopies pour la configuration de l’instance de service actuellement sélectionnée. Vous pouvez ensuite modifier le workflow pour effectuer des ajustements mineurs et le renommer en nouvelle instance.
- **[!UICONTROL Supprimer]** : Vous pouvez supprimer une instance de service, y compris les exécutions historiques.
- **[!UICONTROL Source]** de données : Un lien vers le jeu de données utilisé par cette instance.
- **[!UICONTROL Fréquence d’exécution]** : La fréquence d’une opération de notation et le moment auquel elle a lieu.
- **[!UICONTROL Définition de score]** : Aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>En cas d’échec d’une exécution de notation, vous recevez un message d’erreur. Le message d’erreur est répertorié sous les **détails de la dernière exécution** dans le rail droit, qui est visible uniquement en cas d’exécutions ayant échoué.

![message d’échec d’exécution](../images/insights/failed-run.png)

La deuxième façon d’afficher des détails supplémentaires sur une instance de service se trouve sur la page des insights. Vous pouvez cliquer sur **[!UICONTROL Afficher plus]** en haut à droite pour remplir une liste déroulante. Les détails y sont répertoriés, tels que la définition du score, la date de création et le type de propension. Pour plus d’informations sur l’une des propriétés répertoriées, consultez la section [Configuration d’une instance Customer AI](./configure.md).

![afficher plus](../images/insights/landing-show-more.png)

![afficher plus](../images/insights/show-more.png)

### Modification d’une instance

Pour modifier une instance, cliquez sur **[!UICONTROL Modifier]** dans la navigation en haut à droite.

![cliquez sur le bouton Modifier](../images/insights/edit-button.png)

La boîte de dialogue de modification s’affiche, vous permettant de modifier le nom, la description, l’état et la fréquence de notation de l’instance. Pour confirmer vos modifications et fermer la boîte de dialogue, sélectionnez **[!UICONTROL Enregistrer]** dans le coin inférieur droit.

![modifier la fenêtre contextuelle](../images/insights/edit-instance.png)

### Actions supplémentaires

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. Cliquer sur **[!UICONTROL Actions supplémentaires]** ouvre un menu déroulant qui vous permet de sélection l’une des opérations suivantes :

- **[!UICONTROL Cloner]** : Sélectionnez  **** Clonecopies pour la configuration de l’instance de service. Vous pouvez ensuite modifier le workflow pour effectuer des ajustements mineurs et le renommer en nouvelle instance.
- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Accéder aux scores]** : Sélectionnez  **[!UICONTROL Accéder aux]** scores , puis ouvrez une boîte de dialogue contenant un lien vers le tutoriel  [Téléchargement des scores pour Customer ](./download-scores.md) AI. La boîte de dialogue fournit également l’identifiant du jeu de données requis pour effectuer des appels API.
- **[!UICONTROL Afficher l’historique d’exécution]** : fait apparaître une boîte de dialogue contenant une liste des exécutions de notation associées à l’instance de service.

![actions supplémentaires](../images/insights/more-actions.png)

## Résumé de notation {#scoring-summary}

Le résumé de notation affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible. Les compartiments de propension sont déterminés en fonction de la plage de scores : la propension faible est inférieure à 24, la propension moyenne est comprise entre 25 et 74, et la propension élevée est supérieure à 74. Chaque compartiment a une couleur en fonction de la légende.

>[!NOTE]
>
>S’il s’agit d’un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

![résumé de notation](../images/insights/scoring-summary.png)

Vous pouvez survoler n’importe quelle couleur de l’anneau pour afficher des informations supplémentaires, telles qu’un pourcentage et le nombre total de profils appartenant à un compartiment.

![](../images/insights/scoring-ring.png)

## Distribution des scores

La carte **[!UICONTROL Distribution des scores]** vous donne un résumé visuel de la population en fonction du score. Les couleurs présentes sur la carte [!UICONTROL Distribution des scores] représentent le type de score de propension généré. Passez la souris sur l’une des distributions de notation pour obtenir le nombre exact appartenant à cette distribution.

![distribution des scores](../images/insights/distribution-of-scores.png)

## Facteurs d’influence

Une carte est générée pour chaque compartiment de score, présentant les 10 principaux facteurs d’influence pour ce compartiment. Les facteurs d’influence vous donnent des détails supplémentaires sur la raison pour laquelle vos clients appartiennent à différents compartiments de score.

![facteurs d’influence](../images/insights/influential-factors.png)

### Effondrement des facteurs d’influence

Le survol de l’un des principaux facteurs d’influence ventile les données. Vous obtenez un aperçu des raisons pour lesquelles certains profils appartiennent à un compartiment de propension. Selon le facteur, vous pouvez recevoir des valeurs numériques, catégoriques ou booléennes. L’exemple ci-dessous affiche des valeurs catégoriques par région.

![capture d’écran de drilldown](../images/insights/drilldown.png)

En outre, en utilisant des analyses par analyse, vous pouvez comparer un facteur de distribution s’il se produit dans plusieurs compartiments de propension et créer des segments plus spécifiques avec ces valeurs. L’exemple suivant illustre le premier cas d’utilisation :

![](../images/insights/drilldown-compare.png)

Vous pouvez constater que les profils présentant une faible propension à la conversion ont moins de chance d’avoir effectué une visite récente sur les pages web adobe.com. Le facteur &quot;Jours depuis la dernière visite web&quot; n’a qu’une couverture de 8 % par rapport à 26 % dans les profils de propension moyens. En utilisant ces chiffres, vous pouvez comparer la distribution dans chaque intervalle pour le facteur. Ces informations peuvent être utilisées pour déduire que la récence des visites web n’a pas autant d’influence dans le compartiment à faible propension que dans le compartiment à propension moyenne.

### Création d’un segment

Si vous sélectionnez le bouton **[!UICONTROL Créer un segment]** dans l’un des compartiments de propension faible, moyenne et élevée, vous redirigez vers le créateur de segments.

>[!NOTE]
>
>Le bouton **[!UICONTROL Créer un segment]** n’est disponible que si Real-time Customer Profile est activé pour le jeu de données. Pour plus d’informations sur l’activation de Real-time Customer Profile, consultez la [présentation de Real-time Customer Profile](../../../rtcdp/overview.md).

![Cliquez sur Créer un segment](../images/insights/influential-factors-create-segment.png)

![Création d’un segment](../images/insights/create-segment.png)

Le créateur de segments permet de définir un segment. Lorsque vous sélectionnez **[!UICONTROL Créer un segment]** dans la page Informations, Customer AI ajoute automatiquement les informations des compartiments sélectionnés au segment. Pour terminer la création de votre segment, il vous suffit de renseigner les conteneurs *Nom* et *Description* situés dans le rail droit de l’interface utilisateur du créateur de segments. Après avoir donné un nom et une description au segment, cliquez sur **[!UICONTROL Enregistrer]** en haut à droite.

>[!NOTE]
>
>Puisque les scores de propension sont écrits dans chaque profil individuel, ils sont disponibles dans le créateur de segments comme tout autre attribut de profil. Lorsque vous accédez au créateur de segments pour créer des segments, vous pouvez voir tous les scores de propension sous le Customer AI de votre espace de noms.

![Remplissage de segment](../images/insights/segment-saving.png)

Pour afficher le nouveau segment dans l’interface utilisateur de Platform, cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche. La page **[!UICONTROL Parcourir]** apparaît et affiche tous les segments disponibles.

![Tous vos segments](../images/insights/Segments-dashboard.png)

## Mesures de synthèse des performances {#performance-metrics}

L’onglet **[!UICONTROL Résumé des performances]** affiche les taux de perte ou de conversion réels, séparés dans chacun des compartiments de propension notés par Customer AI.

![Onglet Synthèse des performances](../images/insights/summary_tab.png)

Au départ, seuls les taux prévus (lignes en pointillés) s’affichent. Les taux attendus s’affichent lorsqu’aucune opération de notation n’a eu lieu et que les données ne sont pas encore disponibles. Cependant, une fois qu’une fenêtre de résultat est passée, le taux attendu est remplacé par un taux réel (ligne continue).

Le survol des lignes avec le curseur affiche la date et le taux réel/attendu pour cette journée dans ce compartiment.

![Exemple de compartiment](../images/insights/churn_tab.png)

Vous pouvez filtrer la période pour les taux prévus et réels affichés. Sélectionnez l’**icône de calendrier** ![icône](../images/insights/calendar_icon.png)puis sélectionnez une nouvelle plage de dates. Les résultats de chacun des compartiments sont mis à jour pour s’afficher dans la nouvelle période.

![Sélecteur de date](../images/insights/date_selector.png)

### Taux d’exécution de notation individuels

La moitié inférieure de l’onglet **[!UICONTROL Résumé des performances]** affiche les résultats de chaque opération de notation. Sélectionnez la date de liste déroulante en haut à droite pour afficher les résultats d’une autre opération de notation.

Selon que vous prédites une perte ou une conversion, le graphique [!UICONTROL Distribution des scores] affiche la distribution des profils générés/convertis et non pas générés/non convertis à chaque incrément.

![notation individuelle](../images/insights/scoring_tab.png)

## Étapes suivantes

Ce document décrit les insights fournis par une instance de service Customer AI. Vous pouvez maintenant passer au tutoriel sur le [téléchargement de scores dans Customer AI](./download-scores.md) ou consulter les autres guides proposés sur [Adobe Intelligent Services](../../home.md).

## Ressources supplémentaires

La vidéo suivante explique comment utiliser Customer AI pour afficher la sortie des modèles et des facteurs d’influence.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
