---
keywords: Experience Platform;profil;segment;segments;segmentation;interface utilisateur;interface utilisateur;personnalisation;tableau de bord des segments;tableau de bord
title: Guide du tableau de bord des segments
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les segments créés par votre organisation.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 98%

---

# Tableau de bord des [!UICONTROL segments] {#segment-dashboard}

L’interface utilisateur d’Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos segments. Ceux-ci sont présentés tels qu’ils sont capturés lors d’un instantané quotidien. Ce guide explique comment accéder et travailler avec le tableau de bord des segments dans l’interface utilisateur et fournit plus d’informations sur les visualisations affichées dans le tableau de bord.

Pour obtenir un aperçu de toutes les fonctionnalités du service de segmentation d’Adobe Experience Platform au sein de l’interface utilisateur de la plateforme, veuillez consulter le [Guide de l’interface utilisateur du service de segmentation](../../segmentation/ui/overview.md).

## Données du tableau de bord [!UICONTROL Segments]

Le tableau de bord des segments affiche un instantané des données d’attributs (enregistrements) dont votre organisation dispose dans le magasin de profils d’Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord de segments n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorez le tableau de bord [!UICONTROL Segments] {#explore}

Pour naviguer vers le tableau de bord [!UICONTROL Segments] dans l’interface utilisateur de la plateforme, sélectionnez **[!UICONTROL Segments]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre organisation débute sur Platform et n’a pas encore de jeux de données de profils actifs ou de politiques de fusion créés, le tableau de bord [!UICONTROL Segments] n’est pas visible. Au lieu de cela, l’onglet [!UICONTROL Présentation] affiche des liens et de la documentation pour vous aider à démarrer avec la segmentation.

![Onglet Aperçu du tableau de bord Segments avec les options Segments et Aperçu en surbrillance.](../images/segments/dashboard-overview.png)

### Modifiez le tableau de bord [!UICONTROL Segments] {#modify}

Vous pouvez modifier l’aspect du tableau de bord [!UICONTROL Segments] en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord ainsi que d’accéder à la **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la section [Modification des tableaux de bord](../customize/modify.md) et [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

### Ajouter des widgets {#add-widget}

Sélectionnez **[!UICONTROL Ajouter un widget]** pour accéder à la bibliothèque de widgets et voir la liste des widgets disponibles à ajouter à votre tableau de bord.

![La présentation du tableau de bord Segments avec le widget Ajouter mis en surbrillance.](../images/segments/segments-overview-add-widget.png)

Dans la bibliothèque de widgets, vous pouvez parcourir la sélection de widgets de segments standard et personnalisés. Pour des informations sur la façon d’ajouter des widgets, veuillez consulter la documentation de la bibliothèque de widgets sur la façon [d’ajouter un widget](../customize/widget-library.md#add-widgets).

## Sélectionnez un segment

Le tableau de bord sélectionne automatiquement un segment à afficher, mais vous pouvez changer le segment en utilisant le menu déroulant ou le sélecteur de segment.

Pour choisir un autre segment, sélectionnez la liste déroulante à côté du nom du segment ou utilisez le sélecteur de segment pour ouvrir la boîte de dialogue de sélection de segment.

>[!IMPORTANT]
>
>Seuls les segments dont le nombre de profils est supérieur à zéro sont affichés dans la liste des segments sélectionnables.

![La présentation du tableau de bord des segments avec le menu déroulant du segment global en surbrillance.](../images/segments/change-segment.png)

![La boîte de dialogue Sélectionner un segment qui affiche tous les segments disponibles.](../images/segments/select-segment-dialog.png)

## Widgets et mesures

Le tableau de bord des segments est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes concernant le segment sélectionné.

La date et l’heure de l’instantané le plus récent sont affichées en haut de l’onglet [!UICONTROL Présentation] à côté de la liste déroulante des segments. Toutes les données du widget sont exactes à cette date et cette heure. La date et l’heure de l’instantané sont fournies en UTC ; elles ne se trouvent pas dans le fuseau horaire de l’utilisateur/utilisatrice ou de l’organisation.

![L’onglet Présentation des segments avec une date et heure du widget mis en surbrillance.](../images/segments/widget-timestamp.png)

## Widgets standard {#standard-widgets}

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos segments. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation en utilisant la [!UICONTROL bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire la [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

Pour en savoir plus sur chacun des widgets standards disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Taille de l’audience]](#audience-size)
* [[!UICONTROL Ordre d’activation de l’audience]](#audience-activation-order)
* [[!UICONTROL Tendance de la taille de l’audience]](#audience-size-trend)
* [[!UICONTROL Tendance de changement de la taille de l’audience]](#audience-size-change-trend)
* [[!UICONTROL Tendance de la taille de l’audience par identité]](#audience-size-trend-by-identity)
* [[!UICONTROL Chevauchements d’audience]](#audience-overlap)
* [[!UICONTROL Rapport de chevauchements d’audience]](#audience-overlap-report)
* [[!UICONTROL Chevauchement des identités]](#identity-overlap)
* [[!UICONTROL Profils par identité]](#profiles-by-identity)
* [[!UICONTROL Activations planifiées]](#scheduled-activations)

### [!UICONTROL Taille de l’audience] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Taille de l’audience"
>abstract="Ce widget affiche le nombre total de profils fusionnés dans le segment sélectionné. Ce nombre dépend de la politique de fusion appliquée à vos données et est correct au moment de l’instantané le plus récent."

Le widget **[!UICONTROL Taille de l’audience]** affiche le nombre total de profils fusionnés dans le segment sélectionné au moment de la prise de l’instantané. Ce nombre est le résultat de l’application de la politique de fusion de segments à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu du segment.

Pour plus d&#39;informations sur les fragments et les profils fusionnés, reportez-vous à la section [Présentation de Real-Time Customer Profile](../../profile/home.md).

![Présentation du tableau de bord Segments avec le widget Taille de l’audience en surbrillance.](../images/segments/audience-size.png)

### [!UICONTROL Tendance de la taille de l’audience] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendance de la taille de l’audience"
>abstract="Ce widget fournit des informations sur le nombre total de profils qui répondent aux critères de **toute** définition de segment, telle qu’elle est capturée lors de l’instantané quotidien, pendant les derniers 30 jours, 90 jours ou 12 mois."

Le widget **[!UICONTROL Tendance de la taille d’audience]** fournit une représentation graphique linéaire pour le nombre total de profils qui répondent aux critères de **toute** définition de segment sur une période donnée. La tendance de la taille d’audience peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. La taille de l’audience est représentée sur l’axe y et le temps est représenté sur l’axe x.

Ce widget inclut également la fonctionalité automatique [!UICONTROL Légendes] dans laquelle un modèle de machine learning analyse le graphique et les données de segment et génère automatiquement des légendes pour décrire les tendances clés et les événements importants. Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatique.

![La présentation des segments affiche le widget Tendance de la taille d’audience.](../images/segments/audience-size-trend-captions.png)

La boîte de dialogue de légendes automatique s’ouvre, vous permettant d’obtenir des informations sur vos données.

![La boîte de dialogue de légendes automatique pour le widget Tendance de la taille d’audience.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Pour en savoir plus sur l’évaluation des segments et sur la manière dont les profils sont qualifiés et quittent des segments, reportez-vous à la section [Documentation de Segmentation Service](../../segmentation/home.md).

### [!UICONTROL Tendance de changement de la taille de l’audience] {#audience-size-change-trend}

Ce widget fournit un graphique linéaire qui illustre la différence entre le nombre total de profils qualifiés pour un segment donné et les derniers instantanés quotidiens. Le segment choisi pour analyse est sélectionné dans le menu déroulant de la présentation. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. La taille de l’audience est représentée sur l’axe y et le temps est représenté sur l’axe x.

![Le widget pour la tendance du changement de la taille d’audience.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Tendance de la taille de l’audience par identité] {#audience-size-trend-by-identity}

Ce widget représente la tendance de taille d’audience d’un segment particulier en fonction du type d’identité choisi dans le menu déroulant du widget. Le segment utilisé pour l’analyse est sélectionné dans le menu déroulant de la présentation. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget.

![Widget pour la tendance de la taille des audiences par identité.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Ordre d’activation de l’audience] {#audience-activation-order}

Le widget [!UICONTROL Ordre d’activation de l’audience] génère un tableau à trois colonnes qui répertorie le [!UICONTROL nom de la destination], la [!UICONTROL plateforme] et la [!UICONTROL date] d’activation de l’audience. La liste est classée en fonction de la date en commençant par la plus récente et peut contenir jusqu’à 10 lignes.

![Le widget Ordre d’activation de l’audience.](../images/segments/audience-activation-order.png)

### [!UICONTROL Chevauchement des audiences] {#audience-overlap}

Ce widget représente le nombre de profils de deux segments qui répondent aux critères de définition des deux segments. Les segments utilisés pour la comparaison sont sélectionnés dans les menus déroulants du widget. Le nombre total de profils contenus dans la définition de segment correspondante peut être affiché en passant la souris sur un cercle ou sur l’intersection du diagramme de Venn.

Ce widget vous permet d’optimiser la stratégie de segmentation en consultant les similitudes dans les résultats de vos définitions de segment.

![Le widget de chevauchement des audiences.](../images/segments/audience-overlap.png)

### [!UICONTROL Rapport de chevauchement des audiences] {#audience-overlap-report}

Ce widget met les données de chevauchement d’audience pour un segment spécifique au format tabulaire. Une liste de cinq audiences classées par pourcentage de chevauchement en commençant par le plus élevé est fournie pour le segment sélectionné dans le menu déroulant en haut de l’écran. Pour plus de clarté, le segment sélectionné est répertorié dans la colonne [!UICONTROL NOM DU SEGMENT A]. L’analyse du chevauchement des audiences est fournie pour le deuxième segment répertorié dans la colonne [!UICONTROL NOM DU SEGMENT B]. Le chevauchement en pourcentage est fourni dans la troisième colonne avec une précision de douze décimales.

Le rapport sur le chevauchement des audiences vous permet de créer de nouveaux segments hautement performants. L’observation des chevauchements au pourcentage élevé vous permet de supprimer des audiences et d’empêcher l’envoi d’une même audience vers différentes destinations. Elle vous aide également à identifier les informations cachées qui peuvent contribuer à une meilleure segmentation. Un chevauchement au pourcentage faible permet de localiser les profils uniques à rechercher.

Sélectionnez **[!UICONTROL En savoir plus]** pour ouvrir une boîte de dialogue plein écran contenant davantage de données de chevauchement de segments.

![Le widget de Rapport de chevauchements d’audience avec l’option En savoir plus en surbrillance.](../images/segments/audience-overlap-report.png)

La boîte de dialogue [!UICONTROL Rapport de chevauchement des audiences] s’affiche. Cette boîte de dialogue peut contenir jusqu’à 50 lignes d’analyses de chevauchement des audiences, divisées en six colonnes. Sélectionnez l’icône des paramètres (![Icône des paramètres.](../images/segments/settings-icon.png)) pour supprimer ou ajouter des colonnes du tableau.

![Boîte de dialogue Rapport de chevauchement des audiences.](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Sélectionnez l’en-tête de colonne **[!UICONTROL Chevauchement]** pour modifier le classement des résultats, du plus haut au plus bas ou du plus bas au plus haut.

Pour télécharger l’intégralité du rapport au format PDF, sélectionnez le menu d’options (**`...`**), puis **[!UICONTROL Télécharger]**.

![La boîte de dialogue Rapport de chevauchement des audiences avec les points de suspension et l’option de téléchargement en surbrillance.](../images/segments/segments-audience-overlap-report-dialog-download.png)

Sélectionnez une ligne dans le rapport pour ouvrir un diagramme de Venn de l’analyse de chevauchement. Passez la souris sur une section du diagramme de Venn pour afficher le nombre de profils dans une boîte de dialogue.

![La boîte de dialogue Rapport de chevauchement d’audience avec un diagramme de Venn et une ligne en surbrillance.](../images/segments/audience-overlap-report-dialog-venn.png)

Sélectionnez **[!UICONTROL Fermer]** pour revenir au tableau de bord [!UICONTROL Segments].

### [!UICONTROL Chevauchement des identités] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Chevauchement des identités"
>abstract="Ce widget affiche le chevauchement des profils de votre segment contenant les deux identités sélectionnées. Les cercles affichent la taille relative de chaque identité. Le nombre de profils contenant les deux espaces de noms est représenté par le chevauchement entre les cercles."

Le widget **[!UICONTROL Chevauchement des identités]** affiche un diagramme de Venn, ou diagramme logique, qui montre le chevauchement des profils de votre segment contenant plusieurs identités.

Utilisez les menus déroulants du widget pour sélectionner les identités à comparer. Les cercles affichent la taille relative de chaque identité choisie, le nombre de profils contenant les deux espaces de noms étant représenté par la taille du chevauchement entre les cercles.

Si un(e) client(e) interagit avec votre marque sur plusieurs canaux, plusieurs identités seront associées à ce(tte) client(e) individuel(le). Par conséquent, il est probable que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour en savoir plus sur les identités, rendez-vous sur la page de [documentation d’Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Présentation du tableau de bord Segments avec le widget Chevauchement des identités en surbrillance.](../images/segments/identity-overlap.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profils par identité"
>abstract="Ce widget affiche la répartition des identités pour chaque profil fusionné du segment sélectionné."

Le widget **[!UICONTROL Profils par identité]** affiche la répartition des identités pour chaque profil fusionné du segment sélectionné. Le nombre total de profils par identité peut être supérieur au nombre total de profils dans le segment, car plusieurs identités peuvent être associées à un même profil. En d’autres termes, le fait de cumuler les valeurs affichées pour chaque identité peut donner un total supérieur à la taille totale de l’audience dans le segment, car si un(e) client(e) interagit avec votre marque sur plusieurs canaux, plusieurs identités peuvent être associées à ce(tte) client(e) individuel(lle).

Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue automatique des légendes.

![La présentation du tableau de bord Segments avec le widget Profils par identité et l’option Sous-titres en surbrillance.](../images/segments/profiles-by-identity.png)

Un modèle de machine learning génère automatiquement des informations sur les données en analysant la distribution globale et les dimensions clés des données.

Pour en savoir plus sur les identités, rendez-vous sur la page de la [documentation d’Adobe Experience Platform Identity Service](../../identity-service/home.md).

### Activations planifiées {#scheduled-activations}

Le widget d’[!UICONTROL activations planifiées] offre une vue tabulée des destinations activées le plus récemment. Le tableau comprend la plateforme de destination, le nom de votre flux d’activation vers cette destination et les dates de début et de fin de l’activation pour le segment sélectionné. Si aucune date de fin n’est fournie pour l’activation, elle affiche le statut [!UICONTROL En cours]. Le segment à analyser est sélectionné dans la liste déroulante en haut de la page.

Le widget vous permet de découvrir en un coup d’œil où et quand l’audience est activée. De plus, il rend les activations en double ou inutiles plus transparentes. Ces informations cumulées indiquent également les endroits où les activations ont été laissées de côté.

![Widget Activations planifiées.](../images/segments/scheduled-activations.png)

## Étapes suivantes

Après avoir lu ce document, vous devriez maintenant pouvoir localiser le tableau de bord des segments et sélectionner un segment à afficher. Vous devriez également comprendre désormais les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des segments dans l’interface utilisateur d’Experience Platform, reportez-vous au [Guide de l’interface utilisateur de Segmentation Service](../../segmentation/ui/overview.md).
