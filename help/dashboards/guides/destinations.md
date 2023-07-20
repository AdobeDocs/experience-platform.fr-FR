---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord Profil;tableau de bord
title: Guide du tableau de bord des destinations
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les destinations actives de votre organisation.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 66%

---

# Tableau de bord des [!UICONTROL destinations]

L’interface utilisateur d’Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les destinations actives de votre organisation. Celles-ci sont présentées telles qu’elles sont capturées lors d’instantanés quotidiens. Ce guide explique comment accéder au tableau de bord des destinations et l’utiliser dans l’interface utilisateur. Il fournit également des informations supplémentaires sur les mesures affichées dans le tableau de bord.

Pour obtenir un aperçu des destinations, ainsi qu’un catalogue de toutes les destinations disponibles dans Experience Platform, veuillez consulter la [documentation sur les destinations](../../destinations/home.md).

## Données du tableau de bord des [!UICONTROL destinations] {#destinations-dashboard-data}

Le tableau de bord des destinations affiche un instantané des destinations activées par votre entreprise dans Experience Platform. Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En dʼautres termes, lʼinstantané nʼest pas une approximation ou un exemple des données, et le tableau de bord des destinations n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorez le tableau de bord des [!UICONTROL destinations] {#explore}

Pour accéder au tableau de bord des destinations dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Destinations]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Présentation]** pour afficher le tableau de bord.

La date et l’heure de l’instantané le plus récent s’affichent en haut de la [!UICONTROL Présentation] à côté du menu déroulant de destination. Toutes les données du widget sont exactes à cette date et cette heure. La date et l’heure de l’instantané sont fournies en UTC ; elles ne se trouvent pas dans le fuseau horaire de l’utilisateur/utilisatrice ou de l’organisation.

>[!NOTE]
>
>Si votre organisation débute dans l’utilisation d’Experience Platform et n’a pas encore de destinations actives, le tableau de bord des destinations et l’onglet [!UICONTROL Présentation] ne sont pas visibles. À la place, sélectionnez [!UICONTROL Destinations] dans le volet de navigation de gauche pour afficher l’onglet [!UICONTROL Catalogue]. Pour en savoir plus sur l’onglet [!UICONTROL Catalogue], voir le [[!UICONTROL guide d’espace de travail des ]destinations](../../destinations/ui/destinations-workspace.md).

![Présentation des destinations de l’interface utilisateur de Platform avec l’instantané le plus récent en surbrillance.](../images/destinations/snapshot-timestamp.png)

### Modifier le tableau de bord des [!UICONTROL destinations] {#modify}

Sélectionnez **[!UICONTROL Modifier le tableau de bord]** pour modifier l’aspect du tableau de bord des destinations. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord, ainsi que d’accéder à la bibliothèque de widgets. Dans la bibliothèque de widgets, vous pouvez explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la documentation sur la [modification des tableaux de bord](../customize/modify.md) et la [présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

### Ajouter des widgets {#add-widget}

Sélectionnez **[!UICONTROL Ajouter un widget]** pour accéder à la bibliothèque de widgets et voir la liste des widgets disponibles à ajouter à votre tableau de bord.

![Aperçu du tableau de bord des destinations avec le bouton Ajouter un widget en surbrillance.](../images/destinations/destinations-overview-add-widget.png)

Dans la bibliothèque de widgets, vous pouvez parcourir la sélection de widgets d’audience standard et personnalisés. Pour plus d’informations sur l’ajout de widgets, consultez la documentation de la bibliothèque de widgets sur la manière d’[ajouter un widget](../customize/widget-library.md#add-widgets).

## Widgets standard {#standard-widgets}

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos destinations et évaluer l’exhaustivité des audiences disponibles pour votre analyse des données. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la [!UICONTROL Bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire la [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

### Conditions préalables {#prerequisites}

Avant de poursuivre avec les descriptions des widgets standard, assurez-vous de bien connaître les définitions des termes clés suivants utilisés dans toute la documentation :

* **Définition de segment :** Une définition de segment est une **ensemble de règles** utilisé pour décrire les caractéristiques ou le comportement clés d’une audience cible. Ces règles incluent des données d’attribut et d’événement qui qualifient les profils comme faisant partie d’une audience.
* **Audience** : ensemble de personnes, de comptes, de foyers ou d’autres entités qui partagent des caractéristiques et des comportements communs.
* **Mappé/Mappage**: Le mappage des données est le processus de mappage des champs de données sources aux champs cibles associés dans une destination.
* **Identité**: Une identité est un identifiant qui représente de manière unique un client individuel, tel qu’un identifiant de cookie, un identifiant d’appareil ou un identifiant de courrier électronique.
* **Activer**: Activer est l’action entreprise par un utilisateur pour mapper une audience ou des profils à une destination telle que l’Oracle Eloqua, Google ou le Marketing Cloud Salesforce.

Pour en savoir plus sur chacun des widgets standards disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Destinations les plus utilisées]](#most-used-destinations)
* [[!UICONTROL Destinations créées récemment]](#recently-created-destinations)
* [[!UICONTROL Audiences récemment activées]](#recently-activated-audiences)
* [[!UICONTROL Audiences récemment activées par destination]](#recently-activated-audiences-by-destination)
* [[!UICONTROL Tendance de la taille de l’audience]](#audience-size-trend)
* [[!UICONTROL Audiences non mappées par identité]](#unmapped-audiences-by-identity)
* [[!UICONTROL Audiences mappées par identité]](#mapped-audiences-by-identity)
* [[!UICONTROL Audiences courantes]](#common-audiences)
* [[!UICONTROL Audiences mappées]](#mapped-audiences)
* [[!UICONTROL Intégrité de l’audience mappée]](#mapped-audience-health)
* [[!UICONTROL Nombre de destinations]](#destinations-count)
* [[!UICONTROL Statut de destination]](#destination-status)
* [[!UICONTROL Destinations actives par plateforme de destination]](#active-destinations-by-destination-platform)
* [[!UICONTROL Audiences activées sur toutes les destinations]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Audiences activées]](#activated-audiences)

### [!UICONTROL Destinations les plus utilisées] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Destinations les plus utilisées"
>abstract="Ce widget affiche les destinations les plus actives de votre organisation en fonction du nombre d’audiences mappées. Ces chiffres sont précis au moment du dernier instantané. Ce classement fournit des informations sur les destinations les plus utilisées actuellement tout en mettant en évidence celles qui peuvent être sous-utilisées."

Le **[!UICONTROL Destinations les plus utilisées]** le widget affiche les principales destinations de votre entreprise en fonction du nombre d’audiences mappées, à partir du dernier instantané. Ce classement permet de savoir quelles destinations sont utilisées, tout en présentant éventuellement celles qui peuvent être sous-utilisées.

Par exemple, si vous avez configuré une destination hier mais que vous ne lui avez mappé aucune audience, vous pouvez constater que la destination est actuellement sous-utilisée.

Le nombre d’audiences mappées affiché dans la variable [!UICONTROL Nombre d’audiences] est exacte à partir du dernier instantané quotidien. Le mappage d’une nouvelle audience à la destination ne met pas à jour le décompte tant que l’instantané suivant n’a pas été pris.

Sélectionnez le nom d’une destination dans la liste affichée sur le widget pour accéder aux détails de destination de cette destination spécifique. Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder à l’onglet **[!UICONTROL Parcourir]** et sélectionner le nom d’une destination pour en afficher les détails.

![L’Onglet Aperçu du tableau de bord Destinations avec le widget Destinations les plus utilisées en surbrillance.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinations récemment créées] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Destinations récemment créées"
>abstract="Ce widget affiche la liste des destinations configurées les plus récemment au sein de votre organisation."

Le widget **[!UICONTROL Destinations récemment créées]** vous permet d’afficher la liste des destinations configurées les plus récemment par votre organisation.

La date de création affichée correspond au dernier instantané pris dans la journée. En d’autres termes, si vous créez une nouvelle destination, elle n’apparaîtra sur la liste que lorsque le prochain instantané sera pris.

Sélectionner le nom d’une destination dans la liste affichée sur le widget vous donne accès aux détails de la destination qui sont liés depuis l’onglet **[!UICONTROL Parcourir]**. Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder à l’onglet **[!UICONTROL Parcourir]** et sélectionner le nom d’une destination pour en afficher les détails.

Pour en savoir plus sur la configuration de types de destinations spécifiques, consultez la page [Documentation sur les destinations](../../destinations/home.md).

![L’onglet Aperçu du tableau de bord des destinations avec le widget des destinations récemment créées en surbrillance.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Audiences récemment activées] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Audiences récemment activées"
>abstract="Ce widget fournit une liste des audiences qui ont été les plus récemment mappées à une destination. Cette liste fournit une capture instantanée des audiences et des destinations utilisées activement dans le système et peut aider à corriger les mappages erronés."

Le **[!UICONTROL Audiences récemment activées]** fournit une liste des audiences mappées le plus récemment à une destination. Cette liste fournit une capture instantanée des audiences et des destinations utilisées activement dans le système et peut aider à corriger les mappages erronés.

Le [!UICONTROL Mise à jour] La date affichée affiche la dernière fois que l’audience a été activée vers la destination et est exacte par rapport au dernier instantané quotidien. En d’autres termes, si vous activez une audience vers la destination, la date mise à jour ne changera pas tant que l’instantané suivant n’aura pas été pris.

La sélection du nom d’une audience dans la liste affichée sur le widget vous permet d’accéder aux détails de l’audience. Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder au [!UICONTROL Audiences] [!UICONTROL Parcourir] puis sélectionnez le nom d’une audience pour en afficher les détails.

Pour plus d’informations sur l’utilisation des audiences dans Experience Platform, reportez-vous à la section [Présentation de Segmentation Service](../../segmentation/home.md).

![L’onglet Aperçu du tableau de bord Destinations avec le widget Audiences récemment activées en surbrillance.](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL Audiences récemment activées par destination] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Audiences récemment activées par destination"
>abstract="Ce widget affiche les cinq audiences les plus récemment activées par ordre décroissant en fonction de la destination choisie dans le menu déroulant de la vue d’ensemble."

Le **[!UICONTROL Audiences récemment activées par destination]** widget affiche les cinq dernières audiences activées dans l’ordre décroissant en fonction de la destination choisie dans la liste déroulante d’aperçu. Elle est similaire au [!UICONTROL Audiences récemment activées] widget, mais les données affichées **only** s’applique à la destination sélectionnée.

Ce widget contient deux mesures : le nom et la date de la dernière activation des audiences vers la destination. Les données affichées sont correctes selon le dernier instantané quotidien.

Vous pouvez afficher les détails d’une audience en sélectionnant son nom dans la liste affichée.

![Le widget Audiences récemment activées par destination .](../images/destinations/recently-activated-audiences-by-destination.png)

Consultez la section Conditions préalables pour [définitions des termes utilisés](#prerequisites) dans cette description.

### [!UICONTROL Tendance de la taille de l’audience] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Tendance de la taille de l’audience"
>abstract="Ce widget indique le nombre de profils contenus dans l’audience qui est envoyée quotidiennement au compte de destination. Le premier menu déroulant adapte la période à la tendance de l’audience. Le deuxième menu déroulant du widget sélectionne l’audience à analyser. La destination est choisie dans la liste déroulante de l’aperçu."

Le **[!UICONTROL Tendance de la taille de l’audience]** Le widget illustre la relation entre le nombre de profils sur une période donnée pour une audience qui a été mappée à ce compte de destination. Le widget utilise un graphique linéaire pour illustrer le nombre de profils contenus dans l’audience, qui sont envoyés quotidiennement au compte de destination.

A l’aide du premier menu déroulant, une période peut être ajustée pour la tendance de l’audience des 30 derniers jours, 90 jours ou 12 mois.

Le deuxième menu déroulant répertorie chaque audience disponible qui peut être envoyée au compte de destination choisi en haut du tableau de bord.

![Le widget Tendance de la taille d’audience.](../images/destinations/audience-size-trend.png)

Le widget **[!UICONTROL Tendance de la taille d’audience]** contient un bouton [!UICONTROL Légendes] en haut à droite du widget. Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques. Un modèle d’apprentissage automatique génère automatiquement des sous-titres pour décrire les tendances clés et les événements importants en analysant le graphique et les données d’audience.

![La boîte de dialogue de légendes automatique pour le widget Tendance de la taille d’audience.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Audiences non mappées par identité] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Audiences non mappées par identité"
>abstract="Ce widget répertorie les cinq premières audiences **non mappées** classées par nombre d’identités décroissant pour une destination et une identité données. Les identifiants de filtre répertoriés dans la liste déroulante du widget changent en fonction du compte de destination sélectionné en haut de la page d’aperçu."

Le **[!UICONTROL Audiences non mappées par identité]** Le widget répertorie les cinq premiers **non mappé** les audiences classées par nombre d’identités décroissant pour une destination et une identité données. Il met en évidence les audiences qui sont les plus avantageuses à mapper au compte de destination choisi en fonction de l’identifiant choisi.

La liste déroulante Identifiant de destination filtre vos audiences disponibles. Les identifiants de filtre répertoriés dans la liste déroulante changent en fonction du compte de destination sélectionné en haut de la page d’aperçu.

La colonne Identités comptabilise le nombre d’identifiants source dans l’audience qui peuvent correspondre à l’identifiant choisi dans la liste déroulante Identifiant du widget.

![Le widget Audiences non mappées par identité .](../images/destinations/unmapped-audiences-by-identity.png)

Consultez la section Conditions préalables pour [définitions des termes utilisés](#prerequisites) dans cette description.

### [!UICONTROL Audiences mappées par identité] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Audiences mappées par identité"
>abstract="Ce widget fournit une liste des cinq premières audiences **mappées**. La liste est classée de haut en bas en fonction du nombre d’identifiants sources contenus dans les audiences. L’identifiant de destination à comptabiliser est sélectionné dans le menu déroulant sous le titre du widget. Les identifiants de destination disponibles dans la liste déroulante du widget dépendent de la destination choisie en haut du tableau de bord de la présentation."

Ce widget fournit une liste des cinq premières audiences **mappées**. La liste est classée de haut en bas en fonction du nombre d’identifiants sources contenus dans les audiences. L’identifiant de destination à comptabiliser est sélectionné dans le menu déroulant sous le titre du widget. Les identifiants de destination disponibles dans la liste déroulante du widget changent en fonction du filtre du compte de destination sélectionné en haut du tableau de bord de la présentation.

![Le widget Audiences mappées par identité .](../images/destinations/mapped-audiences-by-identity.png)

Le **[!UICONTROL Audiences mappées par identité]** le widget met en évidence en un coup d’oeil la probabilité de réussir le ciblage des opportunités de profil pour une campagne au sein de la destination choisie. Une campagne ciblée efficace ne dépend pas du nombre de profils envoyés à la destination, mais plutôt du nombre d’identifiants sources qui sont susceptibles d’être associés aux identifiants de destination pour fournir des données utiles et activables.

### Audiences courantes {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Audiences courantes"
>abstract="Ce widget fournit une liste des cinq premières audiences activées sur le compte de destination choisi en haut de la page, ainsi que la destination sélectionnée dans la liste déroulante du widget. La liste d’audiences est classée en fonction de leur date d’activation récente. L’audience la plus récemment activée s’affiche en haut."

Le **[!UICONTROL Audiences courantes]** fournit une liste des cinq premières audiences activées sur le compte de destination choisi en haut de la page, ainsi que la destination sélectionnée dans la liste déroulante du widget. La liste d’audiences est classée en fonction de leur date d’activation récente. L’audience la plus récemment activée s’affiche en haut.

Le [!UICONTROL TAILLE DE L’AUDIENCE] indique le nombre total de profils de chaque audience répertoriée.

![Le widget Audiences courantes.](../images/destinations/common-audiences.png)

### Audiences mappées {#mapped-audiences}

Le widget [!UICONTROL Audiences mappées] affiche le nombre total d’audiences mappées qui peuvent être activées vers la destination sélectionnée en haut de la page.

Sélectionner **[!UICONTROL Audiences]** pour accéder au tableau de bord Audiences [!UICONTROL Parcourir] . Cet espace de travail affiche une liste de toutes les définitions de segment pour votre organisation.

![Le widget Audiences mappées.](../images/destinations/mapped-audiences.png)

### Intégrité de l’audience mappée {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Intégrité de l’audience mappée"
>abstract="Ce widget fournit une liste de 20 audiences mappées au maximum dont le nombre total de profils s’écarte d’un facteur d’au moins un écart-type par rapport à la taille moyenne de l’audience de 30 jours mappée à cette destination. Il fournit une mesure calculée pour la dispersion des tailles d’audience par rapport à la moyenne au cours des 30 derniers jours. Les tailles d’audience sont triées de haut en bas."

Le widget fournit une liste de 20 audiences mappées au maximum dont le nombre total de profils, à partir du dernier instantané quotidien, s’écarte d’un facteur d’écart type au moins par rapport à la taille moyenne d’audience de 30 jours mappée à cette destination.

En résumé, il fournit une mesure calculée pour la dispersion des tailles d’audience par rapport à la moyenne au cours des 30 derniers jours. Il compare la taille actuelle de l’audience en dehors de l’écart-type historique observé dans les données au cours des 30 derniers jours.

Toutes les tailles d’audience du système sont triées de la gande taille à la petite taille, comme indiqué dans la colonne [!UICONTROL DERNIÈRE TAILLE].

Si le nombre de profils d’audience mappés ne correspond pas à l’écart-type par rapport à la taille de profil mappée moyenne au cours des 30 derniers jours, cela indique une anomalie du système et doit être étudié.

Si une audience dans la variable [!UICONTROL Santé de l’audience mappée] vous devez vous reporter au graphique de tendance de la taille de l’audience et localiser l’audience anormale. La tendance peut fournir des informations supplémentaires sur l’état de santé de votre audience.

>[!NOTE]
>
>La taille par défaut du widget d’intégrité de l’audience mappée peut bloquer les informations du tableau. Modifiez la taille du widget pour améliorer la lisibilité de vos noms d’audience et titres de colonnes mappés. Pour plus d’informations sur la modification des tableaux de bord, reportez-vous à la documentation sur le [redimensionnement d’un widget](../customize/modify.md).

![Le widget Intégrité de l’audience mappée.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Nombre de destinations] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Nombre de destinations"
>abstract="Ce widget fournit le nombre total de points d’entrée disponibles où une audience peut être activée et diffusée dans le système. Ce nombre inclut les destinations actives et inactives."

Le widget [!UICONTROL Nombre de destinations] fournit le nombre total de points d’entrée disponibles où une audience peut être activée et diffusée dans le système. Ce nombre inclut les destinations actives et inactives.

Sous le nombre total, sélectionnez **[!UICONTROL Destinations]** pour accéder à l’onglet de navigation des destinations. Cette page répertorie toutes les destinations avec lesquelles vous avez établi une connexion à ce jour.

![Le widget Nombre de destinations.](../images/destinations/destinations-count.png)

### [!UICONTROL Statut de destination] {#destination-status}

Le widget [!UICONTROL Statut de destination] affiche le nombre total de destinations activées sous la forme d’une mesure unique et utilise un graphique en anneau pour illustrer la différence proportionnelle entre les destinations activées et désactivées.

Les décomptes individuels des destinations activées ou désactivées s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Le widget Statut de destination.](../images/destinations/destination-status.png)

### [!UICONTROL Destinations actives par plateforme de destination] {#active-destinations-by-destination-platform}

Ce widget utilise un tableau à deux colonnes pour afficher la liste des plateformes de destination actives et le nombre total de destinations actives pour chaque plateforme de destination. La liste des plateformes de destination est classée de haut en bas.

![Le widget Destinations actives par plateforme de destination.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Audiences activées sur toutes les destinations] {#activated-audiences-across-all-destinations}

Le widget [!UICONTROL Audiences activées sur toutes les destinations] fournit le nombre total d’audiences activées sur toutes les destinations dans une seule mesure. Ce nombre correspond à l’instantané le plus récent.

![Le widget Audiences activées dans toutes les destinations.](../images/destinations/activated-audiences-across-all-destinations.png)

Sélectionnez **[!UICONTROL Audiences]** pour accéder à l’onglet [!UICONTROL Parcourir] des destinations. Cette page fournit une liste de toutes les destinations activées, ainsi que diverses mesures pertinentes. Consultez la documentation pour en savoir plus sur l’onglet [[!UICONTROL Parcourir]](../../destinations/ui/destinations-workspace.md#browse).

Consultez la section Conditions préalables pour [définitions des termes utilisés](#prerequisites) dans cette description.

### [!UICONTROL Audiences activées] {#activated-audiences}

Ce widget fournit une mesure unique pour le nombre total d’audiences activées vers une destination.

![Le widget Audiences activées.](../images/destinations/activated-audiences.png)

Sélectionnez **[!UICONTROL Audiences]** pour accéder à la page de détails du tableau de bord des destinations. Le [!UICONTROL Données d’activation] affiche une liste des audiences qui ont été mappées à la destination, y compris leur date de début et de fin (le cas échéant), ainsi que d’autres informations pertinentes pour l’exportation des données, telles que le type d’exportation, la planification et la fréquence. Pour afficher les détails d’une audience spécifique, sélectionnez son nom dans la [!UICONTROL Nom de l’audience] colonne .

![La page de détails du tableau de bord des destinations avec l’onglet Données d’activation en surbrillance.](../images/destinations/activation-data-tab.png)

Ce widget vous aide à comprendre en un coup d’œil la valeur de vos destinations en fonction du nombre d’audiences activées. Il permet également d’accéder facilement à des informations plus détaillées pour une analyse plus approfondie.

Consultez la section Conditions préalables pour [définitions des termes utilisés](#prerequisites) dans cette description.

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord des destinations et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des destinations dans Experience Platform, reportez-vous à la [documentation sur les destinations](../../destinations/home.md).
