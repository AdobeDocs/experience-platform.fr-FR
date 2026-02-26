---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Annexe du guide de l’API Privacy Service
description: Ce document contient des informations supplémentaires sur l’utilisation de l’API Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 9b3fb0d545408369d96a3fc7c5c6e9c098af9933
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 47%

---

# Annexe du guide de l’API Privacy Service

Les sections suivantes contiennent des informations supplémentaires sur l’utilisation de l’API Adobe Experience Platform Privacy Service.

## Espaces de noms d’identité standard {#standard-namespaces}

Toutes les identités envoyées à [!DNL Privacy Service] doivent être fournies sous un espace de noms d’identité spécifique. Les espaces de noms d’identité sont des composants du [service d’identités d’Adobe Experience Platform](../../identity-service/home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte.

Le tableau suivant présente plusieurs types d’identité prédéfinis couramment utilisés, mis à disposition par [!DNL Experience Platform], ainsi que les valeurs de `namespace` qui leur sont associées :

| Type d’identité | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | `Email` | `6` |
| Téléphone | `Phone` | `7` |
| Identifiant Adobe Advertising Cloud | `AdCloud` | `411` |
| UUID Adobe Audience Manager | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Identifiant Adobe Target | `TNTID` | `9` |
| ID de [!DNL Apple] pour les annonceurs | `IDFA` | `20915` |
| ID de publicité [!DNL Google] | `GAID` | `20914` |
| AIDE [!DNL Windows] | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Chaque type d’identité possède également une valeur entière `namespaceId`, qui peut être utilisée à la place de la chaîne de `namespace` lors de la définition de la propriété `type` de l’identité sur « namespaceId ». Pour plus d’informations, consultez la section sur les [qualificateurs d’espace de noms](#namespace-qualifiers).

Vous pouvez récupérer une liste d’espaces de noms d’identité utilisés par votre organisation en envoyant une requête GET au point d’entrée `idnamespace/identities` dans l’API [!DNL Identity Service]. Pour plus d’informations, consultez le [guide de développement du service d’identités](../../identity-service/api/getting-started.md).

## Qualificateurs d’espace de noms {#namespace-qualifiers}

Lors de la spécification d’une valeur de `namespace` dans l’API [!DNL Privacy Service], un **qualificateur d’espace de noms** doit être inclus dans un paramètre de `type` correspondant. Le tableau suivant présente les différents qualificateurs d’espace de noms acceptés.

| Qualificateur | Définition |
| --------- | ---------- |
| `standard` | Un des espaces de noms standard définis globalement, non lié à un jeu de données d’une organisation individuelle (par exemple, e-mail, numéro de téléphone, etc.). L’identifiant d’espace de noms est fourni. |
| `custom` | Espace de noms unique créé dans le contexte d’une organisation et non partagé dans l’[!DNL Experience Cloud]. La valeur représente le nom convivial (champ « nom ») à rechercher. L’identifiant d’espace de noms est fourni. |
| `integrationCode` | Code d’intégration, similaire à « custom », mais spécifiquement défini comme le code d’intégration d’une source de données à rechercher. L’identifiant d’espace de noms est fourni. |
| `namespaceId` | Indique que la valeur correspond à l’identifiant réel de l’espace de noms créé ou mappé via le service d’espace de noms. |
| `unregistered` | Chaîne de forme libre non définie dans le service d’espace de noms et prise « en l’état ». Toute application qui gère ces types d’espaces de noms les compare et les traite en fonction du contexte de l’entreprise et du jeu de données. Aucun identifiant d’espace de noms n’est fourni. |
| `analytics` | Un espace de noms personnalisé qui est mappé en interne dans [!DNL Analytics], et non dans le service d’espace de noms. Il est transmis directement comme indiqué dans la requête d’origine, sans identifiant d’espace de noms. |
| `target` | Un espace de noms personnalisé compris en interne par [!DNL Target], et non dans le service d’espace de noms. Il est transmis directement comme indiqué dans la requête d’origine, sans identifiant d’espace de noms. |

{style="table-layout:auto"}

## Valeurs de produit acceptées {#accepted-product-values}

Cette section répertorie les valeurs d’identifiant de produit acceptées dans l’attribut `include` lors de la création de tâches Privacy Service (API ou interface utilisateur). Utilisez ces valeurs dans le tableau `include` de votre demande de traitement.

Le tableau suivant répertorie les produits pris en charge, les noms d’affichage de l’interface utilisateur et les valeurs de code correspondantes.

>[!NOTE]
>
>- Les valeurs de produit ne respectent pas la casse. Pour des raisons de cohérence, il est recommandé d’utiliser la casse mixte .
>- Seuls les produits répertoriés ci-dessus sont pris en charge dans l’interface utilisateur et l’API . Si un produit n’est pas configuré pour votre organisation, il peut être ignoré ou entraîner une erreur de validation. Consultez votre contrat Adobe ou la documentation de configuration pour confirmer les droits.

| Nom du produit de marque | Nom d’affichage de l’interface utilisateur | Valeur `include` |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (banque de profils) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform (lac de données) | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| Attributs du client ou de la cliente | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| Service d’identités | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
