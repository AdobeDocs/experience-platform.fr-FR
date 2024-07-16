---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des étiquettes de contrôle d’accès basé sur les attributs
description: Ce document fournit des informations sur la gestion des libellés par le biais de l’interface Autorisations dans Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 5810a7778d86db2720a0372ace33278348d1ffdf
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 37%

---

# Gérer les libellés

>[!NOTE]
>
>Pour créer ou afficher des attributs calculés avec des champs contenant un libellé donné, vous devez avoir accès à ce libellé.

Les libellés vous permettent de classer les jeux de données et les champs en fonction de l’utilisation et des stratégies d’accès qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans Platform, ou dès que les données sont disponibles pour une utilisation dans Platform.

## Créer un nouveau libellé {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Utilisation des libellés"
>abstract="Vous pouvez utiliser des libellés personnalisés pour appliquer à vos données des configurations de gouvernance des données et de contrôle d&#39;accès."

>[!NOTE]
>
>Il existe une liste unique d’étiquettes pour l’ensemble de l’organisation. Pour créer une étiquette personnalisée, vous aurez besoin des autorisations **[!UICONTROL Gérer les libellés d’utilisation]** sur l’environnement de test de production. La suppression d’étiquettes n’est actuellement pas prise en charge.

Pour créer une nouvelle étiquette, sélectionnez l’onglet **[!UICONTROL Étiquettes]** dans la barre latérale et sélectionnez **[!UICONTROL Créer une étiquette]**.

![flac-new-label](../../images/flac-ui/create-label.png)

La boîte de dialogue **[!UICONTROL Créer une étiquette]** s’affiche, vous invitant à saisir un nom, un nom convivial facultatif et une description facultative.

![new-label-info](../../images/flac-ui/new-label-info.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Confirmer]**.
