---
keywords: Experience Platform;profil;audience;audiences;segmentation;interface utilisateur;interface utilisateur;personnalisation;tableau de bord d’audience;tableau de bord
title: Tableau de bord des audiences
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les audiences créées par votre organisation.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3136'
ht-degree: 38%

---

# Tableau de bord des [!UICONTROL Audiences] {#audiences-dashboard}

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos audiences. Celles-ci sont présentées telles qu’elles sont capturées lors d’instantanés quotidiens. Ce guide explique comment accéder au tableau de bord [!UICONTROL Audiences] et l’utiliser dans l’interface utilisateur. Il fournit également des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour une présentation de toutes les fonctionnalités du service de segmentation de Adobe Experience Platform dans l’interface utilisateur d’Experience Platform, consultez le [guide de l’interface utilisateur du service de segmentation](../../segmentation/ui/overview.md).

## [!UICONTROL Audiences] données du tableau de bord

Le tableau de bord [!UICONTROL Audiences] affiche un instantané des données d’attribut (enregistrement) dont dispose votre organisation dans la banque de profils d’Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord [!UICONTROL Audiences] n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorez le tableau de bord [!UICONTROL Audiences] {#explore}

Pour accéder au tableau de bord [!UICONTROL Audiences] dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Audiences]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre organisation débute dans l’utilisation d’Experience Platform et n’a pas encore de jeux de données de profils actifs ou de politiques de fusion créés, le tableau de bord [!UICONTROL Audiences] n’est pas visible. Au lieu de cela, l’onglet [!UICONTROL Présentation] affiche des liens et de la documentation pour vous aider à démarrer avec la segmentation.

![Onglet du tableau de bord [!UICONTROL Audiences] [!UICONTROL Présentation] avec [!UICONTROL Audiences] et [!UICONTROL Présentation] en surbrillance.](../images/audiences/dashboard-overview.png)

### Modification du tableau de bord [!UICONTROL Audiences] {#modify}

Vous pouvez modifier l’aspect du tableau de bord [!UICONTROL Audiences] en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord ainsi que d’accéder à la **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la section [Modification des tableaux de bord](../customize/modify.md) et [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

### Ajouter des widgets {#add-widget}

Sélectionnez **[!UICONTROL Ajouter un widget]** pour accéder à la bibliothèque de widgets et voir la liste des widgets disponibles à ajouter à votre tableau de bord.

![Présentation du tableau de bord [!UICONTROL Audiences] avec [!UICONTROL Ajouter un widget] en surbrillance.](../images/audiences/audiences-overview-add-widget.png)

Dans la bibliothèque de widgets, vous pouvez parcourir la sélection de widgets d’audience standard et personnalisés. Pour plus d’informations sur l’ajout de widgets, consultez la documentation de la bibliothèque de widgets sur la manière d’[ajouter un widget](../customize/widget-library.md#add-widgets).

### Afficher le SQL {#view-sql}

Vous pouvez afficher le code SQL qui génère les informations visualisées dans votre tableau de bord à l’aide du bouton (bascule) de l’espace de travail [!UICONTROL Présentation]. Vous pouvez vous inspirer du SQL de vos informations existantes pour créer de nouvelles requêtes qui obtiennent des informations uniques des données Experience Platform en fonction des besoins de votre entreprise. Pour en savoir plus sur cette fonctionnalité, consultez le guide de l’interface utilisateur [View SQL](../view-sql.md).

## Sélectionner une audience {#select-audience}

Le tableau de bord sélectionne automatiquement une audience à afficher. Cependant, vous pouvez modifier l’audience à l’aide du menu déroulant ou du sélecteur d’audience.

Pour choisir une autre audience, sélectionnez la liste déroulante à côté du nom de l’audience ou utilisez le sélecteur d’audience pour ouvrir la boîte de dialogue de sélection d’audience.

>[!IMPORTANT]
>
>Seules les audiences dont le nombre de profils est supérieur à zéro s’affichent dans la liste des audiences sélectionnables.

![Présentation du tableau de bord des audiences avec le menu déroulant de l’audience globale en surbrillance.](../images/audiences/change-audience.png)

![Boîte de dialogue [!UICONTROL &#x200B; Sélectionner une audience] qui affiche toutes les audiences disponibles.](../images/audiences/select-audience-dialog.png)

## Widgets et mesures {#widgets-and-metrics}

Le tableau de bord [!UICONTROL Audiences] est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur l’audience sélectionnée.

La date et l’heure de l’instantané le plus récent sont affichées en haut de l’onglet [!UICONTROL Présentation] à côté du menu déroulant de l’audience. Toutes les données du widget sont exactes à cette date et cette heure. La date et l’heure de l’instantané sont fournies en UTC ; elles ne se trouvent pas dans le fuseau horaire de l’utilisateur/utilisatrice ou de l’organisation.

![Onglet Présentation des audiences avec un horodatage de widget mis en surbrillance.](../images/audiences/widget-timestamp.png)

## Widgets par défaut {#default-widgets}

Un widget de chargement par défaut est fourni pour toutes les nouvelles instances de Adobe Experience Platform qui met en évidence les dernières informations disponibles à partir de vos données. Les widgets suivants sont préconfigurés dans votre vue de segments dès le départ. Vous trouverez des détails complets sur l’objectif et la fonction des widgets dans leurs sections respectives.

* [[!UICONTROL Taille de l’audience]](#audience-size)
* [[!UICONTROL Tendance de changement de la taille de l’audience]](#audience-size-change-trend)
* [[!UICONTROL Chevauchement des identités]](#identity-overlap)
* [[!UICONTROL Profils par identité]](#profiles-by-identity)

>[!NOTE]
>
>Depuis le 26 juillet 2023, les tableaux de bord [!UICONTROL Profils], [!UICONTROL Audiences] et [!UICONTROL Destinations] Aperçu ont été réinitialisés à un nouveau chargement de widget par défaut pour tous les utilisateurs qui n’ont pas modifié leurs vues au cours des six mois précédents.
>Reportez-vous à la documentation dans les sections de widget par défaut [Profils](./profiles.md#default-widgets) et [Destinations](./destinations.md#default-widgets) pour plus d’informations sur les widgets inclus dans le cadre des chargements de widget par défaut. Vous pouvez continuer à personnaliser les widgets de votre tableau de bord comme auparavant.

## Widgets de l’IA dédiée aux clients {#customer-ai-audiences-widgets}

Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Pour ce faire, l’IA dédiée aux clients analyse les données d’événement d’expérience client existantes afin de prédire les scores de propension **attrition ou conversion**. Ces modèles de propension des clients à haute précision permettent une segmentation et un ciblage plus précis. Les informations [distribution des scores](#customer-ai-distribution-of-scores) et [résumé de notation](#customer-ai-scoring-summary) illustrent la division au sein de votre audience. Ils mettent en évidence les profils à propension élevée/faible/moyenne et la manière dont ils sont répartis entre vos nombres de profils.

* [[!UICONTROL Résumé des scores de l’IA dédiée aux clientes et aux clients]](#customer-ai-scoring-summary)
* [[!UICONTROL Distribution des scores par l’IA dédiée aux clientes et aux clients]](#customer-ai-distribution-of-scores)

### [!UICONTROL Distribution des scores par l’IA dédiée aux clientes et aux clients] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_distributionOfScores"
>title="Distribution des scores"
>abstract="Ce widget visualise la distribution du nombre total de profils en fonction de leurs scores de propension, par incréments de cinq pour cent. La distribution du nombre de profils est déterminée par le modèle d’IA et la politique de fusion sélectionnée. Vous pouvez modifier le modèle d’IA dans le menu déroulant sous le titre du widget."

Le widget [!UICONTROL &#x200B; Distribution des scores de l’IA dédiée aux clients &#x200B;] classe le nombre total de profils en fonction de leurs scores de propension. La distribution du nombre de profils est déterminée par le modèle d’IA et la politique de fusion sélectionnée, puis visualisée par incréments de cinq pour cent qui indiquent leur propension. Le nombre de profils est indiqué le long de l’axe Y et les scores de propension le long de l’axe X.

>[!NOTE]
>
>Si la visualisation est un score de propension à la conversion, les scores les plus élevés s’affichent en vert et les scores les plus bas en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

Le modèle d’IA qui détermine les scores de propension est sélectionné dans le sélecteur de liste déroulante sous le titre du widget. La liste déroulante contient la liste de tous les modèles d’IA dédiée aux clients configurés. Sélectionnez le modèle d’IA approprié à votre analyse dans la liste des modèles disponibles. Si aucun modèle d’IA dédiée aux clients n’est disponible, un message dans le widget vous demande de configurer au moins un modèle d’IA dédiée aux clients et fournit un lien hypertexte vers la page de configuration du modèle d’IA dédiée aux clients. Consultez la documentation pour obtenir des instructions sur [comment configurer une instance IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Sélectionnez la liste déroulante juste en dessous de l’onglet Aperçu pour modifier la politique de fusion qui détermine les profils inclus dans l’analyse. Consultez la section [politiques de fusion](#merge-policies) pour une brève description, ou la [présentation de la politique de fusion](../../profile/merge-policies/overview.md) pour plus d’informations.

Pour accéder à la page d’informations détaillées pour le modèle IA dédiée aux clients sélectionné, sélectionnez **[!UICONTROL Afficher les détails du modèle]**.

![Tableau de bord des audiences Experience Platform avec le [!UICONTROL répartition des scores dans l’IA dédiée aux clients] widget et [!UICONTROL Afficher les détails du modèle] mis en surbrillance.](../images/segments/customer-ai-distribution-of-scores.png)

La page d’informations détaillées sur le modèle s’affiche.

![Page d’informations pour l’IA dédiée aux clients.](../images/profiles/customer-ai-insights-page.png)

Vous trouverez plus d’informations sur l’IA dédiée aux clients dans le guide de l’interface utilisateur [Discover Insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Résumé des scores de l’IA dédiée aux clientes et aux clients] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_scoringSummary"
>title="Résumé des scores"
>abstract="Le résumé des scores affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible. Le graphique en anneau illustre la composition proportionnelle du total des profils selon la propension élevée, moyenne et faible."

Ce widget affiche le nombre total de profils notés et les classe dans des compartiments contenant des valeurs élevées, moyennes et faibles de propension, respectivement en vert, jaune et rouge. Un graphique en anneau est utilisé pour illustrer la composition proportionnelle des profils totaux entre des propensions élevées, moyennes et faibles, telles que le vert, le jaune et le rouge respectivement. Un profil est qualifié pour une propension élevée à plus de 75 ans, une propension moyenne entre 25 et 74 ans et une propension faible avant 24 ans. Une légende indique le code couleur et les seuils des propensions. Le nombre de profils pour les propensions élevée, moyenne et faible est affiché dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

>[!NOTE]
>
>Si la visualisation est un score de propension à la conversion, les scores les plus élevés s’affichent en vert et les scores les plus bas en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

Le menu déroulant situé sous le titre du widget fournit une liste de tous les modèles d’IA dédiée aux clients configurés. Sélectionnez le modèle d’IA approprié à votre analyse dans la liste des modèles disponibles. Si aucun modèle d’IA dédiée aux clients n’est disponible, un message dans le widget vous demande de configurer au moins un modèle d’IA dédiée aux clients et fournit un lien hypertexte vers la page de configuration du modèle d’IA dédiée aux clients. Pour obtenir des instructions détaillées, consultez la documentation sur [comment configurer une instance IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Le nombre total de profils calculés dépend de la politique de fusion choisie. Pour modifier la politique de fusion utilisée, sélectionnez la liste déroulante juste en dessous de l’onglet Aperçu . Consultez la section [politiques de fusion](#merge-policies) pour une brève description, ou la [présentation de la politique de fusion](../../profile/merge-policies/overview.md) pour plus d’informations.

![Tableau de bord des audiences Experience Platform avec le widget Résumé du score de l’IA dédiée aux clients en surbrillance.](../images/segments/customer-ai-scoring-summary.png)

Sélectionnez **[!UICONTROL Afficher les détails du modèle]** pour accéder à la page d’informations détaillées pour le modèle d’IA dédiée aux clients sélectionné. Vous trouverez plus d’informations sur l’IA dédiée aux clients dans le guide de l’interface utilisateur [Discover Insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

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
>abstract="Ce widget affiche le nombre total de profils fusionnés dans l’audience sélectionnée. Ce nombre dépend de la politique de fusion appliquée à vos données et est correct au moment de l’instantané le plus récent."

Le widget **[!UICONTROL Taille de l’audience]** affiche le nombre total de profils fusionnés dans l’audience sélectionnée au moment de la prise de l’instantané. Ce nombre est le résultat de l’application de la politique de fusion d’audience à vos données de profil afin de fusionner les fragments de profil et de former un seul profil pour chaque individu de l’audience.

Pour plus d’informations sur les fragments et les profils fusionnés, reportez-vous à la section [Présentation de Real-Time Customer Profile](../../profile/home.md).

![Présentation du tableau de bord [!UICONTROL Audiences] avec le widget [!UICONTROL Taille de l’audience] en surbrillance.](../images/audiences/audience-size.png)

### [!UICONTROL Tendance de la taille de l’audience] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendance de la taille de l’audience"
>abstract="Ce widget fournit des informations sur le nombre total de profils qui répondent aux critères de **toute** définition de segment, telle qu’elle est capturée lors de l’instantané quotidien, pendant les derniers 30 jours, 90 jours ou 12 mois."

Le widget **[!UICONTROL Tendance de la taille d’audience]** fournit une représentation graphique linéaire pour le nombre total de profils qui remplissent les critères d’une audience **quelconque** sur une période donnée. La tendance de la taille d’audience peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. La taille de l’audience est représentée sur l’axe y et le temps est représenté sur l’axe x.

Ce widget inclut également la fonctionnalité automatique [!UICONTROL Légendes] dans laquelle un modèle de machine learning analyse le graphique et les données d’audience et génère automatiquement des légendes pour décrire les tendances clés et les événements importants. Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques.

![La présentation [!UICONTROL Audiences] affiche le widget Tendance de la taille d’audience.](../images/audiences/audience-size-trend-captions.png)

La boîte de dialogue de légendes automatique s’ouvre, vous permettant d’obtenir des informations sur vos données.

![La boîte de dialogue de légendes automatique pour le widget Tendance de la taille d’audience.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Pour en savoir plus sur l’évaluation des audiences et sur la manière dont les profils sont qualifiés et quittent des audiences, reportez-vous à la [documentation de Segmentation Service](../../segmentation/home.md).

### [!UICONTROL Tendance de changement de la taille de l’audience] {#audience-size-change-trend}

Ce widget fournit un graphique linéaire qui illustre la différence entre le nombre total de profils qualifiés pour une audience donnée et les instantanés quotidiens les plus récents. L’audience choisie pour l’analyse est sélectionnée dans le menu déroulant de la vue d’ensemble. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. La taille de l’audience est représentée sur l’axe y et le temps est représenté sur l’axe x.

![Le widget pour la tendance du changement de la taille d’audience.](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Tendance de la taille de l’audience par identité] {#audience-size-trend-by-identity}

Ce widget illustre la tendance de la taille de l’audience pour une audience particulière en fonction du type d’identité choisi dans le menu déroulant du widget. L’audience utilisée pour l’analyse est sélectionnée dans le menu déroulant de la vue d’ensemble. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget.

![Widget pour la tendance de la taille des audiences par identité.](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Ordre d’activation de l’audience] {#audience-activation-order}

Le widget [!UICONTROL &#x200B; Ordre d’activation de l’audience &#x200B;] fournit un tableau à trois colonnes qui répertorie le nom de la destination, la plateforme et la date d’activation de l’audience. La liste est classée en fonction de la date en commençant par la plus récente et peut contenir jusqu’à 10 lignes.

![Le widget Ordre d’activation de l’audience.](../images/audiences/audience-activation-order.png)

### [!UICONTROL Chevauchement des audiences] {#audience-overlap}

Ce widget utilise un diagramme de Venn pour visualiser le nombre de personnes qui correspondent aux critères des deux audiences. Les audiences utilisées pour la comparaison sont sélectionnées dans les menus déroulants du widget. Le nombre total de profils contenus dans la définition de segment appropriée peut être affiché en passant la souris sur un cercle ou sur l’intersection du diagramme de Venn.

Ce widget vous permet d’optimiser la stratégie de segmentation en consultant les similitudes dans les résultats de vos définitions de segment.

![Le widget de chevauchement des audiences.](../images/audiences/audience-overlap.png)

### [!UICONTROL Rapport de chevauchement des audiences] {#audience-overlap-report}

Ce widget tabularise les données de chevauchement des profils pour une audience spécifique. Une liste de cinq audiences classées du pourcentage de chevauchement le plus élevé au plus faible est fournie pour l’audience choisie dans le menu déroulant en haut de l’écran. Pour plus de clarté, l’audience choisie est répertoriée dans la colonne [!UICONTROL NOM DE L’AUDIENCE A]. L’analyse du chevauchement des audiences est fournie pour la deuxième audience répertoriée dans la colonne [!UICONTROL NOM DE L’AUDIENCE B]. Le chevauchement en pourcentage est fourni dans la troisième colonne avec une précision de douze décimales.

Le rapport sur le chevauchement des audiences vous permet de créer de nouvelles audiences hautement performantes. L’observation des chevauchements au pourcentage élevé vous permet de supprimer des audiences et d’empêcher l’envoi d’une même audience vers différentes destinations. Elle vous aide également à identifier les informations cachées qui peuvent contribuer à une meilleure segmentation. Un chevauchement au pourcentage faible permet de localiser les profils uniques à rechercher.

Sélectionnez **[!UICONTROL Afficher plus]** pour ouvrir une boîte de dialogue plein écran contenant davantage de données de chevauchement des audiences.

![Le widget Rapport de chevauchement des audiences avec l’option Afficher plus en surbrillance.](../images/audiences/audience-overlap-report.png)

La boîte de dialogue [!UICONTROL Rapport de chevauchement des audiences] s’affiche. Cette boîte de dialogue peut contenir jusqu’à 50 lignes d’analyses de chevauchement des audiences, divisées en six colonnes. Sélectionnez l’icône des paramètres (![Icône des paramètres.](/help/images/icons/settings.png)) pour supprimer ou ajouter des colonnes du tableau.

![Boîte de dialogue Rapport de chevauchement des audiences.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Sélectionnez l’en-tête de colonne **[!UICONTROL Chevauchement]** pour modifier le classement des résultats, du plus haut au plus bas ou du plus bas au plus haut.

Pour télécharger l’intégralité du rapport au format PDF, sélectionnez le menu d’options (**`...`**), puis **[!UICONTROL Télécharger]**.

![La boîte de dialogue Rapport de chevauchement des audiences avec les points de suspension et l’option de téléchargement en surbrillance.](../images/audiences/audience-overlap-report-dialog-download.png)

Sélectionnez une ligne dans le rapport pour ouvrir un diagramme de Venn de l’analyse de chevauchement. Passez la souris sur une section du diagramme de Venn pour afficher le nombre de profils dans une boîte de dialogue.

![La boîte de dialogue Rapport de chevauchement des audiences avec un diagramme de Venn et une ligne en surbrillance.](../images/audiences/audience-overlap-report-dialog-venn.png)

Sélectionnez **[!UICONTROL Fermer]** pour revenir au tableau de bord [!UICONTROL Audiences].

### [!UICONTROL Chevauchement des identités] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Chevauchement des identités"
>abstract="Ce widget affiche le chevauchement des profils de votre audience contenant les deux identités sélectionnées. Les cercles affichent la taille relative de chaque identité. Le nombre de profils contenant les deux espaces de noms est représenté par le chevauchement entre les cercles."

Le widget **[!UICONTROL Chevauchement des identités]** affiche un diagramme de Venn, ou diagramme logique, qui montre le chevauchement des profils de votre audience contenant plusieurs identités.

Utilisez les menus déroulants du widget pour sélectionner les identités à comparer. Les cercles affichent la taille relative de chaque identité choisie, le nombre de profils contenant les deux espaces de noms étant représenté par la taille du chevauchement entre les cercles.

Si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités seront associées à ce client individuel. Cette situation rend probable le fait que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour en savoir plus sur les identités, consultez la [documentation du service d’identités](../../identity-service/home.md).

![Présentation du tableau de bord [!UICONTROL Audiences] avec le widget Chevauchement des identités en surbrillance.](../images/audiences/identity-overlap.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profils par identité"
>abstract="Ce widget affiche la répartition des identités pour chaque profil fusionné dans votre audience sélectionnée."

Le widget **[!UICONTROL Profils par identité]** affiche la répartition des identités pour chaque profil fusionné de l’audience sélectionnée. Le nombre total de profils par identité peut être supérieur au nombre total de profils dans l’audience, car plusieurs identités peuvent être associées à un même profil. En d’autres termes, le fait de cumuler les valeurs affichées pour chaque identité peut donner un total supérieur à la taille totale de l’audience. En effet, si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités peuvent être associées à ce client individuel.

Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques.

![Présentation du tableau de bord [!UICONTROL Audiences] avec le widget Profils par identité et l’option Légendes en surbrillance.](../images/audiences/profiles-by-identity.png)

Un modèle de machine learning génère automatiquement des informations sur les données en analysant la distribution globale et les dimensions clés des données.

Pour en savoir plus sur les identités, consultez la [documentation du service d’identités](../../identity-service/home.md).

### Activations planifiées {#scheduled-activations}

Le widget d’[!UICONTROL activations planifiées] offre une vue tabulée des destinations activées le plus récemment. Le tableau comprend la plateforme de destination, le nom de votre flux d’activation vers cette destination et les dates de début et de fin de l’activation pour l’audience sélectionnée. Si aucune date de fin n’est fournie pour l’activation, elle affiche le statut [!UICONTROL En cours]. L’audience à analyser est sélectionnée dans la liste déroulante en haut de la page.

Le widget vous permet de découvrir en un coup d’œil où et quand l’audience est activée. De plus, il rend les activations en double ou inutiles plus transparentes. Ces informations cumulées indiquent également les endroits où les activations ont été laissées de côté.

![Widget Activations planifiées.](../images/audiences/scheduled-activations.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord [!UICONTROL Audiences] et sélectionner une audience à afficher. Vous devriez également comprendre désormais les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des audiences dans l’interface utilisateur d’Experience Platform, reportez-vous au [&#x200B; Guide de l’interface utilisateur de Segmentation Service](../../segmentation/ui/overview.md).
