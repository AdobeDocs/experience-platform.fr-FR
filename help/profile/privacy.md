---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Traitement de la demande d’accès à des informations personnelles dans Real-time Customer Profile
topic: overview
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 46%

---


# Privacy request processing in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] processes customer requests to access, opt out of sale, or delete their personal data as delineated by privacy regulations such as the General Data Protection Regulation (GDPR) and [!DNL California Consumer Privacy Act] (CCPA).

This document covers essential concepts related to processing privacy requests for [!DNL Real-time Customer Profile].

## Prise en main

It is recommended that you have a working understanding of the following [!DNL Experience Platform] services before reading this guide:

* [[ !Privacy Service DNL]](home.md): Gère les demandes des clients pour accéder aux applications Adobe Experience Cloud, les exclure de la vente ou supprimer leurs données personnelles.
* [[ !Service d&#39;identité DNL]](../identity-service/home.md): Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.
* [[ !Profil client en temps réel DNL]](../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] bridges customer identity data across systems and devices. [!DNL Identity Service] utilise les **espaces de noms d’identité** pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

For more information about identity namespaces in [!DNL Experience Platform], see the [identity namespace overview](../identity-service/namespaces.md).

## Envoi de requêtes {#submit}

>[!NOTE]
>
>This section covers how to create privacy requests for the [!DNL Profile] data store. Il est vivement recommandé de consulter l’[API Privacy Service](../privacy-service/api/getting-started.md) ou la documentation de l’[interface utilisateur de Privacy Service](../privacy-service/ui/overview.md) pour obtenir des instructions complètes sur la manière d’envoyer une tâche concernant la confidentialité, y compris sur la manière de formater correctement les données d’identité utilisateur envoyées dans les payloads de requête.

The following section outlines how to make privacy requests for [!DNL Real-time Customer Profile] and the [!DNL Data Lake] using the [!DNL Privacy Service] API or UI.

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, tout `userIDs` fourni doit utiliser un `namespace` et un `type` spécifiques en fonction de la banque de données concernée. IDs for the [!DNL Profile] store must use either &quot;standard&quot; or &quot;custom&quot; for their `type` value, and a valid [identity namespace](#namespaces) recognized by [!DNL Identity Service] for their `namespace` value.


En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. When making requests to the [!DNL Data Lake], the array must include the value &quot;ProfileService&quot;.

The following request creates a new privacy job for both [!DNL Real-time Customer Profile], using the standard &quot;Email&quot; identity namespace. It also includes the product value for [!DNL Profile] in the `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Utilisation de l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à bien sélectionner **[!UICONTROL AEP]** et/ou **[!UICONTROL Profile]** sous _[!UICONTROL Produits]_ afin de traiter les tâches pour les données stockées respectivement dans le lac de données ou dans .[!DNL Data Lake][!DNL Real-time Customer Profile]

<img src="images/privacy/product-value.png" width="450"><br>

## Traitement des demandes de suppression

When [!DNL Experience Platform] receives a delete request from [!DNL Privacy Service], [!DNL Platform] sends confirmation to [!DNL Privacy Service] that the request has been received and affected data has been marked for deletion. The records are then removed from the [!DNL Data Lake] or [!DNL Profile] store within seven days. During that seven-day window, the data is soft-deleted and is therefore not accessible by any [!DNL Platform] service.

In future releases, [!DNL Platform] will send confirmation to [!DNL Privacy Service] after data has been physically deleted.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Experience Platform]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

For information on processing privacy requests for [!DNL Platform] resources not used by [!DNL Profile], see the document on [privacy request processing in the Data Lake](../catalog/privacy.md).