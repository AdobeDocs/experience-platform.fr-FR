---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Annexe du guide de l’API Privacy Service
description: Ce document contient des informations supplémentaires sur l’utilisation de l’API Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 57%

---

# Annexe du guide de l’API Privacy Service

Les sections suivantes contiennent des informations supplémentaires sur l’utilisation de l’API Adobe Experience Platform Privacy Service.

## Espaces de noms d’identité standard {#standard-namespaces}

Toutes les identités envoyées à [!DNL Privacy Service] doivent être fournies sous un espace de noms d’identité spécifique. Les espaces de noms d’identité sont des composants du [service d’identités d’Adobe Experience Platform](../../identity-service/home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte.

Le tableau suivant décrit plusieurs types d’identité prédéfinis couramment utilisés, mis à disposition par [!DNL Experience Platform], ainsi que les valeurs `namespace` qui leur sont associées :

| Type d’identité | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | `Email` | `6` |
| Téléphone | `Phone` | `7` |
| Identifiant Adobe Advertising Cloud | `AdCloud` | `411` |
| UUID Adobe Audience Manager | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Identifiant Adobe Target | `TNTID` | `9` |
| [!DNL Apple] ID pour les annonceurs | `IDFA` | `20915` |
| [!DNL Google] ID de publicité | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Chaque type d’identité possède également une valeur `namespaceId` entière, qui peut être utilisée à la place de la chaîne `namespace` lors de la définition de la propriété `type` de l’identité sur &quot;namespaceId&quot;. Pour plus d’informations, consultez la section sur les [qualificateurs d’espace de noms](#namespace-qualifiers).

Vous pouvez récupérer une liste des espaces de noms d’identité utilisés par votre organisation en envoyant une requête GET au point de terminaison `idnamespace/identities` dans l’API [!DNL Identity Service]. Pour plus d’informations, consultez le [guide de développement du service d’identités](../../identity-service/api/getting-started.md).

## Qualificateurs d’espace de noms

Lors de la spécification d’une valeur `namespace` dans l’API [!DNL Privacy Service], un **qualificateur d’espace de noms** doit être inclus dans un paramètre `type` correspondant. Le tableau suivant présente les différents qualificateurs d’espace de noms acceptés.

| Qualificateur | Définition |
| --------- | ---------- |
| `standard` | Un des espaces de noms standard définis globalement, non lié à un jeu de données d’une organisation individuelle (par exemple, e-mail, numéro de téléphone, etc.). L’identifiant d’espace de noms est fourni. |
| `custom` | Espace de noms unique créé dans le contexte d’une organisation, non partagé dans l’ensemble de [!DNL Experience Cloud]. La valeur représente le nom convivial (champ « nom ») à rechercher. L’identifiant d’espace de noms est fourni. |
| `integrationCode` | Code d’intégration, similaire à « custom », mais spécifiquement défini comme le code d’intégration d’une source de données à rechercher. L’identifiant d’espace de noms est fourni. |
| `namespaceId` | Indique que la valeur correspond à l’identifiant réel de l’espace de noms créé ou mappé via le service d’espace de noms. |
| `unregistered` | Chaîne de forme libre non définie dans le service d’espace de noms et prise « en l’état ». Toute application qui gère ces types d’espaces de noms les compare et les traite en fonction du contexte de l’entreprise et du jeu de données. Aucun identifiant d’espace de noms n’est fourni. |
| `analytics` | Espace de noms personnalisé mappé en interne dans [!DNL Analytics], et non dans le service d’espace de noms. Il est transmis directement comme indiqué dans la requête d’origine, sans identifiant d’espace de noms. |
| `target` | Un espace de noms personnalisé compris en interne par [!DNL Target], et non dans le service d’espace de noms. Il est transmis directement comme indiqué dans la requête d’origine, sans identifiant d’espace de noms. |

{style="table-layout:auto"}

## Valeurs de produit acceptées

Le tableau suivant indique les valeurs acceptées pour la spécification d’un produit Adobe dans l’attribut `include` d’une requête de création de tâche.

>[!NOTE]
>
>Les valeurs de la liste de produits ne sont pas sensibles à la casse. La casse Camel est recommandée mais n’est pas appliquée.

| Produit | Valeur à utiliser dans l’attribut `include` |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (lac de données) | `aepDataLake` |
| Adobe Experience Platform (profil client en temps réel) | `profileService` |
| Authentification Adobe Pass | `primetimeAuthentication` |
| Adobe Target | `target` |
| Attributs du client (CRS) | `CRS` |
| Gestion des Parcours clients | `cjm` |
| Service d’identités | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
