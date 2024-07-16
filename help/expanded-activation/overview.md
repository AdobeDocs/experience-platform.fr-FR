---
title: Activation étendue d’Audience Manager
description: Découvrez comment activer les audiences d’Audience Manager vers les destinations publicitaires et sociales par le biais de l’activation étendue de l’Audience Manager.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 6%

---

# Activation étendue d’Audience Manager

Basée sur Adobe Experience Platform, l’activation étendue d’Audience Manager aide les utilisateurs existants [d’Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) à activer leurs audiences sur les plateformes de destination [social](../destinations/catalog/social/overview.md) et [publicité](../destinations/catalog/advertising/overview.md) à partir de Real-Time CDP, telles que [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md), etc.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] n&#39;est disponible que pour les utilisateurs [!DNL Audience Manager] existants.

## Terminologie {#terminology}

L’activation étendue d’Audience Manager utilise des concepts et des composants de Adobe Experience Platform. Pour mieux comprendre le workflow d’activation étendue et les composants que vous allez utiliser, assurez-vous d’avoir une compréhension de base des concepts suivants :

* [Audiences](../segmentation/ui/overview.md) : les audiences sont des ensembles de personnes qui partagent des comportements et/ou des caractéristiques similaires. Cette collection de personnes peut être générée par Adobe Experience Platform à l’aide de définitions de segment ou de composition d’audience (audience générée par Platform) ou à partir de sources externes telles que les téléchargements personnalisés (audience générée en externe). Dans l’activation étendue, vos segments d’Audience Manager (audiences) sont importés sous la forme de [chargements personnalisés](../segmentation/ui/audience-portal.md#import-audience).
* [Connecteurs Source](../sources/home.md) : les connecteurs Source (également appelés sources) aident les utilisateurs Experience Platform à ingérer facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide des services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.
* [Connecteurs de destination](../destinations/home.md) : les destinations décrivent n’importe quel point de terminaison, tel qu’une application d’Adobe, une plateforme publicitaire, un service de stockage dans le cloud ou un service marketing, où une audience est activée et diffusée. [!DNL Expanded Activation] prend en charge l’activation des audiences vers les connecteurs de destination [advertising](../destinations/catalog/advertising/overview.md) et [social](../destinations/catalog/social/overview.md).

## Conditions préalables {#prerequisites}

Avant d’activer les audiences par le biais de l’activation étendue, assurez-vous de respecter les conditions préalables décrites ci-dessous.

### Exigences des utilisateurs et rôles {#permission-requirements}

Avant de pouvoir utiliser [!DNL Expanded Activation], vous devez créer un compte utilisateur à partir de l’Admin Console et l’affecter au rôle [!DNL Expanded Activation]. Consultez la page [administration](administration.md) pour obtenir des instructions détaillées sur la façon de procéder.

### Exigences d’audience {#audience-requirements}

Pour activer les audiences par le biais de [!DNL Expanded Activation], assurez-vous que les audiences de votre Audience Manager sont basées sur des **adresses électroniques hachées**. Pour ce faire, deux méthodes sont possibles en fonction de l’utilisation de votre Audience Manager :

* Si vous utilisez la fonctionnalité [Audience Manager People-based Destinations](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), vous ingérez déjà des adresses électroniques hachées dans Audience Manager. Dans ce cas, aucune autre étape n’est nécessaire. Vous pouvez passer à l’[activation d’audiences par le biais de l’activation étendue](activate-audiences.md).
* Si vous _n’utilisez pas_ la fonctionnalité [Audience Manager People-based Destinations](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), vous devez créer une source de données dans Audience Manager et l’utiliser pour stocker les adresses électroniques hachées. Consultez la documentation sur la [configuration d’une source de données pour les workflows de messagerie hachée](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) pour savoir comment le faire. Une fois que vous avez ingéré des adresses électroniques hachées dans votre source de données d’Audience Manager, lisez la documentation sur l’ [activation d’audiences par le biais de l’activation étendue](activate-audiences.md).

## Étapes suivantes {#next-steps}

Maintenant que vous connaissez les cas pratiques et les avantages de l&#39;utilisation de [!DNL Expanded Activation], commencez [à configurer votre compte](administration.md), puis [activez vos audiences](activate-audiences.md).
