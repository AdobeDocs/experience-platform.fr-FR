---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: espaces de nommage et qualificatifs d'identité acceptés
topic: developer guide
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# Annexe

## espaces de nommage d&#39;identité standard {#standard-namespaces}

Toutes les identités envoyées à Privacy Service doivent être fournies sous un espace de nommage d&#39;identité spécifique. Les espaces de nommage d’identité sont un composant d’ [Adobe Experience Platform Identity Service](../../identity-service/home.md) qui indique le contexte auquel une identité se rapporte.

Le tableau suivant présente plusieurs types d’identité prédéfinis couramment utilisés, rendus disponibles par Experience Platform, ainsi que les `namespace` valeurs associées :

| Type d&#39;identité | `namespace` | `namespaceId` |
| --- | --- | --- |
| Courriel | Courriel | 6 |
| Téléphone | Téléphone | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| UID Adobe Audience Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Cible ID | TNTID | 9 |
| ID Apple pour les annonceurs | IDFA | 20915 |
| Identifiant de publicité Google | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] Chaque type d&#39;identité possède également une valeur `namespaceId` entière, qui peut être utilisée à la place de la `namespace` chaîne lors de la définition de la propriété `type` de l&#39;identité sur &quot;namespaceId&quot;. Pour plus d&#39;informations, consultez la section relative aux qualificatifs [d&#39;](#namespace-qualifiers) espace de nommage.

Vous pouvez récupérer une liste d’espaces de nommage d’identité utilisée par votre organisation en adressant une demande GET au point de `idnamespace/identities` terminaison dans l’API Identity Service. Pour plus d&#39;informations, consultez le guide [du développeur](../../identity-service/api/getting-started.md) Identity Service.

## Qualificateurs d&#39;Espace de nommage

Lors de la spécification d’une `namespace` valeur dans l’API de Privacy Service, un qualificateur **d’** espace de nommage doit être inclus dans un `type` paramètre correspondant. Le tableau suivant présente les différents qualificatifs d&#39;espace de nommage acceptés.

| Qualificateur | Définition |
| --------- | ---------- |
| standard | L’un des espaces de nommage standard est défini globalement, et non lié à un jeu de données d’entreprise individuel (par exemple, courriel, numéro de téléphone, etc.). L’ID d’Espace de nommage est fourni. |
| personnalisé | espace de nommage unique créé dans le contexte d’une organisation et non partagé dans Experience Cloud. La valeur représente le nom convivial (champ &quot;nom&quot;) à rechercher. L’ID d’Espace de nommage est fourni. |
| integrationCode | Code d’intégration - similaire à &quot;personnalisé&quot;, mais spécifiquement défini comme code d’intégration d’une source de données à rechercher. L’ID d’Espace de nommage est fourni. |
| namespaceId | Indique que la valeur correspond à l’identifiant réel de l’espace de nommage qui a été créé ou mappé via le service d’espace de nommage. |
| non enregistré | Chaîne de forme libre qui n’est pas définie dans le service d’espace de nommage et qui est prise &quot;en l’état&quot;. Toute application qui gère ce type d’espace de nommage vérifie ces  et les gère si nécessaire en fonction du contexte de société et de l’ensemble de données. Aucun ID d’espace de nommage n’est fourni. |
| analytics | espace de nommage personnalisé qui est mappé en interne dans Analytics et non dans le service d’espace de nommage. Elle est transmise directement, comme spécifié par la requête d’origine, sans ID d’espace de nommage. |
| cible | espace de nommage personnalisé compris en interne par la Cible et non dans le service d’espace de nommage. Elle est transmise directement, comme spécifié par la requête d’origine, sans ID d’espace de nommage. |

## Valeurs de produit acceptées

Le tableau suivant décrit les valeurs acceptées pour la spécification d’un produit Adobe dans l’ `include` attribut d’une demande de création d’emploi.

| Produit | Valeur à utiliser dans l’ `include` attribut |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Authentification Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Service d&#39;enregistrement des clients | &quot;CRS&quot; |
| Profil client en temps réel | &quot;ProfileService&quot; |