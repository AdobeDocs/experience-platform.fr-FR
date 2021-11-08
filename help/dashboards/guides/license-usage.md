---
keywords: Experience Platform;interface utilisateur;interface utilisateur;personnalisation;tableau de bord d’utilisation des licences;tableau de bord;utilisation des licences;droits;consommation
title: Tableau de bord de l’utilisation des licences
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 87b6e12b33c49bdae49be45ce10f92b309a1e98e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 5%

---

# Tableau de bord d’utilisation de la licence {#license-usage-dashboard}

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation de la licence de votre entreprise, telles qu’elles sont capturées pendant un instantané quotidien. Ce guide explique comment accéder au tableau de bord de l’utilisation des licences dans l’interface utilisateur et l’utiliser. Il fournit également des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour obtenir un aperçu général de l’interface utilisateur de Platform, consultez le [Guide de l’interface utilisateur Experience Platform](../../landing/ui-guide.md).

## Données du tableau de bord d’utilisation des licences

Le tableau de bord de l’utilisation des licences affiche un instantané des données relatives aux licences de votre entreprise pour Experience Platform. Les données du tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données et le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord de l’utilisation des licences

Pour accéder au tableau de bord de l’utilisation des licences dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Utilisation des licences]** dans le rail de gauche. Cela ouvre la fenêtre **[!UICONTROL Présentation]** du tableau de bord.

>[!NOTE]
>
>Le tableau de bord de l’utilisation des licences n’est pas activé par défaut. Pour pouvoir afficher le tableau de bord, les utilisateurs doivent disposer de l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot;. Pour connaître les étapes d’octroi des autorisations d’accès pour afficher le tableau de bord d’utilisation des licences, reportez-vous à la section [Guide des autorisations de tableau de bord](../permissions.md).

![](../images/license-usage/dashboard-overview.png)

### Sélection d’un environnement de test

Pour choisir un environnement de test à afficher dans le tableau de bord, sélectionnez l’une des options suivantes : [!UICONTROL Production] ou [!UICONTROL Développement]. L’environnement de test sélectionné est indiqué par le bouton radio en regard du nom de l’environnement de test.

La création de rapports de consommation pour les environnements de test est cumulative pour tous les environnements de test du même type. En d’autres termes, la sélection [!UICONTROL Production] ou [!UICONTROL Développement] fournit des rapports sur la consommation pour tous les environnements de test de production ou de développement, respectivement.

![](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>L’autorisation d’afficher le tableau de bord de l’utilisation des licences doit être spécifiée au niveau de l’environnement de test. Cela signifie que l’autorisation d’afficher le tableau de bord doit être ajoutée à chaque environnement de test individuel. Cette limitation sera corrigée dans une version ultérieure. En attendant, la solution suivante est disponible :
>
>1. Créez un profil de produit dans Adobe Admin Console.
>2. Sous Autorisation dans la catégorie Sandbox , ajoutez tous les environnements de test que vous souhaitez afficher dans le tableau de bord de l’utilisation des licences.
>3. Dans la catégorie Autorisation du tableau de bord utilisateur , ajoutez l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot;.


### Sélection d’une période

Après avoir sélectionné un environnement de test, vous pouvez utiliser la liste déroulante de période pour sélectionner la période à afficher dans le tableau de bord. Plusieurs options sont disponibles, notamment la valeur par défaut des 30 derniers jours.

![](../images/license-usage/select-date-range.png)

Vous pouvez également sélectionner **[!UICONTROL Date personnalisée]** pour choisir la période qui s’affiche.

![](../images/license-usage/select-custom-date.png)

## Widgets

Le tableau de bord de l’utilisation des licences est constitué de widgets qui affichent des mesures en lecture seule fournissant des informations importantes sur l’utilisation des licences de votre entreprise. Les mesures visibles dépendent des licences spécifiques à votre entreprise (voir la section [mesures disponibles](#available-metrics) pour plus d’informations).

Chaque widget affiche un graphique linéaire qui compare les chiffres réels de votre entreprise au total disponible avec les licences de votre entreprise et fournit un pourcentage de l’utilisation totale.

![](../images/license-usage/widgets.png)

## Mesures disponibles

Le tableau de bord de l’utilisation des licences répertorie quatre mesures clés, avec d’autres mesures à ajouter dans les versions suivantes. Les mesures disponibles sont les suivantes :

* [!UICONTROL Audience adressable]
* [!UICONTROL Richesse moyenne du profil]
* [!UICONTROL Ratio de segmentation des données analysées]
* [!UICONTROL Stockage total consommé]

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par votre entreprise. Pour obtenir des définitions détaillées de chaque mesure, reportez-vous à la documentation appropriée Description du produit :

| Licence | Description du produit |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, services d’application et services intelligents](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMOMENT DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 50M</li></ul> | [Plateforme de données clients en temps réel](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>ACTIVATION AEP:OD</li><li>AEP:OD ACTIVATION PRFL À 10M</li><li>AEP:PRFL D’ACTIVATION OD JUSQU’À 50 M</li></ul> | [Activation de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELLIGENCE OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

>[!WARNING]
>
>Le tableau de bord de l’utilisation des licences ne tient compte que de la dernière licence configurée pour votre entreprise. Si la dernière licence configurée pour votre entreprise n’apparaît pas dans le tableau ci-dessus, le tableau de bord de l’utilisation des licences peut ne pas s’afficher correctement. La prise en charge de licences supplémentaires et de plusieurs licences au sein d’une même organisation est prévue pour une version ultérieure.

## Étapes suivantes

Après avoir lu ce document, vous pouvez localiser le tableau de bord de l’utilisation des licences et sélectionner un environnement de test à afficher. Vous trouverez également plus d’informations sur les mesures disponibles pour votre entreprise, en fonction des licences acquises par votre entreprise.

Pour en savoir plus sur les autres fonctionnalités disponibles dans l’interface utilisateur de l’Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur de Platform](../../landing/ui-guide.md).
