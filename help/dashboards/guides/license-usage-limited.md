---
keywords: Experience Platform;interface utilisateur;interface utilisateur;personnalisation;tableau de bord d’utilisation de la licence;tableau de bord;utilisation des licences;droits;consommation
title: Tableau de bord d’utilisation de la licence Guide
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise.
type: Documentation
hide: true
hidefromtoc: true
source-git-commit: 25f57b1bfbcb2ec95f88afb69386a10deb600125
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 7%

---

# Tableau de bord de l’utilisation de la licence (version limitée) {#license-usage-dashboard-limited-release}

>[!IMPORTANT]
>
>La mise à jour [!UICONTROL Utilisation des licences] Le tableau de bord est actuellement disponible dans une **version limitée uniquement** et n’est pas disponible pour tous les clients.

Vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise via Adobe Experience Platform [!UICONTROL Utilisation des licences] tableau de bord. Les informations affichées ici sont capturées pendant un instantané quotidien de votre instance Platform.

Les rapports sur l’utilisation des licences fournissent un niveau de granularité élevé par rapport à vos mesures d’utilisation des licences. Le tableau de bord fournit des mesures d’utilisation pour chaque produit acheté, l’utilisation consolidée des mesures dans tous les environnements de test de production ou de développement et la mesure d’utilisation d’un environnement de test spécifique. Les applications Experience Platform suivantes peuvent être suivies avec des mesures d’utilisation : Real-Time Customer Data Profile, Adobe Journey Optimizer et Customer Journey Analytics.

Ce guide explique comment accéder au tableau de bord de l’utilisation des licences dans l’interface utilisateur et l’utiliser. Il fournit également des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour une présentation générale de l’interface utilisateur de Platform, reportez-vous à la section [Guide de l’interface utilisateur Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL Utilisation des licences] données du tableau de bord

La variable [!UICONTROL Utilisation des licences] tableau de bord affiche la liste de tous les produits Experience Platform que vous avez achetés. Dans cette liste, vous pouvez trouver un instantané des données liées aux licences de votre entreprise pour Experience Platform sur n’importe quel environnement de test associé.

Les données de ce tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données et le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord d’utilisation des licences {#explore}

Pour accéder au tableau de bord de l’utilisation des licences dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Utilisation des licences]** dans le rail de gauche. La variable [!UICONTROL Présentation] s’ouvre, affichant une liste des produits disponibles.

>[!NOTE]
>
>Le tableau de bord de l’utilisation des licences n’est pas activé par défaut. Les utilisateurs doivent se voir accorder &quot;[!UICONTROL Afficher le tableau de bord d’utilisation de licence]&quot; pour pouvoir afficher le tableau de bord. Pour connaître les étapes d’octroi des autorisations d’accès pour afficher le tableau de bord d’utilisation des licences, reportez-vous à la section [Guide des autorisations de tableau de bord](../permissions.md).

![Onglet Aperçu de l’utilisation de la licence , avec l’utilisation de la licence mise en surbrillance dans la barre de navigation de gauche.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Onglet Aperçu] {#overview-tab}

Ce tableau de bord affiche sous forme de tableau tous les produits Adobe Experience Platform sous licence, y compris les modules complémentaires. Le tableau fournit des informations clés sur l’utilisation de votre licence pour tous les profils disponibles.

| Nom de la colonne | Description |
|---|---|
| **[!UICONTROL Produit]** | La solution d’Adobe sous licence de votre entreprise. |
| **[!UICONTROL Mesure de Principal]** | Mesure principale utilisée pour le suivi dans pour ce produit. |
| **[!UICONTROL Montant de la licence]** | La valeur contractuelle correspondant au montant maximal de la mesure de Principal, conformément à ce qui est convenu dans votre contrat de licence de produit. |
| **[!UICONTROL Utilisation]** | Montant de la mesure principale utilisée. Cette valeur fournit l’utilisation totale de cette mesure pour tous les environnements de test, que ce soit la production ou le développement. |
| **[!UICONTROL Utilisation %]** | Le pourcentage de votre mesure principale utilisée en fonction de votre montant de licence. |

>[!NOTE]
>
>Ajouts au [!UICONTROL Montant de la licence] suite à des modules complémentaires, sont ajoutés en plus de la fonction [!UICONTROL Montant de la licence] pour les produits de base tels que Real-time Customer Data Profile, Adobe Journey Optimizer et Customer Journey Analytics. L’utilisation de ce montant sous licence (après les modules complémentaires) est suivie par le biais des produits de base. Par exemple, si vous achetez un pack de cinq environnements de test, la quantité de cinq est ajoutée à celle du produit de base. Dans ce cas, le module complémentaire affiche une [!UICONTROL Montant de la licence] d’un, et l’utilisation de ce module complémentaire est &quot;vide&quot;, car l’utilisation est suivie via le produit de base.

Le tableau indique la mesure principale de chaque produit, car chaque produit peut effectuer le suivi de nombreuses mesures. Pour afficher d’autres mesures et des informations détaillées sur l’utilisation de votre licence de produit, sélectionnez un nom de produit dans la liste. La variable [!UICONTROL Résumé] s’affiche pour ce produit.

## [!UICONTROL Onglet Résumé] {#summary-tab}

Toutes les mesures disponibles s’affichent sur la page [!UICONTROL Résumé] . Les mesures disponibles dépendent du produit sous licence. Cette vue fournit **une vue consolidée de toutes les mesures pour tous les environnements de test de production ou de développement ;**. Le même niveau d’analyse est fourni pour les environnements de test de production et de développement.

![Vue récapitulative d’un produit Platform qui affiche toutes les mesures disponibles pour ce produit.](../images/license-usage/summary-tab.png)

Dans l’onglet Résumé, le tableau comprend la variable [!UICONTROL Mesure] colonne . Ces descriptions lisibles par l’utilisateur indiquent toutes les mesures utilisées pour ce type d’environnement de test.

### Sélection d’un environnement de test {#select-sandbox}

Pour modifier l’affichage entre les types d’environnements de test de production et de développement, sélectionnez l’une des options suivantes : [!UICONTROL Environnements de test de production] ou [!UICONTROL Environnements de test de développement]. Le type d’environnement de test sélectionné est indiqué par le bouton radio en regard du nom de l’environnement de test.

La création de rapports de consommation pour les environnements de test est cumulative pour tous les environnements de test du même type. En d’autres termes, la sélection [!UICONTROL Production] ou [!UICONTROL Développement] fournit des rapports sur la consommation pour tous les environnements de test de production ou de développement, respectivement.

![La vue de synthèse d’un produit Platform avec des environnements de test de production et des environnements de test de développement est mise en surbrillance.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>L’autorisation d’afficher le tableau de bord de l’utilisation des licences doit être spécifiée au niveau de l’environnement de test. Vous devez ajouter des autorisations à chaque environnement de test individuel pour les afficher dans le tableau de bord. Cette limitation sera corrigée dans une version ultérieure. En attendant, la solution suivante est disponible :
>
>1. Créez un profil de produit dans Adobe Admin Console.
>2. Sous Autorisation dans la catégorie Sandbox , ajoutez tous les environnements de test que vous souhaitez afficher dans le tableau de bord de l’utilisation des licences.
>3. Dans la catégorie Autorisation du tableau de bord utilisateur , ajoutez l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot;.

## La variable [!UICONTROL Détails] tab {#details-tab}

Pour voir **une mesure d’utilisation spécifique d’un environnement de test spécifique ;**, accédez à la [!UICONTROL Détails] . La variable [!UICONTROL Détails] affiche tous les environnements de test disponibles dans les environnements de test Production ou Développement.

![Onglet Détails du tableau de bord Utilisation de la licence.](../images/license-usage/details-tab.png)

Dans cette vue, vous pouvez sélectionner ![Icône d’inspection.](../images/license-usage/inspect-icon.png) en regard d’un nom d’environnement de test pour afficher la visualisation de cette mesure. Une boîte de dialogue s’ouvre avec une visualisation pour cette mesure.

### Visualisations {#visualizations}

Chaque widget de visualisation comprend les aspects suivants :

- Graphique linéaire qui suit le changement de mesure au fil du temps
- Clé du graphique linéaire.
- Le nom du sandbox
- Menu déroulant permettant d’ajuster la période du graphique linéaire.

Les graphiques linéaires comparent les chiffres d’utilisation de votre entreprise au total disponible avec les licences de votre entreprise et fournissent un pourcentage de l’utilisation totale.

![Visualisation d’une mesure.](../images/license-usage/visualization.png)

La période de recherche arrière de l’analyse peut être ajustée à partir du menu déroulant. Valeur par défaut des 30 derniers jours

Pour sélectionner une plage de dates, vous pouvez utiliser la liste déroulante de plage de dates afin de sélectionner la période à afficher dans le tableau de bord. Plusieurs options sont disponibles, notamment la valeur par défaut des 30 derniers jours.

![La boîte de dialogue de visualisation avec la liste déroulante de période mise en surbrillance.](../images/license-usage/date-range.png)

Vous pouvez également sélectionner **[!UICONTROL Date personnalisée]** pour choisir la période qui s’affiche.

![L’onglet Aperçu du tableau de bord de l’utilisation de la licence avec les options de période personnalisées surlignées.](../images/license-usage/custom-date-range.png)

## Mesures disponibles

Le tableau de bord de l’utilisation des licences répertorie plusieurs mesures uniques qui s’appliquent à plusieurs produits de l’entreprise. Les mesures disponibles sont les suivantes :

- [!UICONTROL Nombre d’environnements de test]
- [!UICONTROL Audience adressable]
- [!UICONTROL Richesse moyenne du profil]
- [!UICONTROL Heures principales]
- [!UICONTROL Stockage du lac de données]
- [!UICONTROL Ratio de segmentation des données analysées]
- [!UICONTROL Audience dynamique]
- [!UICONTROL Stockage total consommé]
- [!UICONTROL Stockage total]
- [!UICONTROL Heures de calcul de Query Service]

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par l’entreprise. Pour obtenir des définitions détaillées de chaque mesure, reportez-vous à la documentation Description du produit appropriée :

| Licence | Description du produit |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, services d’application et services intelligents](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMOMENT DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>ACTIVATION AEP:OD</li><li>AEP:OD ACTIVATION PRFL À 10M</li><li>AEP:PRFL D’ACTIVATION OD JUSQU’À 50 M</li></ul> | [Activation de Adobe Experience Platform](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELLIGENCE OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME : OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>DÉMARRAGE ULTIMATE DE L’OPTION UNP AJO : OD</li><li>UNP REAL-TIME CDP : ORCHESTRATION DU PROFIL OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Le tableau de bord de l’utilisation des licences ne tient compte que de la dernière licence configurée pour votre entreprise. Si la dernière licence configurée pour votre entreprise n’apparaît pas dans le tableau ci-dessus, le tableau de bord de l’utilisation des licences peut ne pas s’afficher correctement. La prise en charge de licences supplémentaires et de plusieurs licences au sein d’une même organisation est prévue pour une version ultérieure.

## Étapes suivantes

Après avoir lu ce document, vous pouvez localiser le tableau de bord d’utilisation des licences et afficher les mesures d’utilisation de chaque produit acheté, pour tous les environnements de test de production ou de développement, ainsi que pour un environnement de test spécifique. Vous trouverez plus d’informations sur les mesures disponibles pour votre entreprise, en fonction des licences achetées par celle-ci.

Pour en savoir plus sur les autres fonctionnalités disponibles dans l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Platform](../../landing/ui-guide.md).
