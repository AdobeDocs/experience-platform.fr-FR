---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord Profil;tableau de bord
title: Tableau de bord des profils
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les données du profil client en temps réel de votre organisation.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '5005'
ht-degree: 43%

---

# Tableau de bord des [!UICONTROL profils]

L’interface utilisateur d’Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos données [!DNL Real-Time Customer Profile], présentées ainsi lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord Profils et l’utiliser dans l’interface utilisateur. Il fournit également des informations sur les mesures affichées dans le tableau de bord.

Reportez-vous au [Guide de l’interface utilisateur du profil client en temps réel](../../profile/ui/user-guide.md) pour une présentation des fonctionnalités de profil de l’interface utilisateur d’Experience Platform.

## Données du tableau de bord Profils

Le tableau de bord Profils affiche un instantané des données d’attribut (enregistrement) dont dispose votre organisation dans la banque de profils d’Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En dʼautres termes, lʼinstantané nʼest pas une approximation ou un exemple des données, et le tableau de bord Profils n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorer le tableau de bord des profils {#explore-dashboard}

Pour accéder au tableau de bord Profils dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Profils]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre organisation débute avec Experience Platform et n’a pas encore de jeux de données ou de politiques de fusion de profils actifs, le tableau de bord Profils n’est pas visible. À la place, l’onglet [!UICONTROL Aperçu] affiche des liens et de la documentation pour vous aider à prendre en main le profil client en temps réel.

![Tableau de bord Profils Experience Platform avec Profils et Présentation en surbrillance.](../images/profiles/dashboard-overview.png)

### Modification du tableau de bord Profils {#modify-dashboard}

Vous pouvez modifier l’aspect du tableau de bord Profils en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Vous pouvez déplacer, ajouter, redimensionner et supprimer des widgets du tableau de bord, ainsi que pour accéder à la **[!UICONTROL Bibliothèque de widgets]** afin d’explorer les widgets disponibles et de créer des widgets personnalisés pour votre organisation.

Pour en savoir plus, consultez la documentation [modification des tableaux de bord](../customize/modify.md) et [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

### Ajouter des widgets {#add-widget}

Sélectionnez **[!UICONTROL Ajouter un widget]** pour accéder à la bibliothèque de widgets et voir la liste des widgets disponibles à ajouter à votre tableau de bord.

![La présentation du tableau de bord Profils avec Ajouter un widget mis en surbrillance.](../images/profiles/profiles-overview-add-widget.png)

Dans la bibliothèque de widgets, vous pouvez parcourir la sélection de widgets d’audience standard et personnalisés. Pour plus d’informations sur l’ajout de widgets, consultez la documentation de la bibliothèque de widgets sur la manière d’[ajouter un widget](../customize/widget-library.md#add-widgets).

### Afficher le SQL {#view-sql}

Vous pouvez afficher le code SQL qui génère les informations visualisées dans votre tableau de bord à l’aide du bouton (bascule) de l’espace de travail [!UICONTROL Présentation]. Vous pouvez vous inspirer du SQL de vos informations existantes pour créer de nouvelles requêtes qui obtiennent des informations uniques des données Experience Platform en fonction des besoins de votre entreprise. Pour en savoir plus sur cette fonctionnalité, consultez le guide de l’interface utilisateur [View SQL](../view-sql.md).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Parcourir les profils {#browse-profiles}

L’onglet [!UICONTROL Parcourir] vous permet de rechercher et d’afficher les profils en lecture seule ingérés dans votre organisation. Vous y trouverez des informations importantes appartenant au profil concernant leurs préférences, les événements passés, les interactions et les audiences.

## Détails du profil {#profile-details}

Pour ouvrir l’espace de travail [!UICONTROL Profils] [!UICONTROL Détail], sélectionnez un [!UICONTROL Identifiant de profil] dans la liste.

![Onglet Parcourir les profils avec un identifiant de profil mis en surbrillance.](../images/profiles/profile-id.png)

L’espace de travail [!UICONTROL Profils] [!UICONTROL Détail] affiche plusieurs widgets préconfigurés qui transmettent des informations spécifiques à ce profil. Ces informations vous permettent de comprendre les attributs clés du profil en un coup d’œil. Vous pouvez également personnaliser votre espace de travail [!UICONTROL Profils] [!UICONTROL Détail] en créant vos propres widgets. Pour plus d’informations, consultez la section sur [comment ajouter des widgets](#add-widgets).

![L’espace de travail [!UICONTROL Profils] [!UICONTROL Détail] avec l’onglet [!UICONTROL Détail] en surbrillance.](../images/profiles/profile-details-workspace.png)

### Widgets de détails de profil {#widgets}

Les widgets de détails de profil préconfigurés sont les suivants :

#### Profil client {#customer-profile}

Le widget [!UICONTROL Profil client] affiche le prénom et le nom de l’utilisateur associé au profil, ainsi que son [!UICONTROL Identifiant de profil]. Un identifiant de profil est un identifiant généré automatiquement associé à un type d’identité et représente un profil. Pour en savoir plus sur les identités et les espaces de noms d’identité, consultez [Présentation des identités](../../rtcdp/profile/identities-overview.md).

![Le widget Profil client.](../images/profiles/customer-profile.png)

#### Attributs de base {#basic-attributes}

Le widget [!UICONTROL Attributs de base] affiche les attributs les plus couramment utilisés pour définir un profil individuel.

![Le widget Attributs de base.](../images/profiles/basic-attributes.png)

#### Identités liées {#linked-identities}

Le widget [!UICONTROL Identités liées] affiche toutes les autres identités associées au profil.

Pour afficher les détails de l’identité du profil de manière plus approfondie et accéder à l’espace de travail [!UICONTROL Identités], sélectionnez **[!UICONTROL Afficher le graphique d’identité]**.

![Widget Identités liées.](../images/profiles/linked-identities.png)

#### Préférences de canaux {#channel-preferences}

Le widget [!UICONTROL Préférences de canal] affiche les canaux de communication depuis lesquels l’utilisateur a consenti à recevoir des communications. Une coche indique chaque canal depuis lequel l’utilisateur a consenti à recevoir des communications.

<!-- image needs a blue tick added below -->

![Widget Préférences de canal.](../images/profiles/channel-preferences.png)

Le consentement du client et les préférences de contact sont des sujets complexes. Pour découvrir comment les préférences de consentement et de contexte peuvent être collectées, traitées et filtrées dans Experience Platform, nous vous recommandons de lire les documents suivants :

* Pour en savoir plus sur les groupes de champs de schéma requis pour [collecter les données de consentement selon la norme Adobe](../../landing/governance-privacy-security/consent/adobe/overview.md), consultez la documentation sur ces groupes de champs de schéma activés pour Profile.
   * [[!UICONTROL Détails relatifs au consentement et aux préférences]](../../xdm/field-groups/profile/consents.md)
   * [[!UICONTROL IdentityMap]](../../xdm/field-groups/profile/identitymap.md) (obligatoire si vous utilisez Experience Platform Web ou Mobile SDK pour envoyer des signaux de consentement)
* Pour savoir comment traiter les données de consentement et de préférence des clients à l’aide de la norme Adobe, consultez la présentation sur le [traitement du consentement dans Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md).
* Une gouvernance des données et une politique de consentement combinées peuvent être utilisées pour filtrer les profils pour la segmentation en fonction de leurs préférences de consentement et de vos règles d’organisation établies. Pour savoir comment créer et utiliser ces politiques combinées, consultez le guide d’utilisation sur la [gestion des politiques d’utilisation des données](../../data-governance/policies/user-guide.md#combine-policies).

### Ajouter des widgets {#add-widgets}

Pour ajouter des widgets personnalisés à votre espace de travail [!UICONTROL Profils] [!UICONTROL Détails], sélectionnez **[!UICONTROL Personnaliser les détails du profil]**.

![Espace de travail Détails des profils avec l’option [!UICONTROL Personnaliser les détails du profil] mise en surbrillance.](../images/profiles/customize-profile-details.png)

Vous pouvez désormais modifier l’espace de travail en redimensionnant ou en déplaçant les widgets. Sélectionnez **[!UICONTROL Ajouter un widget]** pour créer un widget avec des attributs personnalisés.

![L’espace de travail Profils [!UICONTROL Détails] avec [!UICONTROL Ajouter un widget] mis en surbrillance.](../images/profiles/add-widget.png)

Le créateur du widget s’affiche. Saisissez un nom explicite pour votre widget dans le champ de texte [!UICONTROL Titre de la carte] et sélectionnez **[!UICONTROL Ajouter des attributs]**.

![Zone de travail du créateur du widget avec le champ [!UICONTROL Titre de la carte] et [!UICONTROL Ajouter des attributs] en surbrillance.](../images/profiles/widget-creator.png)

Une boîte de dialogue s’affiche, contenant une visualisation du schéma d’union du profil. Utilisez le champ de recherche ou faites défiler l’écran pour trouver les attributs pour lesquels vous souhaitez créer des rapports avec votre widget. Cochez la case correspondant aux attributs que vous souhaitez inclure. Sélectionnez **[!UICONTROL Sélectionner]** pour continuer le workflow de création.

>[!TIP]
>
>Une sélection de la case à cocher de niveau supérieur inclut tous les éléments enfants.

![Schéma d’union avec la case à cocher Attribut de fidélité et [!UICONTROL Sélectionner] mise en surbrillance.](../images/profiles/union-schema-attributes.png)

Un aperçu du widget terminé s’affiche sur la zone de travail. Une fois que vous êtes satisfait des attributs sélectionnés, sélectionnez **[!UICONTROL Enregistrer]** pour confirmer vos choix et revenir à l’espace de travail [!UICONTROL Profils] [!UICONTROL Détail]. Le widget que vous venez de créer est désormais visible dans l’espace de travail.

![Zone de travail du créateur de widgets avec Enregistrer mise en surbrillance et affichage de l’aperçu du widget.](../images/profiles/widget-preview.png)

## Politiques de fusion {#merge-policies}

Les mesures affichées dans le tableau de bord Profils reposent sur les politiques de fusion appliquées à vos données de profil client en temps réel. Lorsque des données sont rassemblées à partir de plusieurs sources pour créer le profil client, les données peuvent contenir des valeurs en conflit. Par exemple, un jeu de données peut désigner un(e) client(e) comme « célibataire » tandis qu’un autre jeu de données peut désigner le/la client(e) comme « marié(e) ». La tâche de la politique de fusion consiste à déterminer les données à prioriser et à afficher dans le cadre du profil.

Pour plus d’informations sur les politiques de fusion, notamment sur la création, la modification et la déclaration d’une politique de fusion par défaut pour votre organisation, reportez-vous à la [présentation des politiques de fusion](../../profile/merge-policies/overview.md).

Le tableau de bord sélectionne automatiquement une politique de fusion à utiliser. La politique de fusion appliquée peut être modifiée à l’aide du menu déroulant à côté du nom de la politique de fusion.

>[!NOTE]
>
>Le menu déroulant affiche uniquement les politiques de fusion qui utilisent le schéma `_xdm.context.profile`. Cependant, si votre organisation a créé plusieurs politiques de fusion, vous devrez peut-être faire défiler la liste complète des politiques de fusion disponibles.

![Onglet Aperçu des profils avec le menu déroulant Politique de fusion en surbrillance.](../images/profiles/select-merge-policy.png)

## Schémas d’union

Le tableau de bord [!UICONTROL Schéma d’union] affiche le schéma d’union pour une classe XDM spécifique. En sélectionnant la liste déroulante **[!UICONTROL Classe]**, vous pouvez afficher les schémas d’union pour différentes classes XDM.

Les schémas d’union sont composés de plusieurs schémas qui partagent la même classe et qui ont été activés pour Profile. Ils vous permettent de voir en une seule vue, une fusion de chaque champ contenu dans chaque schéma qui partage la même classe.

Pour en savoir plus sur l’[affichage des schémas d’union dans l’interface utilisateur d’Experience Platform](../../profile/ui/union-schema.md#view-union-schemas), consultez le guide de l’interface utilisateur des schémas d’union .

## Widgets et mesures

Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur vos données de profil.

La date et l’heure de l’instantané le plus récent s’affichent en haut de l’onglet [!UICONTROL Présentation] à côté de la liste déroulante Politique de fusion. Toutes les données du widget sont exactes à cette date et cette heure. La date et l’heure de l’instantané sont fournies en UTC ; elles ne se trouvent pas dans le fuseau horaire de l’utilisateur/utilisatrice ou de l’organisation.

![Onglet Aperçu du tableau de bord Profils avec la date et l’heure de l’instantané le plus récent en surbrillance.](../images/profiles/snapshot-timestamp.png)

## Widgets par défaut {#default-widgets}

Un widget de chargement par défaut est fourni pour toutes les nouvelles instances de Adobe Experience Platform qui met en évidence les dernières informations disponibles à partir de vos données. Les widgets suivants sont préconfigurés dans votre vue de segments dès le départ. Vous trouverez des détails complets sur l’objectif et la fonction des widgets ci-dessous.

* [[!UICONTROL Nombre de profils]](#profile-count)
* [[!UICONTROL Modification du nombre de profils]](#profile-count-change)
* [[!UICONTROL Tendance de modification du nombre de profils]](#profiles-count-change-trend)
* [[!UICONTROL Profils par identité]](#profiles-by-identity)
* [[!UICONTROL Chevauchement des identités]](#identity-overlap)

>[!NOTE]
>
>Depuis le 26 juillet 2023, les tableaux de bord [!UICONTROL Profils], [!UICONTROL Audiences] et [!UICONTROL Destinations] Aperçu ont été réinitialisés à un nouveau chargement de widget par défaut pour tous les utilisateurs qui n’ont pas modifié leurs vues au cours des six mois précédents. Reportez-vous à la documentation dans les sections de widget par défaut [Destinations](./destinations.md#default-widgets) et [Audiences](./audiences.md#default-widgets) pour plus d’informations sur les widgets inclus dans le cadre des chargements de widget par défaut. Vous pouvez continuer à personnaliser les widgets de votre tableau de bord comme auparavant.

## Widgets de l’IA dédiée aux clients {#customer-ai-profiles-widgets}

Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Pour ce faire, l’IA dédiée aux clients analyse les données d’événement d’expérience client existantes afin de prédire les scores de propension **attrition ou conversion**. Ces modèles de propension des clients à haute précision permettent une segmentation et un ciblage plus précis. Les informations [distribution des scores](#customer-ai-distribution-of-scores) et [résumé de notation](#customer-ai-scoring-summary) illustrent la division au sein de votre audience. Ils mettent en évidence les profils à propension élevée/faible/moyenne et la manière dont ils sont répartis entre vos nombres de profils.

* [[!UICONTROL Résumé des scores de l’IA dédiée aux clientes et aux clients]](#customer-ai-scoring-summary)
* [[!UICONTROL Distribution des scores par l’IA dédiée aux clientes et aux clients]](#customer-ai-distribution-of-scores)

### [!UICONTROL Distribution des scores par l’IA dédiée aux clientes et aux clients] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="Distribution des scores"
>abstract="Ce widget visualise la distribution du nombre total de profils en fonction de leurs scores de propension, par incréments de cinq pour cent. La distribution du nombre de profils est déterminée par le modèle d’IA et la politique de fusion sélectionnée. Vous pouvez modifier le modèle d’IA dans le menu déroulant sous le titre du widget."

Le widget [!UICONTROL  Distribution des scores de l’IA dédiée aux clients ] classe le nombre total de profils en fonction de leurs scores de propension. La distribution du nombre de profils est déterminée par le modèle d’IA et la politique de fusion sélectionnée, puis visualisée par incréments de cinq pour cent qui indiquent leur propension. Le nombre de profils est indiqué le long de l’axe Y et les scores de propension le long de l’axe X.

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
>id="platform_dashboards_profiles_scoringSummary"
>title="Résumé des scores"
>abstract="Le résumé des scores affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible. Le graphique en anneau illustre la composition proportionnelle du total des profils selon la propension élevée, moyenne et faible."

Ce widget affiche le nombre total de profils notés et les classe dans des compartiments contenant des valeurs élevées, moyennes et faibles de propension, respectivement en vert, jaune et rouge. Un graphique en anneau illustre la composition proportionnelle des profils entre des propensions élevées, moyennes et faibles. Un profil est qualifié pour une propension élevée à plus de 75 ans, une propension moyenne entre 25 et 74 ans et une propension faible avant 24 ans. Une légende indique le code couleur et les seuils des propensions. Le nombre de profils pour les propensions élevée, moyenne et faible est affiché dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

>[!NOTE]
>
>Si la visualisation est un score de propension à la conversion, les scores les plus élevés s’affichent en vert et les scores les plus bas en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

Le menu déroulant situé sous le titre du widget fournit une liste de tous les modèles d’IA dédiée aux clients configurés. Sélectionnez le modèle d’IA approprié à votre analyse dans la liste des modèles disponibles. Si aucun modèle d’IA dédiée aux clients n’est disponible, un message dans le widget vous demande de configurer au moins un modèle d’IA dédiée aux clients et fournit un lien hypertexte vers la page de configuration du modèle d’IA dédiée aux clients. Pour obtenir des instructions détaillées, consultez la documentation sur [comment configurer une instance IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Le nombre total de profils calculés dépend de la politique de fusion choisie. Pour modifier la politique de fusion utilisée, sélectionnez la liste déroulante juste en dessous de l’onglet Aperçu . Consultez la section [politiques de fusion](#merge-policies) pour une brève description, ou la [présentation de la politique de fusion](../../profile/merge-policies/overview.md) pour plus d’informations.

![Tableau de bord des audiences Experience Platform avec le widget Résumé du score de l’IA dédiée aux clients en surbrillance.](../images/segments/customer-ai-scoring-summary.png)

Pour accéder à la page d’informations détaillées pour le modèle IA dédiée aux clients sélectionné, sélectionnez **[!UICONTROL Afficher les détails du modèle]**. Vous trouverez plus d’informations sur l’IA dédiée aux clients dans le guide de l’interface utilisateur [Discover Insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

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
* [[!UICONTROL Tendance de modification des profils non segmentés]](#unsegmented-profiles-change-trend)
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
>Le widget [!UICONTROL Nombre de profils] peut afficher un nombre différent du nombre de profils affiché dans l’onglet [!UICONTROL Parcourir] dans la section [!UICONTROL Profils] de l’interface utilisateur pour plusieurs raisons. La raison la plus courante de cette différence est que l’onglet [!UICONTROL Parcourir] référence le nombre total de profils fusionnés en fonction de la politique de fusion par défaut de votre organisation, tandis que le widget [!UICONTROL Nombre de profils] référence le nombre total de profils fusionnés en fonction de la politique de fusion que vous avez sélectionnée pour afficher dans le tableau de bord.
>
>Une autre raison courante est due aux différences entre le moment où l’instantané du tableau de bord est pris et le moment où l’exemple de tâche est exécuté pour l’onglet [!UICONTROL Parcourir]. Vous pouvez voir quand le widget [!UICONTROL Nombre de profils] a été mis à jour pour la dernière fois en regardant la date et l’heure sur le widget. Pour en savoir plus sur la manière dont l’exemple de tâche est déclenché sur l’onglet [!UICONTROL Parcourir], voir la section [nombre de profils](../../profile/ui/user-guide.md#profile-count) dans le guide de l’interface utilisateur du profil client en temps réel.

![Le tableau de bord Profils Experience Platform avec le widget Nombre de profils en surbrillance.](../images/profiles/profile-count.png)

### [!UICONTROL Tendance du nombre de profils] {#profile-count-trend}

Le widget [!UICONTROL Tendance du nombre de profils] utilise un graphique linéaire pour illustrer la tendance du nombre total de profils contenus dans le système au fil du temps. Ce nombre total inclut tous les profils importés dans le système depuis le dernier instantané quotidien. Les données peuvent être visualisées sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget.

![Le widget Tendance du nombre de profils.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Modification du nombre de profils] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Modification du nombre de profils"
>abstract="Ce widget affiche le nombre total de profils fusionnés **ajoutés** à la banque de profils au moment du dernier instantané. Le nombre dépend de la politique de fusion sélectionnée appliquée à vos données de profil."

Le widget **[!UICONTROL Modification du nombre de profils]** affiche le nombre de profils fusionnés ajoutés à la banque de profils depuis l’instantané précédent. Ce nombre est le résultat de l’application de la politique de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu. Vous pouvez utiliser le sélecteur de liste déroulante pour afficher le nombre de profils ajoutés au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois.

>[!NOTE]
>
>Le widget [!UICONTROL  Modification du nombre de profils ] reflète le nombre de profils ajoutés **après** la configuration initiale de l’ingestion des profils et de la banque de profils. En d’autres termes, si votre organisation a configuré la banque de profils et ingéré 4 000 000 profils au jour 1, le tableau de bord sera disponible dans les 24 heures, mais le widget [!UICONTROL  Modification du nombre de profils ] sera défini sur 0. Cette méthode de comptage permet d’éviter un pic associé à l’ingestion initiale des profils dans le système. Au cours des 30 prochains jours, votre organisation ingérera 1 000 000 profils supplémentaires dans la banque de profils. Une fois l’instantané suivant pris, le widget [!UICONTROL Modification du nombre de profils] affiche un total de 1 000 000 profils ajoutés, tandis que le widget [!UICONTROL Nombre de profils] affiche un total de 5 000 000 profils.

![Le tableau de bord Profils de l’interface utilisateur d’Experience Platform avec le widget Modification du nombre de profils en surbrillance.](../images/profiles/profile-count-change.png)

### [!UICONTROL Tendance de modification du nombre de profils] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Tendance de modification du nombre de profils"
>abstract="Ce widget affiche le nombre de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois. Le nombre dépend également de la politique de fusion sélectionnée appliquée à vos données de profil."

Le widget **[!UICONTROL Tendance de modification du nombre de profils]** affiche le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois. Ce nombre est mis à jour chaque jour lorsque l’instantané est pris. Par conséquent, si vous deviez ingérer des profils dans Experience Platform, le nombre de profils ne serait pas reflété tant que l’instantané suivant n’aurait pas été pris. Le nombre de profils ajoutés est le résultat de l’application de la politique de fusion sélectionnée à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu.

Pour en savoir plus, consultez la section [ sur les politiques de fusion plus haut dans ce document](#merge-policies).

Le widget **[!UICONTROL Tendance de modification du nombre de profils]** affiche un bouton « légendes » en haut à droite du widget. Pour ouvrir la boîte de dialogue de légendes automatiques, sélectionnez **[!UICONTROL Légendes]**.

![L’onglet Aperçu du profil affiche le widget Tendance de modification du nombre de profils avec le bouton Légendes en surbrillance.](../images/profiles/profiles-count-change-trend-captions.png)

Un modèle de machine learning génère automatiquement des légendes pour décrire les tendances clés et les événements importants en analysant le graphique et les données. Les annotations sont ajoutées au graphique en fonction des légendes. Sélectionnez une légende pour mettre l’accent sur l’annotation correspondante.

![La boîte de dialogue de légendes automatiques du widget Tendance de modification de nombre de profils.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Tendance de modification du nombre de profils par identité] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Ce widget filtre le nombre de profils en fonction d’une identité source sélectionnée et d’une politique de fusion, puis illustre la modification du nombre pour différentes périodes à l’aide d’un graphique linéaire. La politique de fusion est sélectionnée dans la liste déroulante d’aperçu située en haut de la page. L’identité source et la période sont sélectionnées dans les menus déroulants du widget. La tendance peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois.

Ce widget vous permet de gérer vos besoins d’activation de destination en présentant le modèle de croissance des profils filtrés selon l’identité requise.

![Le widget Tendance de modification du nombre de profils par identité.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profils par identité"
>abstract="Ce widget affiche la répartition de tous les profils fusionnés dans votre banque de profils par identités."

Le widget **[!UICONTROL Profils par identité]** affiche la répartition des identités pour tous les profils fusionnés de votre banque de profils. Le nombre total de profils par identité (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent être associés à un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

Pour en savoir plus, consultez la section [ sur les politiques de fusion plus haut dans ce document](#merge-policies).

![Le tableau de bord d’aperçu des profils avec le widget Profils par identité mis en surbrillance.](../images/profiles/profiles-by-identity.png)

Pour ouvrir la boîte de dialogue de légendes automatiques, sélectionnez **[!UICONTROL Légendes]**.

![La boîte de dialogue des légendes des profils par identité.](../images/profiles/profiles-by-identity-captions.png)

Un modèle de machine learning génère automatiquement des informations sur les données en analysant la distribution globale et les dimensions clés des données.

Pour en savoir plus sur les identités, consultez la documentation du service Adobe Experience Platform Identity [](../../identity-service/home.md).

### [!UICONTROL Chevauchement des identités] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Chevauchement des identités"
>abstract="Ce widget utilise un diagramme de Venn pour afficher le chevauchement des profils de votre banque de profils qui contiennent les deux identités sélectionnées."

Le widget **[!UICONTROL Chevauchement des identités]** utilise un diagramme de Venn, ou un diagramme logique, pour afficher le chevauchement des profils de votre banque de profils qui contiennent les deux identités sélectionnées.

Utilisez les menus déroulants du widget pour sélectionner les identités à comparer. Les cercles affichent le nombre total relatif de profils qui contiennent chaque identité. Le nombre de profils contenant les deux identités est représenté par la taille du chevauchement entre les cercles. Si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités sont associées à ce client individuel. Dans ce cas, il est probable que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour plus d’informations sur les fragments de profil, reportez-vous à la section [fragments de profil contre profils fusionnés](../../profile/home.md#profile-fragments-vs-merged-profiles) dans la présentation du profil client en temps réel.

Pour en savoir plus sur les identités, consultez la documentation du service Adobe Experience Platform Identity [](../../identity-service/home.md).

![Présentation du tableau de bord Profils avec le widget Chevauchement des identités en surbrillance.](../images/profiles/identity-overlap.png)

### [!UICONTROL Profils à identité unique] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Profils à identité unique"
>abstract="Ce widget fournit le nombre de profils de votre organisation qui n’ont qu’un seul type d’identifiant qui crée leur identité. Ce type d’identifiant peut être une adresse e-mail ou un ECID."

Le widget [!UICONTROL Profils à identité unique] fournit un nombre des profils de votre organisation qui ne disposent que d’un seul type d’identifiant qui crée leur identité. Ce type d’identifiant peut être une adresse e-mail ou un ECID. Le nombre de profils est généré à partir des données contenues dans l’instantané le plus récent.

![Widget Profils d’identité unique.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Profils d’identité unique par identité] {#single-identity-profiles-by-identity}

Ce widget utilise un graphique à barres pour illustrer le nombre total de profils qui sont identifiés à l’aide d’un identifiant unique. Le widget prend en charge jusqu’à cinq des identités les plus courantes.

Pour afficher une boîte de dialogue détaillant le nombre total de profils pour une identité, utilisez le curseur pour pointer sur des barres individuelles.

![Widget Profils d’identité unique par identité.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Profils non segmentés] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Profils non segmentés"
>abstract="Ce widget fournit le nombre total de profils qui ne sont associés à aucune audience et représente l’opportunité d’activation des profils à l’échelle de votre organisation."

Le widget [!UICONTROL  Profils non segmentés ] fournit le nombre total de profils qui ne sont associés à aucune audience. Le nombre, généré à partir du dernier instantané, est précis et souligne l’opportunité d’activation de profils dans votre entreprise. Il indique également la possibilité d’effacer les profils qui ne fournissent pas un retour sur investissement adéquat.

![Widget Profils non segmentés.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Tendance de modification des profils non segmentés] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Tendance des profils non segmentés"
>abstract="Ce widget fournit une illustration graphique linéaire du nombre de profils qui ne sont associés à aucune audience sur une période donnée. La tendance des profils non associés à une audience peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois."

Le widget [!UICONTROL  Tendance de modification des profils non segmentés ] utilise un graphique linéaire pour illustrer le nombre de profils ajoutés depuis le dernier instantané quotidien qui ne sont associés à aucune audience. La tendance de changement des profils qui ne sont associés à aucune audience peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. La période est sélectionnée dans un menu déroulant du widget. Le nombre de profils est reflété sur l’axe des ordonnées et la période sur l’axe des abscisses.

![Le widget Tendance de modification des profils non segmentés.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Profils non segmentés par identité] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>Le widget Profils non segmentés par identité est obsolète depuis octobre 2022 et n’est plus disponible.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Audiences] {#audiences}

Ce widget fournit le nombre total d’audiences prêtes à être activées, en fonction de la politique de fusion choisie appliquée aux données de votre profil.

Sélectionnez **[!UICONTROL Audiences]** pour accéder à l’onglet [!UICONTROL Parcourir] du tableau de bord [!UICONTROL Audiences]. De là, vous pouvez voir une liste de toutes les définitions de segment pour votre organisation.

![Widget Audiences.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Rapport de chevauchement des audiences] {#audience-overlap-report}

Ce widget tabularise le chevauchement des données de toutes les audiences disponibles filtrées par politique de fusion. Une liste de cinq audiences classées du pourcentage de chevauchement le plus élevé au plus faible est fournie pour la politique de fusion choisie dans le menu déroulant en haut de l’écran. Les deux audiences analysées sont répertoriées dans les colonnes [!UICONTROL NOM DE L’AUDIENCE A] et [!UICONTROL NOM DE L’AUDIENCE B]. Le chevauchement en pourcentage est fourni dans la troisième colonne avec une précision de douze décimales.

Le rapport sur le chevauchement des audiences vous permet de créer de nouvelles audiences hautement performantes. L’observation des chevauchements au pourcentage élevé vous permet de supprimer des audiences et d’empêcher l’envoi d’une même audience vers différentes destinations. Elle vous aide également à identifier les informations cachées qui peuvent contribuer à une meilleure segmentation. Un chevauchement au pourcentage faible permet de localiser les profils uniques à rechercher.

Sélectionnez **[!UICONTROL Afficher plus]** pour ouvrir une boîte de dialogue plein écran contenant davantage de données de chevauchement des audiences.

![Le widget Rapport de chevauchement des audiences avec l’option Afficher plus en surbrillance.](../images/profiles/profiles-audience-overlap-report.png)

La boîte de dialogue [!UICONTROL Rapport de chevauchement des audiences] s’affiche. Cette boîte de dialogue peut contenir jusqu’à 50 lignes d’analyses de chevauchement des audiences, divisées en six colonnes. Pour supprimer ou ajouter des colonnes du tableau, sélectionnez l’icône des paramètres (![icône des paramètres.](/help/images/icons/settings.png)).

![Boîte de dialogue Rapport de chevauchement des audiences.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Pour modifier le classement des résultats, du plus haut au plus bas ou du plus bas au plus haut, sélectionnez l’en-tête de colonne **[!UICONTROL Chevauchement]**.

Pour télécharger l’intégralité du rapport au format PDF, sélectionnez le menu d’options (**`...`**), puis **[!UICONTROL Télécharger]**.

![La boîte de dialogue Rapport de chevauchement des audiences avec les points de suspension et l’option de téléchargement en surbrillance.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Pour ouvrir un diagramme de Venn de l’analyse de chevauchement, sélectionnez une ligne dans le rapport. Pour afficher le nombre de profils dans une boîte de dialogue, passez la souris sur une section du diagramme de Venn.

![La boîte de dialogue Rapport de chevauchement des audiences avec un diagramme de Venn et une ligne en surbrillance.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Sélectionnez **[!UICONTROL Fermer]** pour revenir au tableau de bord des [!UICONTROL Profils].

### [!UICONTROL Audiences mappées au statut de destination] {#audiences-mapped-to-destination-status}

Le widget [!UICONTROL  Audiences mappées au statut de destination ] affiche le nombre total d’audiences mappées et non mappées dans une seule mesure et utilise un graphique en anneau pour illustrer la différence proportionnelle entre les totaux. Les nombres calculés dépendent de la politique de fusion choisie.

Les nombres individuels des audiences mappées ou non mappées s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Le widget Audiences mappées au statut de destination.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Taille des audiences] {#audiences-size}

Le widget [!UICONTROL  Taille des audiences ] fournit un tableau à deux colonnes qui répertorie les noms de 20 audiences maximum et le nombre total de profils contenus dans chaque audience. La liste est classée de haut en bas en fonction du nombre total de profils contenus dans l’audience. Le nombre total de tailles d’audience dépend de la politique de fusion appliquée.

![Le widget Taille des audiences.](../images/profiles/audiences-size.png)

Pour afficher des informations complètes sur une audience, sélectionnez un nom d’audience dans la liste fournie pour accéder à la page [!UICONTROL Audiences] [!UICONTROL Détail]. En outre, en sélectionnant **[!UICONTROL Afficher toutes les audiences]** à la fin du widget, vous pouvez accéder à l’onglet [!UICONTROL Audiences] [!UICONTROL Parcourir] pour trouver une audience existante.

![Le widget Taille des audiences avec un nom d’audience et le texte Afficher toutes les audiences en surbrillance.](../images/profiles/audiences-size-view-all-audiences.png)

Vous trouverez plus d’informations sur les détails de l’audience dans la [documentation du portail Audience](../../segmentation/ui/audience-portal.md).

### [!UICONTROL Chevauchements d’audience par politique de fusion] {#audience-overlap-by-merge-policy}

Ce widget utilise un diagramme de Venn pour afficher le chevauchement de deux audiences sélectionnées. La politique de fusion est sélectionnée dans la liste déroulante d’aperçu située en haut de la page et les audiences à analyser sont sélectionnées dans deux menus déroulants du widget. Le nombre total de profils contenus dans la définition de segment appropriée peut être affiché en passant la souris sur un cercle ou l’intersection.

Ce widget affiche le croisement visuel des définitions de segment et vous permet d’optimiser la politique de segmentation en étudiant les similitudes entre les définitions de segment.

![Tableau de bord Profils de l’interface utilisateur d’Experience Platform avec les listes déroulantes Politique de fusion et Audience du widget en surbrillance.](../images/profiles/audience-overlap-by-merge-policy.png)


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

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord des profils et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des données [!DNL Profile] dans l’interface utilisateur d’Experience Platform, reportez-vous au guide [Real-Time Customer Profile UI guide](../../profile/ui/user-guide.md).
