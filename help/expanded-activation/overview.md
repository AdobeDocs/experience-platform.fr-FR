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

Basée sur Adobe Experience Platform, l’Audience Manager de l’activation étendue aide les [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) les utilisateurs activent leur audience vers [social](../destinations/catalog/social/overview.md) et [publicité](../destinations/catalog/advertising/overview.md) plateformes de destination de Real-Time CDP, telles que [Facebook](../destinations/catalog/social/facebook.md), [Publicités Google](../destinations/catalog/advertising/google-ads-destination.md), etc.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] est uniquement disponible pour les [!DNL Audience Manager] utilisateurs.

## Terminologie {#terminology}

L’activation étendue d’Audience Manager utilise des concepts et des composants de Adobe Experience Platform. Pour mieux comprendre le workflow d’activation étendue et les composants que vous allez utiliser, assurez-vous d’avoir une compréhension de base des concepts suivants :

* [Audiences](../segmentation/ui/overview.md): les audiences sont des ensembles de personnes qui partagent des comportements et/ou des caractéristiques similaires. Cette collection de personnes peut être générée par Adobe Experience Platform à l’aide de définitions de segment ou de composition d’audience (audience générée par Platform) ou à partir de sources externes telles que les téléchargements personnalisés (audience générée en externe). Dans l’activation étendue, vos segments d’Audience Manager (audiences) sont importés en tant que [chargements personnalisés](../segmentation/ui/audience-portal.md#import-audience).
* [Connecteurs Source](../sources/home.md): les connecteurs Source (également appelés sources) aident les utilisateurs Experience Platform à ingérer facilement des données provenant de plusieurs sources, ce qui permet de structurer, d’étiqueter et d’améliorer les données à l’aide des services Experience Platform. Les données peuvent être ingérées à partir de différentes sources, comme le stockage dans le cloud, les logiciels tiers et les systèmes de gestion de la relation client.
* [Connecteurs de destination](../destinations/home.md): les destinations décrivent n’importe quel point de terminaison, tel qu’une application d’Adobe, une plateforme publicitaire, un service de stockage dans le cloud ou un service marketing, où une audience est activée et diffusée. [!DNL Expanded Activation] prend en charge l’activation des audiences vers [publicité](../destinations/catalog/advertising/overview.md) et [social](../destinations/catalog/social/overview.md) connecteurs de destination.

## Conditions préalables {#prerequisites}

Avant d’activer les audiences par le biais de l’activation étendue, assurez-vous de respecter les conditions préalables décrites ci-dessous.

### Exigences des utilisateurs et rôles {#permission-requirements}

Avant d’utiliser [!DNL Expanded Activation], vous devez créer un compte utilisateur à partir de l’Admin Console et l’affecter à la variable [!DNL Expanded Activation] rôle. Voir [administration](administration.md) pour obtenir des instructions détaillées sur la manière de procéder.

### Exigences d’audience {#audience-requirements}

Pour activer des audiences par le biais de [!DNL Expanded Activation], assurez-vous que les audiences de votre Audience Manager sont basées sur **adresses électroniques hachées**. Pour ce faire, deux méthodes sont possibles en fonction de l’utilisation de votre Audience Manager :

* Si vous utilisez la variable [Audience Manager de destinations basées sur les personnes](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) , vous ingérez déjà des adresses électroniques hachées dans Audience Manager. Dans ce cas, aucune autre étape n’est nécessaire. Vous pouvez passer à [activation d’audiences par le biais d’une activation étendue](activate-audiences.md).
* Si vous _not_ en utilisant la variable [Audience Manager de destinations basées sur les personnes](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) , vous devez créer une source de données dans Audience Manager et l’utiliser pour stocker les adresses électroniques hachées. Consultez la documentation relative à [configuration d’une source de données pour les workflows de courrier électronique haché](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) pour apprendre à le faire. Après avoir ingéré des adresses électroniques hachées dans votre source de données d’Audience Manager, lisez la documentation sur [activation d’audiences par le biais d’une activation étendue](activate-audiences.md).

## Étapes suivantes {#next-steps}

Maintenant que vous comprenez mieux les cas d’utilisation et les avantages de l’utilisation de [!DNL Expanded Activation], démarrez [configuration de votre compte](administration.md) puis [activation de vos audiences](activate-audiences.md).
