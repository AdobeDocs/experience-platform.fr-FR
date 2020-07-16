---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualificateurs et espaces de noms d’identité acceptés
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 87%

---


# Annexe

## Espaces de noms d’identité standard {#standard-namespaces}

All identities that are sent to [!DNL Privacy Service] must be provided under a specific identity namespace. Les espaces de noms d’identité sont des composants [Adobe Experience Platform Identity Service](../../identity-service/home.md) qui servent d’indicateurs du contexte auquel une identité se rapporte.

The following table outlines several commonly used, pre-defined identity types made available by [!DNL Experience Platform], along with their associated `namespace` values:

| Type d’identité | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | E-mail | 6 |
| Téléphone | Téléphone | 7 |
| Identifiant Adobe Advertising Cloud | AdCloud | 411 |
| UUID Adobe Audience Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Identifiant Adobe Target | TNTID | 9 |
| [!DNL Apple] Identifiant pour les annonceurs | IDFA | 20915 |
| [!DNL Google] Identifiant de publicité | GAID | 20914 |
| [!DNL Windows] AIDE | WAID | 8 |

>[!NOTE]
>
> Chaque type d’identité possède également une valeur entière `namespaceId`, qui peut être utilisée à la place de la chaîne `namespace` lorsque la propriété `type` de l’identité est « namespaceId ». Pour plus d’informations, consultez la section sur les [qualificateurs d’espace de noms](#namespace-qualifiers).

Vous pouvez récupérer une liste des espaces de noms d’identité utilisés par votre organisation en exécutant une requête GET sur le point de terminaison `idnamespace/identities` dans l’API [!DNL Identity Service] Pour plus d’informations, consultez le [guide de développement d’Identity Service](../../identity-service/api/getting-started.md).

## Qualificateurs d’espace de noms

Lors de la spécification d’une valeur `namespace`[!DNL Privacy Service] dans l’API , un **qualificateur d’espace de noms** doit être inclus dans un paramètre `type` correspondant. Le tableau suivant présente les différents qualificateurs d’espace de noms acceptés.

| Qualificateur | Définition |
| --------- | ---------- |
| standard | Un des espaces de noms standard définis globalement, non lié à un jeu de données d’une organisation individuelle (par exemple, e-mail, numéro de téléphone, etc.). L’identifiant d’espace de noms est fourni. |
| custom | Espace de noms unique créé dans le contexte d’une organisation et non partagé dans [!DNL Experience Cloud]. La valeur représente le nom convivial (champ « nom ») à rechercher. L’identifiant d’espace de noms est fourni. |
| integrationCode | Code d’intégration, similaire à « custom », mais spécifiquement défini comme le code d’intégration d’une source de données à rechercher. L’identifiant d’espace de noms est fourni. |
| namespaceId | Indique que la valeur correspond à l’identifiant réel de l’espace de noms créé ou mappé via le service d’espace de noms. |
| unregistered | Chaîne de forme libre non définie dans le service d’espace de noms et prise « en l’état ». Toute application qui gère ces types d’espaces de noms les compare et les traite en fonction du contexte de l’entreprise et du jeu de données. Aucun identifiant d’espace de noms n’est fourni. |
| analytics | A custom namespace that is mapped internally in [!DNL Analytics], not in the namespace service. Il est transmis directement comme indiqué dans la requête d’origine, sans identifiant d’espace de noms. |
| target | A custom namespace understood internally by [!DNL Target], not in the namespace service. Il est transmis directement comme indiqué dans la requête d’origine, sans identifiant d’espace de noms. |

## Valeurs de produit acceptées

Le tableau suivant indique les valeurs acceptées pour la spécification d’un produit Adobe dans l’attribut `include` d’une requête de création de tâche.

| Produit | Valeur à utiliser dans l’attribut `include` |
--- | ---
| Adobe Advertizing Cloud | « AdCloud » |
| Adobe Analytics | « Analytics » |
| Adobe Audience Manager | « AudienceManager » |
| Adobe Campaign | « Campaign » |
| Adobe Experience Platform | « aepDataLake » |
| Adobe Primetime Authentication | « primetimeAuthentication » |
| Adobe Target | « Target » |
| Customer Record Service | « CRS » |
| Real-time Customer Profile | « ProfileService » |