---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Traitement des demandes d’accès à des informations personnelles dans Real-time Customer Profile
type: Documentation
description: Adobe Experience Platform Privacy Service traite les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les supprimer, comme le stipulent de nombreuses réglementations de confidentialité. Ce document couvre les concepts essentiels associés au traitement des demandes d’accès à des informations personnelles pour Real-time Customer Profile.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e94482532e0c5698cfe5e51ba260f89c67fa64f0
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 30%

---

# Traitement des demandes d’accès à des informations personnelles dans [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes des clients pour accéder à leurs données personnelles, en refuser la vente ou les supprimer, comme le stipulent les réglementations de confidentialité telles que le Règlement général sur la protection des données (RGPD) et la loi [!DNL California Consumer Privacy Act] (CCPA).

Ce document couvre les concepts essentiels liés au traitement des demandes d’accès à des informations personnelles pour [!DNL Real-time Customer Profile] dans Adobe Experience Platform.

>[!NOTE]
>
>Ce guide porte uniquement sur la manière d’effectuer des demandes d’accès à des informations personnelles pour le magasin de données Profile dans Experience Platform. Si vous prévoyez également d’effectuer des demandes d’accès à des informations personnelles pour le lac de données de Platform, reportez-vous au guide sur le [traitement des demandes d’accès à des informations personnelles dans le lac de données](../catalog/privacy.md) en plus de ce tutoriel.
>
>Pour savoir comment effectuer des demandes d’accès à des informations personnelles pour d’autres applications Adobe Experience Cloud, reportez-vous à la [documentation du Privacy Service](../privacy-service/experience-cloud-apps.md).

## Prise en main

Une connaissance concrète des services [!DNL Experience Platform] suivants est recommandée avant la lecture de ce guide :

* [[!DNL Privacy Service]](../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [[!DNL Real-time Customer Profile]](home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] rapproche les données dʼidentité client entre les systèmes et les appareils. [!DNL Identity Service]**utilise les espaces de noms d’identité pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine.** Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus dʼinformations sur les espaces de noms dʼidentité dans [!DNL Experience Platform], consultez la [présentation de lʼespace de noms dʼidentité](../identity-service/namespaces.md).

## Envoi de requêtes {#submit}

Les sections ci-dessous expliquent comment effectuer des demandes d’accès à des informations personnelles pour [!DNL Real-time Customer Profile] à l’aide de l’API ou de l’interface utilisateur [!DNL Privacy Service]. Avant de lire ces sections, il est vivement recommandé de consulter la documentation [API Privacy Service](../privacy-service/api/getting-started.md) ou [interface utilisateur Privacy Service](../privacy-service/ui/overview.md) pour obtenir des instructions complètes sur la manière d’envoyer une tâche de confidentialité, y compris sur la manière de formater correctement les données d’identité utilisateur envoyées dans les payloads de requête.

>[!IMPORTANT]
>
>Privacy Service ne peut traiter que les données [!DNL Profile] à l’aide d’une stratégie de fusion qui n’effectue pas de combinaison d’identités. Si vous utilisez l’interface utilisateur pour confirmer que vos demandes d’accès à des informations personnelles sont en cours de traitement, assurez-vous que vous utilisez une stratégie de type [!DNL None] avec pour type [!UICONTROL Combinaison d’identifiants]. En d’autres termes, vous ne pouvez pas utiliser de stratégie de fusion si [!UICONTROL l’assemblage d’identifiants] est défini sur &quot;[!UICONTROL Graphique privé]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Il est également important de noter que le temps nécessaire à l’exécution d’une demande d’accès à des informations personnelles ne peut pas être garanti. Si des modifications se produisent dans vos données [!DNL Profile] alors qu’une demande est toujours en cours de traitement, le fait que ces enregistrements soient traités ou non ne peut pas non plus être garanti.

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, tout ID fourni dans `userIDs` doit utiliser une balise `namespace` et `type` spécifique. Un [espace de noms d’identité](#namespaces) valide reconnu par [!DNL Identity Service] doit être fourni pour la valeur `namespace`, tandis que la valeur `type` doit être `standard` ou `unregistered` (respectivement pour les espaces de noms standard et personnalisés).

>[!NOTE]
>
>Vous devrez peut-être fournir plusieurs identifiants pour chaque client, en fonction du graphique d’identités et de la manière dont vos fragments de profil sont distribués dans les jeux de données Platform. Voir la section suivante [fragments de profil](#fragments) pour plus d’informations.

En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Lors de l’envoi de requêtes à [!DNL Data Lake], le tableau doit inclure la valeur &quot;ProfileService&quot;.

La requête suivante crée une nouvelle tâche de confidentialité pour les données d’un seul client dans la boutique [!DNL Profile]. Deux valeurs d’identité sont fournies pour le client dans le tableau `userIDs` ; l’une utilisant l’espace de noms d’identité `Email` standard, l’autre un espace de noms `Customer_ID` personnalisé. Elle inclut également la valeur du produit pour [!DNL Profile] (`ProfileService`) dans le tableau `include` :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### Utilisation de l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à bien sélectionner **[!UICONTROL AEP]** et/ou **[!UICONTROL Profile]** sous **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées respectivement dans [!DNL Data Lake] ou dans [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Fragments de profil dans les demandes d’accès à des informations personnelles {#fragments}

Dans l’entrepôt de données [!DNL Profile], les données personnelles d’un client individuel sont souvent composées de plusieurs fragments de profil, qui sont associés à la personne par le biais du graphique d’identités. Lors de l’envoi de demandes d’accès à des informations personnelles au magasin [!DNL Profile], il est important de noter que les demandes sont traitées uniquement au niveau du fragment de profil, plutôt que sur l’ensemble du profil.

Prenons l’exemple d’une situation où vous stockez des données d’attributs du client dans trois jeux de données distincts, qui utilisent différents identifiants pour associer ces données à des clients individuels :

| Nom du jeu de données | Champ d’identité Principal | Attributs stockés |
| --- | --- | --- |
| Jeu de données 1 | `customer_id` | `address` |
| Jeu de données 2 | `email_id` | `firstName`, `lastName` |
| Jeu de données 3 | `email_id` | `mlScore` |

L’un des jeux de données utilise `customer_id` comme identifiant Principal, tandis que les deux autres utilisent `email_id`. Si vous deviez envoyer une demande d’accès à des informations personnelles (accès ou suppression) en utilisant uniquement `email_id` comme valeur d’identifiant utilisateur, seuls les attributs `firstName`, `lastName` et `mlScore` seraient traités, tandis que `address` ne seraient pas affectés.

Pour vous assurer que vos demandes d’accès à des informations personnelles traitent tous les attributs du client pertinents, vous devez fournir les Principales valeurs d’identité pour tous les jeux de données applicables où ces attributs peuvent être stockés (jusqu’à neuf identifiants par client). Consultez la section sur les champs d’identité dans les [principes de base de la composition des schémas](../xdm/schema/composition.md#identity) pour plus d’informations sur les champs généralement marqués comme identités.

>[!NOTE]
>
>Si vous utilisez des [environnements de test](../sandboxes/home.md) différents pour stocker vos données [!DNL Profile], vous devez effectuer une demande d’accès à des informations personnelles distincte pour chaque environnement de test, en indiquant le nom de l’environnement de test approprié dans l’en-tête `x-sandbox-name`.

## Traitement des demandes de suppression

Lorsquʼ[!DNL Experience Platform] reçoit une requête DELETE de la part de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] pour confirmer que la requête a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite supprimés de la boutique [!DNL Data Lake] ou [!DNL Profile] une fois la tâche de confidentialité terminée. Bien que la tâche de suppression soit toujours en cours de traitement, les données sont supprimées en douceur et ne sont donc accessibles par aucun service [!DNL Platform]. Pour plus d’informations sur les statuts des tâches de suivi, consultez la [[!DNL Privacy Service] documentation](../privacy-service/home.md#monitor) .

>[!IMPORTANT]
>
>Bien qu’une requête de suppression réussie supprime les données d’attribut collectées pour un client (ou un ensemble de clients), la requête ne supprime pas les associations établies dans le graphique d’identités.
>
>Par exemple, une requête de suppression qui utilise les valeurs `email_id` et `customer_id` d’un client supprime toutes les données d’attribut stockées sous ces identifiants. Cependant, toute donnée qui est ensuite ingérée sous le même `customer_id` sera toujours associée à la `email_id` appropriée, car l’association existe toujours.

Dans les prochaines versions, [!DNL Platform] enverra une confirmation à [!DNL Privacy Service] une fois les données supprimées de manière irréversible.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Experience Platform]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

Pour plus d’informations sur le traitement des demandes d’accès à des informations personnelles pour les ressources [!DNL Platform] non utilisées par [!DNL Profile], consultez le document sur le traitement des demandes d’accès à des informations personnelles dans le lac de données](../catalog/privacy.md).[
