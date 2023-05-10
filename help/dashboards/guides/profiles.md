---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord Profil;tableau de bord
title: Guide du tableau de bord Profils
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les données Real-time Customer Profile de votre entreprise.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: a28c1c00fd0b33af3b797ecf2b4d45154dedc823
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 92%

---

# Tableau de bord des [!UICONTROL profils]

L’interface utilisateur d’Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos données [!DNL Real-Time Customer Profile], présentées ainsi lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord Profils et l’utiliser dans l’interface utilisateur. Il fournit également des informations sur les mesures affichées dans le tableau de bord.

Pour une présentation de toutes les fonctionnalités de profil de l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Real-Time Customer Profile](../../profile/ui/user-guide.md).

## Données du tableau de bord Profils

Le tableau de bord Profils affiche un instantané des données d’attribut (d’enregistrement) dont votre entreprise dispose dans la banque de profils d’Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En dʼautres termes, lʼinstantané nʼest pas une approximation ou un exemple des données, et le tableau de bord Profils n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorer le tableau de bord Profils

Pour accéder au tableau de bord Profils dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre organisation débute avec Platform et ne dispose pas encore de jeux de données ou de politiques de fusion de profil actifs, le tableau de bord Profils n’est pas visible. Au lieu de cela, la variable [!UICONTROL Présentation] Cet onglet affiche des liens et de la documentation pour vous aider à prendre en main Real-time Customer Profile.

![Le tableau de bord Profils Experience Platform avec les options Profils et Aperçu en surbrillance.](../images/profiles/dashboard-overview.png)

### Modifier le tableau de bord Profils

Vous pouvez modifier l’aspect du tableau de bord Profils en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord, ainsi que d’accéder à la **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la documentation sur la [modification des tableaux de bord](../customize/modify.md) et à la [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

### Ajouter des widgets {#add-widget}

Sélectionnez **[!UICONTROL Ajouter un widget]** pour accéder à la bibliothèque de widgets et voir la liste des widgets disponibles à ajouter à votre tableau de bord.

![La présentation du tableau de bord Profils avec Ajouter un widget mis en surbrillance.](../images/profiles/profiles-overview-add-widget.png)

Dans la bibliothèque de widgets, vous pouvez parcourir la sélection de widgets de segment standards et personnalisés. Pour plus d’informations sur l’ajout de widgets, consultez la documentation sur la bibliothèque de widgets concernant la manière d’[ajouter un widget](../customize/widget-library.md#add-widgets).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Parcourir les profils {#browse-profiles}

L’onglet [!UICONTROL Parcourir] vous permet de rechercher et d’afficher les profils en lecture seule ingérés dans votre organisation. Vous y trouverez des informations importantes appartenant au profil concernant leurs préférences, les événements passés, les interactions et les segments.

Pour en savoir plus sur les fonctionnalités d’affichage des profils fournies dans l’interface utilisateur de Platform, consultez la documentation sur la [navigation dans les profils dans Adobe Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Politiques de fusion {#merge-policies}

Les mesures affichées dans le tableau de bord Profils reposent sur les stratégies de fusion appliquées à vos données Real-Time Customer Profile. Lorsque des données sont rassemblées à partir de plusieurs sources pour créer le profil client, les données peuvent contenir des valeurs en conflit. Par exemple, un jeu de données peut désigner un(e) client(e) comme « célibataire » tandis qu’un autre jeu de données peut désigner le/la client(e) comme « marié(e) ». La tâche de la politique de fusion consiste à déterminer les données à prioriser et à afficher dans le cadre du profil.

Pour plus d’informations sur les politiques de fusion, notamment sur la création, la modification et la déclaration d’une politique de fusion par défaut pour votre organisation, reportez-vous à la [présentation des politiques de fusion](../../profile/merge-policies/overview.md).

Le tableau de bord sélectionne automatiquement une politique de fusion à utiliser. La politique de fusion appliquée peut être modifiée à l’aide du menu déroulant à côté du nom de la politique de fusion.

>[!NOTE]
>
>Le menu déroulant affiche uniquement les politiques de fusion qui utilisent le schéma `_xdm.context.profile`. Cependant, si votre organisation a créé plusieurs politiques de fusion, vous devrez peut-être faire défiler la liste complète des politiques de fusion disponibles.

![Onglet Aperçu des profils avec le menu déroulant Politique de fusion en surbrillance.](../images/profiles/select-merge-policy.png)

## Schémas d’union

Le tableau de bord [!UICONTROL Schéma d’union] affiche le schéma d’union pour une classe XDM spécifique. En sélectionnant la liste déroulante **[!UICONTROL Classe]**, vous pouvez afficher les schémas d’union pour différentes classes XDM.

Les schémas d’union sont composés de plusieurs schémas qui partagent la même classe et qui ont été activés pour Profile. Ils vous permettent de voir en une seule vue, une fusion de chaque champ contenu dans chaque schéma qui partage la même classe.

Consultez le guide de l’interface utilisateur du schéma d’union pour en savoir plus sur l’[affichage des schémas d’union dans l’interface utilisateur de Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets et mesures

Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur vos données de profil.

La date et l’heure de l’instantané le plus récent s’affichent en haut de l’onglet [!UICONTROL Présentation] à côté de la liste déroulante Politique de fusion. Toutes les données du widget sont exactes à cette date et cette heure. La date et l’heure de l’instantané sont fournies en UTC ; elles ne se trouvent pas dans le fuseau horaire de l’utilisateur/utilisatrice ou de l’organisation.

![Onglet Aperçu du tableau de bord Profils avec la date et l’heure de l’instantané le plus récent en surbrillance.](../images/profiles/snapshot-timestamp.png)

## Widgets standard {#standard-widgets}

Adobe fournit plusieurs widgets standards que vous pouvez utiliser pour visualiser différentes mesures liées à vos données de profil. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la [!UICONTROL Bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire la [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

Pour en savoir plus sur chacun des widgets standards disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Nombre de profils]](#profile-count)
* [[!UICONTROL Tendance du nombre de profils]](#profile-count-trend)
* [[!UICONTROL Modification du nombre de profils]](#profile-count-change)
* [[!UICONTROL Tendance de modification du nombre de profils]](#profiles-count-change-trend)
* [[!UICONTROL Tendance de modification du nombre de profils par d’identité]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Profils par identité]](#profiles-by-identity)
* [[!UICONTROL Chevauchement des identités]](#identity-overlap)
* [[!UICONTROL Profils à identité unique]](#single-identity-profiles)
* [[!UICONTROL Profils à identité unique par identité]](#single-identity-profiles-by-identity)
* [[!UICONTROL Profils non segmentés]](#unsegmented-profiles)
* [[!UICONTROL Les profils non segmentés changent de tendance]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Profils non segmentés par identité]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Audiences]](#audiences)
* [[!UICONTROL Audiences mappées au statut de destination]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Taille des audiences]](#audiences-size)
* [[!UICONTROL Chevauchements d’audience par politique de fusion]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Rapport de chevauchement d’audience]](#audience-overlap-report)

### [!UICONTROL Nombre de profils] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Nombre de profils"
>abstract="Ce widget affiche le nombre total de profils fusionnés dans la banque de profils au moment où l’instantané a été pris. Le nombre dépend de la politique de fusion sélectionnée appliquée à vos données de profil."

Le widget **[!UICONTROL Nombre de profils]** affiche le nombre total de profils fusionnés dans la banque de profils au moment où l’instantané a été pris. Ce nombre est le résultat de l’application de la politique de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Pour en savoir plus, consultez la [section sur les politiques de fusion plus haut dans ce document](#merge-policies).

>[!NOTE]
>
>Le widget [!UICONTROL Nombre de profils] peut afficher un nombre différent du nombre de profils affiché dans l’onglet [!UICONTROL Parcourir] dans la section [!UICONTROL Profils] de l’interface utilisateur pour plusieurs raisons. La raison la plus courante est que l’onglet [!UICONTROL Parcourir] référence le nombre total de profils fusionnés en fonction de la politique de fusion par défaut de votre organisation, tandis que le widget [!UICONTROL Nombre de profils] référence le nombre total de profils fusionnés en fonction de la politique de fusion que vous avez sélectionnée pour afficher dans le tableau de bord.
>
>Une autre raison courante est due aux différences entre le moment où l’instantané du tableau de bord est pris et le moment où l’exemple de tâche est exécuté pour l’onglet [!UICONTROL Parcourir]. Vous pouvez voir quand le widget [!UICONTROL Nombre de profils] a été mis à jour pour la dernière fois en regardant la date et l’heure sur le widget. Pour en savoir plus sur la manière dont l’exemple de tâche est déclenché sur la page [!UICONTROL Parcourir] , voir [section sur le nombre de profils dans le guide de l’interface utilisateur de Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=fr#profile-count).

![Le tableau de bord Profils Experience Platform avec le widget Nombre de profils mis en surbrillance.](../images/profiles/profile-count.png)

### [!UICONTROL Tendance du nombre de profils] {#profile-count-trend}

Le widget [!UICONTROL Tendance du nombre de profils] utilise un graphique linéaire pour illustrer la tendance du nombre total de profils contenus dans le système au fil du temps. Ce nombre total inclut tous les profils importés dans le système depuis le dernier instantané quotidien. Les données peuvent être consultées sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget.

![Le widget Tendance du nombre de profils.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Modification du nombre de profils] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Modification du nombre de profils"
>abstract="Ce widget affiche le nombre total de profils fusionnés **ajoutés** à la banque de profils au moment du dernier instantané. Le nombre dépend de la politique de fusion sélectionnée appliquée à vos données de profil."

Le widget **[!UICONTROL Modification du nombre de profils]** affiche le nombre de profils fusionnés ajoutés à la banque de profils depuis l’instantané précédent. Ce nombre est le résultat de l’application de la politique de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu. Vous pouvez utiliser le sélecteur de liste déroulante pour afficher le nombre de profils ajoutés au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois.

>[!NOTE]
>
>Le widget [!UICONTROL Modification du nombre de profils] reflète le nombre de profils ajoutés **après** la configuration initiale de l’ingestion des profils et de la banque de profils. En d’autres termes, si votre organisation a configuré la banque de profils et ingéré 4 000 000 profils au jour 1, le tableau de bord sera disponible dans les 24 heures, mais le widget [!UICONTROL Modification du nombre de profils] sera défini sur 0. Cela permet d’éviter un pic associé à l’ingestion initiale des profils dans le système. Au cours des 30 prochains jours, votre organisation ingèrera 1 000 000 profils supplémentaires dans la banque de profils. Une fois l’instantané suivant pris, le widget [!UICONTROL Modification du nombre de profils] affiche un total de 1 000 000 profils ajoutés, tandis que le widget [!UICONTROL Nombre de profils] affiche un total de 5 000 000 profils.

![Le tableau de bord Profils de l’interface utilisateur de Platform avec le widget Modification du nombre de profils mis en surbrillance.](../images/profiles/profile-count-change.png)

### [!UICONTROL Tendance de modification du nombre de profils] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Tendance de modification du nombre de profils"
>abstract="Ce widget affiche le nombre de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois. Le nombre dépend également de la politique de fusion sélectionnée appliquée à vos données de profil."

Le widget **[!UICONTROL Tendance de modification du nombre de profils]** affiche le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois. Ce nombre est mis à jour chaque jour lorsque l’instantané est pris. Par conséquent, si vous deviez ingérer des profils dans Platform, le nombre de profils ne serait pas reflété tant que l’instantané suivant n’aurait pas été pris. Le nombre de profils ajoutés est le résultat de l’application de la politique de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Pour en savoir plus, consultez la [section sur les politiques de fusion plus haut dans ce document](#merge-policies).

Le widget **[!UICONTROL Tendance de modification du nombre de profils]** affiche un bouton « légendes » en haut à droite du widget. Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques.

![L’onglet Aperçu du profil affiche le widget Tendance de modification du nombre de profils avec le bouton Légendes en surbrillance.](../images/profiles/profiles-count-change-trend-captions.png)

Un modèle de machine learning génère automatiquement des légendes pour décrire les tendances clés et les événements importants en analysant le graphique et les données. Les annotations sont ajoutées au graphique en fonction des légendes. Sélectionnez une légende pour mettre l’accent sur l’annotation correspondante.

![La boîte de dialogue de légendes automatiques du widget Tendance de modification de nombre de profils.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Tendance de modification du nombre de profils par identité] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Ce widget filtre le nombre de profils en fonction d’une identité source sélectionnée et d’une politique de fusion, puis illustre la modification du nombre pour diverses périodes à l’aide d’un graphique linéaire. La politique de fusion est sélectionnée dans la liste déroulante d’aperçu située en haut de la page. L’identité source et la période sont sélectionnées dans les menus déroulants du widget. La tendance peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois.

Ce widget vous permet de gérer vos besoins d’activation de destination en présentant le modèle de croissance des profils filtrés selon l’identité requise.

![Le widget Tendance de modification du nombre de profils par identité.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profils par identité"
>abstract="Ce widget affiche la répartition de tous les profils fusionnés dans votre banque de profils par identités."

Le widget **[!UICONTROL Profils par identité]** affiche la répartition des identités pour tous les profils fusionnés de votre banque de profils. Le nombre total de profils par identité (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent être associés à un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

Pour en savoir plus, consultez la [section sur les politiques de fusion plus haut dans ce document](#merge-policies).

![Le tableau de bord d’aperçu des profils avec le widget Profils par identité mis en surbrillance.](../images/profiles/profiles-by-identity.png)

Sélectionnez **[!UICONTROL Légendes]** pour ouvrir la boîte de dialogue des légendes automatiques.

![La boîte de dialogue des légendes des profils par identité.](../images/profiles/profiles-by-identity-captions.png)

Un modèle de machine learning génère automatiquement des informations sur les données en analysant la distribution globale et les dimensions clés des données.

Pour en savoir plus sur les identités, consultez la [documentation du Service d’identités Adobe Experience Platform](../../identity-service/home.md).

### [!UICONTROL Chevauchement des identités] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Chevauchement des identités"
>abstract="Ce widget utilise un diagramme de Venn pour afficher le chevauchement des profils de votre banque de profils qui contiennent les deux identités sélectionnées."

Le widget **[!UICONTROL Chevauchement des identités]** utilise un diagramme de Venn, ou un diagramme logique, pour afficher le chevauchement des profils de votre banque de profils qui contiennent les deux identités sélectionnées.

Utilisez les menus déroulants du widget pour sélectionner les identités à comparer. Les cercles affichent le nombre total relatif de profils qui contiennent chaque identité. Le nombre de profils contenant les deux identités est représenté par la taille du chevauchement entre les cercles. Si un(e) client(e) interagit avec votre marque sur plusieurs canaux, plusieurs identités seront associées à ce(tte) client(e) individuel(le). Par conséquent, il est probable que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour plus d&#39;informations sur les fragments de profil, reportez-vous à la section sur [fragments de profil par rapport aux profils fusionnés](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=fr#profile-fragments-vs-merged-profiles) dans la présentation de Real-time Customer Profile.

Pour en savoir plus sur les identités, consultez la [documentation du Service d’identités Adobe Experience Platform](../../identity-service/home.md).

![Le tableau de bord Profils présente un aperçu du widget de chevauchement des identités mis en surbrillance.](../images/profiles/identity-overlap.png)

### [!UICONTROL Profils à identité unique] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Profils à identité unique"
>abstract="Ce widget fournit le nombre de profils de votre organisation qui n’ont qu’un seul type d’identifiant qui crée leur identité. Ce type d’identifiant peut être une adresse e-mail ou un ECID."

Le widget [!UICONTROL Profils à identité unique] fournit un nombre des profils de votre organisation qui ne disposent que d’un seul type d’identifiant qui crée leur identité. Ce type d’identifiant peut être une adresse e-mail ou un ECID. Le nombre de profils est généré à partir des données contenues dans l’instantané le plus récent.

![Widget Profils d’identité unique.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Profils d’identité unique par identité] {#single-identity-profiles-by-identity}

Ce widget utilise un graphique à barres pour illustrer le nombre total de profils qui sont identifiés à l’aide d’un identifiant unique. Le widget prend en charge jusqu’à cinq des identités les plus courantes.

Pointez sur des barres individuelles pour afficher une boîte de dialogue détaillant le nombre total de profils pour une identité.

![Widget Profils d’identité unique par identité.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Profils non segmentés] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Profils non segmentés"
>abstract="Ce widget fournit le nombre total de profils qui ne sont associés à aucun segment et représente l’opportunité d’activation des profils à l’échelle de votre organisation."

Le widget [!UICONTROL Profils non segmentés] fournit le nombre total de profils qui ne sont associés à aucun segment. Le nombre, généré à partir du dernier instantané, est précis et souligne l’opportunité d’activation de profils dans votre entreprise. Il indique également la possibilité d’effacer les profils qui ne fournissent pas un retour sur investissement adéquat.

![Widget Profils non segmentés.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Les profils non segmentés changent de tendance] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Tendance des profils non segmentés"
>abstract="Ce widget fournit une représentation graphique linéaire du nombre de profils qui ne sont associés à aucun segment sur une période donnée. La tendance des profils non associés à un segment peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois."

Le [!UICONTROL Les profils non segmentés changent de tendance] widget utilise un graphique linéaire pour illustrer le nombre de profils ajoutés depuis le dernier instantané quotidien qui ne sont associés à aucun segment. La tendance de changement des profils non associés à un segment peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. Le nombre de profils est reflété sur l’axe des ordonnées et la période sur l’axe des abscisses.

![Les profils non segmentés changent de widget de tendance.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Profils non segmentés par identité] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>Le widget Profils non segmentés par identité a été abandonné en octobre 2022 et n’est plus disponible.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Audiences] {#audiences}

Ce widget fournit le nombre total de segments prêts à être activés, en fonction de la politique de fusion choisie appliquée aux données de votre profil.

Sélectionnez **[!UICONTROL Audiences]** pour accéder à l’onglet [!UICONTROL Parcourir] du tableau de bord [!UICONTROL Segments]. De là, vous pouvez voir une liste de toutes les définitions de segment pour votre organisation.

![Widget Audiences.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Rapport de chevauchement des audiences] {#audience-overlap-report}

Ce widget tabularise les données de chevauchement des audiences de tous les segments disponibles filtrés par politique de fusion. Une liste de cinq audiences classées du pourcentage de chevauchement le plus élevé au plus faible est fournie pour la politique de fusion choisie dans le menu déroulant en haut de l’écran. Les deux segments analysés sont répertoriés dans les colonnes [!UICONTROL NOM DU SEGMENT A] et [!UICONTROL NOM DU SEGMENT B]. Le chevauchement en pourcentage est fourni dans la troisième colonne avec une précision de douze décimales.

Le rapport sur le chevauchement des audiences vous permet de créer de nouveaux segments hautement performants. L’observation des chevauchements au pourcentage élevé vous permet de supprimer des audiences et d’empêcher l’envoi d’une même audience vers différentes destinations. Elle vous aide également à identifier les informations cachées qui peuvent contribuer à une meilleure segmentation. Un chevauchement au pourcentage faible permet de localiser les profils uniques à rechercher.

Sélectionnez **[!UICONTROL Afficher plus]** pour ouvrir une boîte de dialogue plein écran contenant davantage de données de chevauchement des audiences.

![Le widget Rapport de chevauchement des audiences avec l’option Afficher plus en surbrillance.](../images/profiles/profiles-audience-overlap-report.png)

La boîte de dialogue [!UICONTROL Rapport de chevauchement des audiences] s’affiche. Cette boîte de dialogue peut contenir jusqu’à 50 lignes d’analyses de chevauchement des audiences, divisées en six colonnes. Sélectionnez l’icône des paramètres (![Icône des paramètres.](../images/profiles/settings-icon.png)) pour supprimer ou ajouter des colonnes du tableau.

![Boîte de dialogue Rapport de chevauchement des audiences.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Sélectionnez l’en-tête de colonne **[!UICONTROL Chevauchement]** pour modifier le classement des résultats, du plus haut au plus bas ou du plus bas au plus haut.

Pour télécharger l’intégralité du rapport au format PDF, sélectionnez le menu d’options (**`...`**), puis **[!UICONTROL Télécharger]**.

![La boîte de dialogue Rapport de chevauchement des audiences avec les points de suspension et l’option de téléchargement en surbrillance.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Sélectionnez une ligne dans le rapport pour ouvrir un diagramme de Venn de l’analyse de chevauchement. Passez la souris sur une section du diagramme de Venn pour afficher le nombre de profils dans une boîte de dialogue.

![La boîte de dialogue Rapport de chevauchement des audiences avec un diagramme de Venn et une ligne en surbrillance.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Sélectionnez **[!UICONTROL Fermer]** pour revenir au tableau de bord des [!UICONTROL Profils].

### [!UICONTROL Audiences mappées au statut de destination] {#audiences-mapped-to-destination-status}

Le widget [!UICONTROL Audiences mappées au statut de destination] affiche le nombre total d’audiences mappées et non mappées dans une seule mesure et utilise un graphique en anneau pour illustrer la différence proportionnelle entre les totaux. Les nombres calculés dépendent de la politique de fusion choisie.

Les nombres individuels des audiences mappées ou non mappées s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Le widget Audiences mappées au statut de destination.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Taille des audiences] {#audiences-size}

Le widget [!UICONTROL Taille des audiences] fournit un tableau à deux colonnes qui répertorie jusqu’à 20 segments et le nombre total d’audiences contenues dans chaque segment. La liste est classée en fonction du nombre total d’audiences, du plus élevé au plus bas. Le nombre total de tailles d’audience dépend de la politique de fusion appliquée.

![Le widget Taille des audiences.](../images/profiles/audiences-size.png)

Pour afficher des informations complètes sur un segment, sélectionnez un nom de segment dans la liste fournie pour accéder à la page [!UICONTROL Détail] des [!UICONTROL Segments]. En outre, en sélectionnant **[!UICONTROL Afficher tous les segments]** à partir de la fin du widget, vous pouvez accéder à l’onglet [!UICONTROL Parcourir] des [!UICONTROL Segments] pour rechercher un segment existant.

![Le widget Taille des audiences avec un nom de segment et Afficher le texte de tous les segments en surbrillance.](../images/profiles/audiences-size-view-all-segments.png)

Consultez la documentation pour plus d’informations sur l’onglet [!UICONTROL  Parcourir] des [[!UICONTROL Segments] ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=fr#browse).

### [!UICONTROL Chevauchements d’audience par politique de fusion] {#audience-overlap-by-merge-policy}

Ce widget utilise un diagramme de Venn pour afficher le chevauchement de deux segments sélectionnés. La politique de fusion est sélectionnée dans la liste déroulante d’aperçu située en haut de la page et les segments à analyser sont sélectionnés dans deux menus déroulants du widget. Le nombre total de profils contenus dans la définition de segment pertinente peut être affiché en passant la souris sur un cercle ou l’intersection.

Ce widget affiche le croisement visuel des définitions de segment et vous permet d’optimiser la politique de segmentation en étudiant les similitudes entre les définitions de segment.

![Le tableau de bord Profils de l’interface utilisateur de Platform avec la liste déroulante Politique de fusion et les menus déroulants de segment du widget en surbrillance.](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord des profils et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation de [!DNL Profile] données de l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Real-Time Customer Profile](../../profile/ui/user-guide.md).
