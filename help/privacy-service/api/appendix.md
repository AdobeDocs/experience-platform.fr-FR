---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identité acceptée  et qualificateurs
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Annexe

##  d&#39;identité standard 

Toutes les identités envoyées au Service de la protection des renseignements personnels doivent être fournies sous une  d&#39;identité spécifique . Les  d’identité sont un composant d’ [Adobe Experience Platform Identity Service](../../identity-service/home.md) qui indique le contexte auquel une identité se rapporte.

Le tableau suivant présente plusieurs types d’identité prédéfinis couramment utilisés, rendus disponibles par Experience Platform, ainsi que leurs `namespace` valeurs associées :

| Type d’identité | `namespace` | `namespaceId` |
| --- | --- | --- |
| Courriel | Courriel | 6 |
| Téléphone | Téléphone | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| UID d’Adobe   Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe ID | TNTID | 9 |
| ID Apple pour les annonceurs | IDFA | 20915 |
| Identifiant de publicité Google | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] Chaque type d’identité possède également une valeur `namespaceId` entière, qui peut être utilisée à la place de la `namespace` chaîne lors de la définition de la `type` propriété de l’identité sur &quot;namespaceId&quot;. Pour plus d’informations, reportez-vous à la section sur [qualificateurs](#namespace-qualifiers) de.

Vous pouvez récupérer un  d’identité  en cours d’utilisation par votre organisation en envoyant une requête GET au point de `idnamespace/identities` fin dans l’API Identity Service. Pour plus d&#39;informations, consultez le guide [du développeur](../../identity-service/api/getting-started.md) Identity Service.

##  qualificatifs 

Lors de la spécification d’une `namespace` valeur dans l’API de Privacy Service, un qualificateur **de  de** doit être inclus dans un `type` paramètre correspondant. Le tableau ci-dessous présente les différents qualificatifs  acceptés .

| Qualificateur | Définition |
| --------- | ---------- |
| standard | L’un des  standard  défini globalement, et non lié à un jeu de données d’entreprise individuel (par exemple, courrier électronique, numéro de téléphone, etc.).   ID de est fourni. |
| personnalisé |  unique  créé dans le contexte d’une organisation et non partagé dans Experience Cloud. La valeur représente le nom convivial (champ &quot;nom&quot;) à rechercher.   ID de est fourni. |
| integrationCode | Code d’intégration - similaire à &quot;personnalisé&quot;, mais spécifiquement défini comme code d’intégration d’une source de données à rechercher.   ID de est fourni. |
| namespaceId | Indique que la valeur correspond à l’ID réel de l’ de  qui a été créé ou mappé via le service de . |
| non enregistré | Chaîne de forme libre qui n’est pas définie dans le service de   et qui est prise &quot;en l’état&quot;. Toute application qui gère ce type de   vérifie et traite les données en fonction du contexte et de l&#39;ensemble de données de la  de. Aucun   ID de n’est fourni. |
| analytics |  personnalisé qui est mappé en interne dans Analytics, et non dans le service de . Elle est transmise directement comme spécifié par la requête d’origine, sans ID de  |
| cible | Un  personnalisé  compris en interne par les, et non dans le service de. Elle est transmise directement comme spécifié par la requête d’origine, sans ID de  |

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
| Service d’enregistrement des clients | &quot;CRS&quot; |
| Profil client en temps réel | &quot;ProfileService&quot; |