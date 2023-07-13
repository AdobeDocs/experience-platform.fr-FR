---
title: Guide du tableau de bord des profils de compte
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les profils de compte B2B de votre entreprise.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 10%

---

# [!UICONTROL Profils de compte] tableau de bord

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos profils de compte, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder à et utiliser le [!UICONTROL Profils de compte] tableau de bord dans l’interface utilisateur et fournit des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour une présentation de toutes les fonctionnalités de l’interface utilisateur du profil de compte, rendez-vous sur la page [guide de l’interface utilisateur du profil de compte](../../rtcdp/accounts/account-profile-ui-guide.md).

## Prise en main

Vous devez avoir le droit de [Adobe Real-time Customer Data Platform version B2B](../../rtcdp/b2b-overview.md) afin d’accéder à l’objet B2B [!UICONTROL Profils de compte] tableau de bord.

## Données des profils de compte

Le [!UICONTROL Profils de compte] le tableau de bord affiche un instantané des informations de compte unifiées provenant de plusieurs sources sur vos canaux marketing et des différents systèmes actuellement utilisés par votre organisation pour stocker les informations de compte client.

Les données de profil de l’instantané affichent les données exactement telles qu’elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et la variable [!UICONTROL Profils de compte] le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorez les [!UICONTROL Profils de compte] tableau de bord

Pour accéder au [!UICONTROL Profils de compte] Tableau de bord dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** under [!UICONTROL Comptes] dans le panneau de navigation de gauche.

![L’interface utilisateur de Platform avec les profils de compte dans le volet de navigation de gauche est mise en surbrillance et l’onglet de présentation s’affiche.](../images/account-profiles/account-profiles-dashboard.png)

Dans la [!UICONTROL Profils de compte] vous pouvez effectuer l’une des opérations suivantes : [parcourir les profils de compte ingérés dans votre organisation ;](#browse-account-profiles)ou [afficher l’intégralité des données de profil de compte en un coup d’oeil à l’aide de widgets ;](#standard-widgets) qui visualisent les aspects des données.

## Parcourir les profils de compte {#browse-account-profiles}

Le [!UICONTROL Parcourir] vous permet de rechercher et d’afficher les profils de compte en lecture seule ingérés dans votre organisation à l’aide d’un ID de compte provenant d’une source d’entreprise connectée ou en saisissant directement les détails de la source. Vous y trouverez des informations importantes appartenant au profil du compte, notamment leur nom, leur secteur d’activité, leurs recettes et leur audience.

Sélectionnez la [!UICONTROL Identifiant de profil] dans les résultats affichés sur la [!UICONTROL Parcourir] pour ouvrir la [!UICONTROL Détails] pour le profil du compte.

![L’onglet de navigation Profils de compte avec les résultats affichés et l’identifiant de profil mis en surbrillance.](../images/account-profiles/account-profiles-browse-tab.png)

Les informations de profil du compte affichées sur la [!UICONTROL Détails] a été fusionné à partir de plusieurs fragments de profil pour former une vue unique du compte individuel. Consultez la documentation relative à [navigation dans les profils de compte dans Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) pour en savoir plus sur les fonctionnalités d’affichage des profils de compte dans l’interface utilisateur de Platform.

## Le [!UICONTROL Profils de compte] [!UICONTROL Présentation] {#overview}

Le [!UICONTROL Présentation] Cet onglet est composé de widgets qui fournissent des mesures en lecture seule pour transmettre des informations importantes sur vos profils de compte. Sélectionner **[!UICONTROL Modifier le tableau de bord]** pour modifier l’aspect de la variable [!UICONTROL Présentation] en déplaçant et en redimensionnant les widgets.

![Onglet Aperçu des profils de compte avec l’option Modifier le tableau de bord mise en surbrillance.](../images/account-profiles/modify-dashboard.png)

Reportez-vous au document sur [modification des tableaux de bord](../customize/modify.md) et le [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

## Widgets standard {#standard-widgets}

Adobe fournit des widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos profils de compte.

Pour en savoir plus sur chacun des widgets standards disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [ du nombre total de comptes par secteur](#total-accounts-by-industry)
* [Profils de compte ajoutés](#account-profiles-added)
* [Distribution de notation prédictive](#predictive-scoring-distribution)
* [Facteurs d’influence de la notation prédictive](#predictive-scoring-top-influential-factors)

###  du nombre total de comptes par secteur {#total-accounts-by-industry}

Ce widget affiche le nombre total de comptes dans une seule mesure. Un graphique en anneau permet en outre d’illustrer la proportion de comptes pour chaque secteur constituant le nombre global. La clé fournit des informations de codage en couleur pour les différents secteurs qui composent le graphique en anneau.

Les décomptes individuels des différentes industries s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Total des comptes par widget industriel.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Profils de compte ajoutés {#account-profiles-added}

Ce widget utilise un graphique à barres avec code-couleur pour illustrer le nombre de profils ajoutés à un compte sur une période donnée, ainsi que la proportion des différents secteurs d’activité qui constituent ces profils ajoutés. Les secteurs sont codés en couleur et une clé fournit des informations de codage des couleurs pour les différents secteurs qui constituent le graphique à barres. La période d’analyse est sélectionnée dans le menu déroulant du widget. Le graphique à barres peut être visualisé sur une période de 30 jours, 90 jours et 12 mois.

>[!NOTE]
>
>Comme les profils ne sont ajoutés qu’à un compte et ne sont jamais supprimés, le plus petit nombre possible de profils ajoutés sur une période donnée est zéro.

![Le widget Profils de compte ajouté.](../images/account-profiles/accounts-profiles-added-widget.png)

### Distribution de notation prédictive {#predictive-scoring-distribution}

Le [!UICONTROL Distribution de notation prédictive] widget affiche la distribution des scores de tous les profils de compte pour vous aider à comprendre en un coup d’oeil l’état de votre pipeline de ventes. Les données de notation sont véhiculées par le biais d’un graphique en anneau et d’un graphique en colonnes.

Le graphique en anneau illustre la proportion de vos profils de compte totaux dans chacune des classes à forte, moyenne et faible propension à acheter des compartiments. La clé fournit plus de détails sur les sections codées par couleur, y compris les plages de compartiment de notation et le nombre de profils de compte dans cette plage.

Le graphique en colonnes fournit une ventilation de notation plus granulaire. Chaque colonne indique le nombre de profils de compte dans chacun des 20 intervalles de cinq points.

Le menu déroulant du widget vous permet de sélectionner le modèle de notation du compte.

![Le widget de distribution de notation prédictive.](../images/account-profiles/predictive-scoring-distribution.png)

### Facteurs d’influence de la notation prédictive {#predictive-scoring-top-influential-factors}

Le [!UICONTROL Facteurs d’influence de la notation prédictive] vous aide à comprendre les facteurs les plus significatifs qui génèrent les scores pour chaque compartiment de propension.

Ce widget présente les principaux facteurs d’influence pour chacun des compartiments de propension élevée, moyenne et faible. Une barre pour chaque facteur d’influence indique le pourcentage des profils de compte dans ce compartiment de propension qui contient le facteur d’influence spécifique.

Le menu déroulant du widget vous permet de sélectionner le modèle de notation du compte.

![Le widget Score prédictif des principaux facteurs d’influence .](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Étapes suivantes

En suivant ce document, vous devez maintenant savoir comment localiser la variable [!UICONTROL Profils de compte] tableau de bord. Vous devriez également comprendre désormais les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des profils de compte dans le cadre de vos données B2B dans l’interface utilisateur de l’Experience Platform, reportez-vous à la section [présentation des profils de compte](../../rtcdp/accounts/account-profile-overview.md) pour Adobe Real-Time CDP, édition B2B.
