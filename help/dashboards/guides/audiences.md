---
keywords: Experience Platform;profil;audience;audiences;segmentation;interface utilisateur;interface utilisateur;personnalisation;tableau de bord de l’audience;tableau de bord
title: Guide du tableau de bord Audiences
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les audiences que votre entreprise a créées.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 48%

---

# [!UICONTROL Audiences] tableau de bord {#audiences-dashboard}

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos audiences, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder à et utiliser le [!UICONTROL Audiences] tableau de bord dans l’interface utilisateur et fournit des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour obtenir un aperçu de toutes les fonctionnalités du service de segmentation d’Adobe Experience Platform au sein de l’interface utilisateur de la plateforme, veuillez consulter le [Guide de l’interface utilisateur du service de segmentation](../../segmentation/ui/overview.md).

## [!UICONTROL Audiences] données du tableau de bord

Le [!UICONTROL Audiences] Le tableau de bord affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils dans Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et la variable [!UICONTROL Audiences] Le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorez les [!UICONTROL Audiences] tableau de bord {#explore}

Pour accéder au [!UICONTROL Audiences] Tableau de bord dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Audiences]** dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre entreprise est une nouvelle entreprise de Platform et qu’elle ne dispose pas encore de jeux de données Profile principaux ni de stratégies de fusion créés, la variable [!UICONTROL Audiences] tableau de bord n’est pas visible. Au lieu de cela, l’onglet [!UICONTROL Présentation] affiche des liens et de la documentation pour vous aider à démarrer avec la segmentation.

![Le [!UICONTROL Audiences] tableau de bord [!UICONTROL Présentation] avec [!UICONTROL Audiences] et [!UICONTROL Présentation] surlignée.](../images/audiences/dashboard-overview.png)

### Modifiez le [!UICONTROL Audiences] tableau de bord {#modify}

Vous pouvez modifier l’aspect de la variable [!UICONTROL Audiences] tableau de bord en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord ainsi que d’accéder à la **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la section [Modification des tableaux de bord](../customize/modify.md) et [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

### Ajouter des widgets {#add-widget}

Sélectionnez **[!UICONTROL Ajouter un widget]** pour accéder à la bibliothèque de widgets et voir la liste des widgets disponibles à ajouter à votre tableau de bord.

![Le [!UICONTROL Audiences] présentation du tableau de bord avec [!UICONTROL Ajouter un widget] surlignée.](../images/audiences/audiences-overview-add-widget.png)

Dans la bibliothèque de widgets, vous pouvez parcourir la sélection de widgets d’audience standard et personnalisés. Pour plus d’informations sur l’ajout de widgets, consultez la documentation de la bibliothèque de widgets sur la manière d’[ajouter un widget](../customize/widget-library.md#add-widgets).

## Sélection d’une audience {#select-audience}

Le tableau de bord sélectionne automatiquement l’audience à afficher. Vous pouvez toutefois modifier l’audience à l’aide du menu déroulant ou du sélecteur d’audiences.

Pour choisir une autre audience, sélectionnez la liste déroulante en regard du nom de l’audience ou utilisez le sélecteur d’audience pour ouvrir la boîte de dialogue de sélection d’audience.

>[!IMPORTANT]
>
>Seules les audiences dont le nombre de profils est supérieur à zéro s’affichent dans la liste des audiences sélectionnables.

![Aperçu du tableau de bord Audiences avec le menu déroulant de l’audience globale en surbrillance.](../images/audiences/change-audience.png)

![Le [!UICONTROL Sélection de l’audience] qui affiche toutes les audiences disponibles.](../images/audiences/select-audience-dialog.png)

## Widgets et mesures {#widgets-and-metrics}

Le [!UICONTROL Audiences] Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur votre audience sélectionnée.

La date et l’heure de l’instantané le plus récent sont affichées en haut de la [!UICONTROL Présentation] en regard de la liste déroulante audience. Toutes les données du widget sont exactes à cette date et cette heure. La date et l’heure de l’instantané sont fournies en UTC ; elles ne se trouvent pas dans le fuseau horaire de l’utilisateur/utilisatrice ou de l’organisation.

![Onglet Aperçu des audiences avec un horodatage de widget mis en surbrillance.](../images/audiences/widget-timestamp.png)

## Widgets standard {#standard-widgets}

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos audiences. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la [!UICONTROL Bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire la [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

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
>abstract="Ce widget affiche le nombre total de profils fusionnés au sein de l’audience sélectionnée. Ce nombre dépend de la politique de fusion appliquée à vos données et est correct au moment de l’instantané le plus récent."

Le **[!UICONTROL Taille de l’audience]** widget affiche le nombre total de profils fusionnés dans l’audience sélectionnée au moment de la prise de vue instantanée. Ce nombre est le résultat de l’application de la stratégie de fusion d’audiences à vos données de profil pour fusionner des fragments de profil et former un seul profil pour chaque individu de l’audience.

Pour plus d&#39;informations sur les fragments et les profils fusionnés, reportez-vous à la section [Présentation de Real-Time Customer Profile](../../profile/home.md).

![Le [!UICONTROL Audiences] présentation du tableau de bord avec la fonction [!UICONTROL Taille de l’audience] widget mis en surbrillance.](../images/audiences/audience-size.png)

### [!UICONTROL Tendance de la taille de l’audience] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendance de la taille de l’audience"
>abstract="Ce widget fournit des informations sur le nombre total de profils qui répondent aux critères de **toute** définition de segment, telle qu’elle est capturée lors de l’instantané quotidien, pendant les derniers 30 jours, 90 jours ou 12 mois."

Le **[!UICONTROL Tendance de la taille de l’audience]** Le widget fournit une représentation graphique linéaire pour le nombre total de profils à inclure **any** sur une période donnée. La tendance de la taille d’audience peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. La taille de l’audience est représentée sur l’axe y et le temps est représenté sur l’axe x.

Ce widget inclut également le [!UICONTROL Sous-titres] fonction dans laquelle un modèle d’apprentissage automatique analyse les données de graphique et d’audience et génère automatiquement des sous-titres pour décrire les tendances clés et les événements importants. Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques.

![Le [!UICONTROL Audiences] La présentation affiche le widget de tendance de taille d’audience .](../images/audiences/audience-size-trend-captions.png)

La boîte de dialogue de légendes automatique s’ouvre, vous permettant d’obtenir des informations sur vos données.

![La boîte de dialogue de légendes automatique pour le widget Tendance de la taille d’audience.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Pour en savoir plus sur l’évaluation des audiences et sur la façon dont les profils remplissent les critères et sortent des audiences, reportez-vous à la section [Documentation de Segmentation Service](../../segmentation/home.md).

### [!UICONTROL Tendance de changement de la taille de l’audience] {#audience-size-change-trend}

Ce widget fournit un graphique linéaire qui illustre la différence entre le nombre total de profils qualifiés pour une audience donnée et les instantanés quotidiens les plus récents. L’audience choisie pour l’analyse est sélectionnée dans la liste déroulante de présentation. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. La taille de l’audience est représentée sur l’axe y et le temps est représenté sur l’axe x.

![Le widget pour la tendance du changement de la taille d’audience.](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Tendance de la taille de l’audience par identité] {#audience-size-trend-by-identity}

Ce widget illustre la tendance de taille de l’audience pour une audience spécifique en fonction du type d’identité sélectionné dans le menu déroulant du widget. L’audience utilisée pour l’analyse est sélectionnée dans la liste déroulante d’aperçu. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget.

![Widget pour la tendance de la taille des audiences par identité.](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Ordre d’activation de l’audience] {#audience-activation-order}

Le widget [!UICONTROL Ordre d’activation de l’audience] génère un tableau à trois colonnes qui répertorie le nom de la destination, la plateforme et la date d’activation de l’audience. La liste est classée en fonction de la date en commençant par la plus récente et peut contenir jusqu’à 10 lignes.

![Le widget Ordre d’activation de l’audience.](../images/audiences/audience-activation-order.png)

### [!UICONTROL Chevauchement des audiences] {#audience-overlap}

Ce widget utilise un diagramme de Venn pour visualiser le nombre de personnes qui correspondent aux critères des deux audiences. Les audiences utilisées pour la comparaison sont sélectionnées dans les menus déroulants du widget. Le nombre total de profils contenus dans la définition de segment correspondante peut être affiché en passant la souris sur un cercle ou sur l’intersection du diagramme de Venn.

Ce widget vous permet d’optimiser la stratégie de segmentation en consultant les similitudes dans les résultats de vos définitions de segment.

![Le widget de chevauchement des audiences.](../images/audiences/audience-overlap.png)

### [!UICONTROL Rapport de chevauchement des audiences] {#audience-overlap-report}

Ce widget tabulaire les données de chevauchement de profils pour une audience spécifique. Une liste de cinq audiences classées des pourcentages de chevauchement les plus élevés aux plus bas est fournie pour l’audience choisie dans le menu déroulant en haut de l’écran. Pour plus de clarté, l’audience choisie est répertoriée dans la variable [!UICONTROL AUDIENCE A NAME] colonne . L’analyse du chevauchement des audiences est fournie pour la deuxième audience répertoriée dans le [!UICONTROL NOM DE L’AUDIENCE B] colonne . Le chevauchement en pourcentage est fourni dans la troisième colonne avec une précision de douze décimales.

Le rapport sur les chevauchements d’audiences vous aide à créer de nouvelles audiences hautement performantes. L’observation des chevauchements au pourcentage élevé vous permet de supprimer des audiences et d’empêcher l’envoi d’une même audience vers différentes destinations. Elle vous aide également à identifier les informations cachées qui peuvent contribuer à une meilleure segmentation. Un chevauchement au pourcentage faible permet de localiser les profils uniques à rechercher.

Sélectionnez **[!UICONTROL Afficher plus]** pour ouvrir une boîte de dialogue plein écran contenant davantage de données de chevauchement des audiences.

![Le widget Rapport de chevauchement des audiences avec l’option Afficher plus en surbrillance.](../images/audiences/audience-overlap-report.png)

La boîte de dialogue [!UICONTROL Rapport de chevauchement des audiences] s’affiche. Cette boîte de dialogue peut contenir jusqu’à 50 lignes d’analyses de chevauchement des audiences, divisées en six colonnes. Sélectionnez l’icône des paramètres (![Icône des paramètres.](../images/audiences/settings-icon.png)) pour supprimer ou ajouter des colonnes du tableau.

![Boîte de dialogue Rapport de chevauchement des audiences.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Sélectionnez l’en-tête de colonne **[!UICONTROL Chevauchement]** pour modifier le classement des résultats, du plus haut au plus bas ou du plus bas au plus haut.

Pour télécharger l’intégralité du rapport au format PDF, sélectionnez le menu d’options (**`...`**), puis **[!UICONTROL Télécharger]**.

![La boîte de dialogue Rapport de chevauchement des audiences avec les points de suspension et l’option de téléchargement en surbrillance.](../images/audiences/audience-overlap-report-dialog-download.png)

Sélectionnez une ligne dans le rapport pour ouvrir un diagramme de Venn de l’analyse de chevauchement. Passez la souris sur une section du diagramme de Venn pour afficher le nombre de profils dans une boîte de dialogue.

![La boîte de dialogue Rapport de chevauchement des audiences avec un diagramme de Venn et une ligne en surbrillance.](../images/audiences/audience-overlap-report-dialog-venn.png)

Sélectionner **[!UICONTROL Fermer]** pour revenir au [!UICONTROL Audiences] tableau de bord.

### [!UICONTROL Chevauchement des identités] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Chevauchement des identités"
>abstract="Ce widget montre le chevauchement des profils de votre audience contenant les deux identités sélectionnées. Les cercles affichent la taille relative de chaque identité. Le nombre de profils contenant les deux espaces de noms est représenté par le chevauchement entre les cercles."

Le **[!UICONTROL Superposition des identités]** ce widget affiche un diagramme de Venn, ou un diagramme de jeu, qui montre le chevauchement des profils de votre audience contenant plusieurs identités.

Utilisez les menus déroulants du widget pour sélectionner les identités à comparer. Les cercles affichent la taille relative de chaque identité choisie, le nombre de profils contenant les deux espaces de noms étant représenté par la taille du chevauchement entre les cercles.

Si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités seront associées à ce client individuel. Cela signifie qu’il est probable que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour en savoir plus sur les identités, rendez-vous sur la page [Documentation d’Identity Service](../../identity-service/home.md).

![Le [!UICONTROL Audiences] Présentation du tableau de bord avec le widget de chevauchement d’identités surligné.](../images/audiences/identity-overlap.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profils par identité"
>abstract="Ce widget affiche la ventilation des identités pour chaque profil fusionné de l’audience sélectionnée."

Le **[!UICONTROL Profils par identité]** widget affiche la ventilation des identités pour chaque profil fusionné de l’audience sélectionnée. Le nombre total de profils par identité peut être supérieur au nombre total de profils dans l’audience, car plusieurs identités peuvent y être associées pour un profil. En d’autres termes, le fait de additionner les valeurs affichées pour chaque identité peut représenter un total supérieur à la taille totale de l’audience. En effet, si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités peuvent être associées à ce client individuel.

Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques.

![Le [!UICONTROL Audiences] Présentation du tableau de bord avec l’option Profils par widget d’identité et Légendes mise en surbrillance.](../images/audiences/profiles-by-identity.png)

Un modèle de machine learning génère automatiquement des informations sur les données en analysant la distribution globale et les dimensions clés des données.

Pour en savoir plus sur les identités, rendez-vous sur la page [Documentation d’Identity Service](../../identity-service/home.md).

### Activations planifiées {#scheduled-activations}

Le widget d’[!UICONTROL activations planifiées] offre une vue tabulée des destinations activées le plus récemment. Le tableau comprend la plateforme de destination, le nom de votre flux d’activation vers cette destination et les dates de début et de fin de l’activation pour l’audience sélectionnée. Si aucune date de fin n’est fournie pour l’activation, elle affiche le statut [!UICONTROL En cours]. L’audience à analyser est sélectionnée dans la liste déroulante en haut de la page.

Le widget vous permet de découvrir en un coup d’œil où et quand l’audience est activée. De plus, il rend les activations en double ou inutiles plus transparentes. Ces informations cumulées indiquent également les endroits où les activations ont été laissées de côté.

![Widget Activations planifiées.](../images/audiences/scheduled-activations.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser la variable [!UICONTROL Audiences] tableau de bord et sélectionnez l’audience à afficher. Vous devriez également comprendre désormais les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des audiences dans l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Segmentation Service](../../segmentation/ui/overview.md).
