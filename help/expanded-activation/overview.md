---
title: Activation étendue d’Audience Manager
description: Découvrez comment activer les audiences Audience Manager vers des destinations sociales et publicitaires, via l’activation étendue d’Audience Manager.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 6%

---

# Activation étendue d’Audience Manager

Basée sur Adobe Experience Platform, l’activation étendue d’Audience Manager aide les utilisateurs [Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/aam-home) existants à activer leurs audiences vers des plateformes de destination [sociales](../destinations/catalog/social/overview.md) et [publicitaires](../destinations/catalog/advertising/overview.md) à partir de Real-Time CDP, telles que [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md), etc.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] n’est disponible que pour les utilisateurs et utilisatrices [!DNL Audience Manager] existants.

## Terminologie {#terminology}

L’activation étendue d’Audience Manager utilise des concepts et des composants de Adobe Experience Platform. Pour mieux comprendre le workflow d’activation développée et les composants que vous utiliserez, assurez-vous de posséder une compréhension de base des concepts suivants :

* [Audiences](../segmentation/ui/overview.md) : les audiences sont des ensembles de personnes qui partagent des comportements et/ou des caractéristiques similaires. Cette collection de personnes peut être générée par Adobe Experience Platform à l’aide des définitions de segment ou de la composition de l’audience (audience générée par Experience Platform) ou à partir de sources externes telles que des chargements personnalisés (audience générée en externe). Dans l’activation développée, vos segments Audience Manager (audiences) sont importés en tant que [chargements personnalisés](../segmentation/ui/audience-portal.md#import-audience).
* [Connecteurs Source &#x200B;](../sources/home.md) : les connecteurs Source (également appelés sources) aident les utilisateurs Experience Platform à ingérer facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide des services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.
* [Connecteurs de destination](../destinations/home.md) : les destinations décrivent tout point d’entrée (application Adobe, plateforme publicitaire, service de stockage dans le cloud ou service marketing, par exemple) où une audience est activée et diffusée. [!DNL Expanded Activation] prend en charge l’activation des audiences vers les connecteurs de destination [advertising](../destinations/catalog/advertising/overview.md) et [social](../destinations/catalog/social/overview.md).

## Conditions préalables {#prerequisites}

Avant d’activer des audiences par le biais de l’activation étendue, veillez à respecter les conditions préalables décrites ci-dessous.

### Exigences relatives aux utilisateurs et aux rôles {#permission-requirements}

Avant de pouvoir utiliser [!DNL Expanded Activation], vous devez créer un compte utilisateur à partir d’Admin Console et l’affecter au rôle [!DNL Expanded Activation]. Voir la page [administration](administration.md) pour obtenir des instructions détaillées sur la manière de procéder.

### Exigences en matière d’audience {#audience-requirements}

Pour activer des audiences par le biais de [!DNL Expanded Activation], assurez-vous que vos audiences Audience Manager sont basées sur des adresses e-mail **hachées**. Pour ce faire, il existe deux manières, en fonction de votre utilisation d’Audience Manager :

* Si vous utilisez la fonctionnalité [Destinations basées sur les individus d’Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), vous ingérez déjà des adresses e-mail hachées dans Audience Manager. Il n’y a aucune étape supplémentaire à franchir dans ce cas. Vous pouvez passer à [activation des audiences via l’activation étendue](activate-audiences.md).
* Si vous n’utilisez _pas_ la fonctionnalité [Destinations basées sur les individus d’Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), vous devez créer une nouvelle source de données dans Audience Manager et l’utiliser pour stocker les adresses e-mail hachées. Pour découvrir comment procéder, consultez la documentation sur la [configuration d’une source de données pour les workflows d’e-mail hachés](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails). Après avoir ingéré des adresses e-mail hachées dans votre source de données Audience Manager, lisez la documentation sur l’[activation des audiences via l’activation étendue](activate-audiences.md).

## Étapes suivantes {#next-steps}

Maintenant que vous comprenez mieux les cas d’utilisation et les avantages de l’utilisation de [!DNL Expanded Activation], commencez par [configurer votre compte](administration.md) puis [activer vos audiences](activate-audiences.md).
