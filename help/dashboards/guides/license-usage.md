---
keywords: Experience Platform ; interface utilisateur ; interface utilisateur ; personnalisation ; tableau de bord d’utilisation des licences ; tableau de bord ; utilisation des licences ; droits ; consommation
title: Tableau de bord d'utilisation des licences
description: Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur l’utilisation des licences de votre entreprise.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 3908011b31dd24b13a58a2bc5ad5137dd3af5f63
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 4%

---


# (bêta) tableau de bord d&#39;utilisation de la licence {#license-usage-dashboard}

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord décrite dans ce document est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez vue des informations importantes sur l’utilisation des licences de votre entreprise, telles qu’elles sont capturées au cours d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord d’utilisation des licences dans l’interface utilisateur et comment l’utiliser. Il fournit également plus d’informations sur les visualisations affichées dans le tableau de bord.

Pour un aperçu général de l’interface utilisateur de la plate-forme, consultez le [guide de l’interface utilisateur Experience Platform](../../landing/ui-guide.md).

## Données du tableau de bord d&#39;utilisation de la licence

Le tableau de bord d’utilisation des licences affiche un instantané des données relatives aux licences de votre entreprise pour l’Experience Platform. Les données du tableau de bord s&#39;affichent exactement comme elles s&#39;affichent au moment précis où l&#39;instantané a été pris. En d&#39;autres termes, l&#39;instantané n&#39;est pas une approximation ou un échantillon des données et le tableau de bord n&#39;est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis l&#39;instantané ne seront pas répercutées dans le tableau de bord tant que l&#39;instantané suivant n&#39;aura pas été pris.

## Exploration du tableau de bord d’utilisation des licences

Pour accéder au tableau de bord d’utilisation des licences dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Utilisation des licences]** dans le rail de gauche. Cette opération s’ouvre avec l’onglet **[!UICONTROL Aperçu]** qui affiche le tableau de bord.

![](../images/license-usage/dashboard-overview.png)

### Sélectionner un sandbox

Pour choisir un sandbox à vue dans le tableau de bord, sélectionnez [!UICONTROL Production] ou [!UICONTROL Développement]. Le sandbox sélectionné est indiqué par le bouton radio en regard du nom du sandbox.

>[!NOTE]
>
>Le rapports de consommation des sandbox est cumulé pour tous les sandbox du même type. En d’autres termes, la sélection de [!UICONTROL Production] ou [!UICONTROL Développement] fournit des rapports de consommation pour tous les sandbox de production ou de développement, respectivement.

![](../images/license-usage/select-sandbox.png)

### Sélectionner une plage de dates

Après avoir sélectionné un sandbox, vous pouvez utiliser la liste déroulante de plage de dates pour sélectionner la période à afficher dans le tableau de bord. Trois options sont disponibles : [!UICONTROL 30 derniers jours], [!UICONTROL 90 derniers jours] et [!UICONTROL 12 derniers mois]. Les 30 derniers jours sont sélectionnés par défaut.

![](../images/license-usage/select-date-range.png)

## Widgets

Le tableau de bord d’utilisation des licences est composé de widgets qui affichent des mesures en lecture seule fournissant des informations importantes sur l’utilisation des licences de votre entreprise. Les mesures visibles dépendent de la licence spécifique de votre entreprise (voir la section [mesures disponibles](#available-metrics) pour plus de détails).

Chaque widget affiche un graphique linéaire qui compare les chiffres réels de votre entreprise au total disponible avec les licences de votre entreprise et fournit un pourcentage de l’utilisation totale.

![](../images/license-usage/widgets.png)

## Mesures disponibles

Le tableau de bord d’utilisation des licences comprend actuellement quatre mesures :

* [!UICONTROL Audience]  adressable (mesurée par le nombre de profils)
* [!UICONTROL Richesse moyenne du profil]
* [!UICONTROL Enregistrement total consommé]
* [!UICONTROL Taux de segmentation des données analysées]

La définition de chacune de ces mesures varie en fonction des licences achetées par votre entreprise. Pour obtenir des définitions détaillées de chaque mesure, veuillez consulter la documentation appropriée sur la description du produit :

| Licence | Description du produit |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD LOURD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>RT CLIENT DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 50M</li></ul> | [Plateforme de données clients en temps réel](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL to 10M</li><li>AEP:OD ACTIVATION PRFL JUSQU’À 50 M</li></ul> | [activation Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELLIGENCE OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## Étapes suivantes

Après avoir lu ce document, vous pouvez localiser le tableau de bord d&#39;utilisation de la licence et sélectionner un sandbox à vue. Vous pouvez également trouver d’autres informations sur les mesures disponibles pour votre entreprise, en fonction des licences achetées par votre entreprise.

Pour en savoir plus sur les autres fonctionnalités disponibles dans l’interface utilisateur de l’Experience Platform, consultez le [Guide de l’interface utilisateur de la plate-forme](../../landing/ui-guide.md).