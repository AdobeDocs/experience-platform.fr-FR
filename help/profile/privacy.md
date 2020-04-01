---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Traitement des demandes de confidentialité dans le client en temps réel '
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# Traitement des demandes de confidentialité dans le client en temps réel 

Le service de confidentialité d’Adobe Experience Platform traite les demandes des clients d’accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux règles de confidentialité, telles que le Règlement général sur la protection des données (RDDC) et la Loi sur la protection des renseignements personnels des consommateurs (LPCA) de Californie.

Ce couvre les concepts essentiels liés au traitement des demandes de confidentialité pour le client en temps réel.

## Prise en main

Il est recommandé de bien comprendre les services Experience Platform suivants avant de lire ce guide :

* [Privacy Service](home.md): Gère les demandes des clients pour accéder aux applications Adobe Experience Cloud, les exclure de la vente ou les supprimer.
* [Service](../identity-service/home.md)d&#39;identité : Résout le problème fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.
* [](../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

## Compréhension des  d&#39;identité {#namespaces}

Le service d’identité Adobe Experience Platform relie les données d’identité des clients entre les systèmes et les périphériques. Le service d’identité utilise **l’ d’identité** pour fournir un contexte aux valeurs d’identité en les reliant à leur système de  de. Un   peut représenter un concept générique tel qu’une adresse électronique (&quot;Email&quot;) ou associer l’identité à une application spécifique, telle qu’un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou un Adobe  ID (&quot;TNTID&quot;).

Identity Service conserve un stock de d&#39;identité définis (standard) et définis par l&#39;utilisateur (personnalisés)  de . Les  de  standard sont disponibles pour toutes les organisations (par exemple, &quot;Courriel&quot; et &quot;ECID&quot;), tandis que votre organisation peut également créer des de  personnalisés en fonction de ses besoins spécifiques.

Pour plus d’informations sur l’ d’identité  dans la plateforme d’expérience, reportez-vous à la section Présentation [](../identity-service/namespaces.md)du d’ d’identité.

## Envoi de requêtes {#submit}

>[!NOTE] Cette section explique comment formater les demandes de protection de la vie privée pour le lac Data. Il est vivement recommandé de consulter l’API [](../privacy-service/api/getting-started.md) Privacy Service ou la documentation de l’interface utilisateur [de](../privacy-service/ui/overview.md) Privacy Service pour obtenir des instructions complètes sur la manière d’envoyer une tâche de confidentialité, y compris sur la manière de formater correctement les données d’identité utilisateur envoyées dans les charges de demande.

La section suivante explique comment effectuer des demandes de confidentialité pour les  de clients en temps réel et Data Lake à l’aide de l’API ou de l’interface utilisateur de Privacy Service.

### Utilisation de l’API

Lors de la création de demandes de tâche dans l’API, les demandes `userIDs` fournies doivent utiliser une valeur spécifique `namespace` et `type` en fonction du magasin de données auquel elles s’appliquent. Les identifiants du magasin de  de doivent utiliser soit &quot;standard&quot;, soit &quot;personnalisé&quot; pour leur `type` valeur, et une [identité valide ](#namespaces) reconnue par Identity Service pour leur `namespace` valeur.


En outre, le `include` tableau de la charge utile de requête doit inclure les valeurs de produit pour les différents entrepôts de données auxquels la demande est effectuée. Lors de l’envoi de demandes au lac Data, la baie doit inclure la valeur &quot;ProfileService&quot;.

La requête suivante crée une nouvelle tâche de confidentialité pour les deux  Client en temps réel, à l’aide de l’ d’identité &quot;E-mail&quot; standard . Elle inclut également la valeur du produit pour les  de dans la `include` baie :

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

Lors de la création de demandes d’emploi dans l’interface utilisateur, veillez à sélectionner **AEP Data Lake** et/ou le **de produits** sous _Produits_ afin de traiter les tâches pour les données stockées dans le  de données Data Lake ou dans le client en temps réel, respectivement.

<img src="images/privacy/product-value.png" width="450"><br>

## Supprimer le traitement de requête

Lorsque la plateforme d’expérience reçoit une demande de suppression de la part de Privacy Service, la plate-forme envoie une confirmation au service de confidentialité pour confirmer que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les dossiers sont ensuite retirés du magasin Data Lake ou du magasin de  d’dans les sept jours. Pendant cette période de sept jours, les données sont supprimées à l’écran et ne sont donc accessibles à aucun service de plateforme.

Dans les prochaines versions, Platform enverra une confirmation à Privacy Service une fois les données physiquement supprimées.

## Étapes suivantes

En lisant ce , vous avez été initié aux concepts importants liés au traitement des demandes de confidentialité dans Experience Platform. Il est recommandé de continuer à lire la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches de confidentialité.

Pour plus d’informations sur le traitement des demandes de confidentialité pour les ressources de plateformes non utilisées par les , consultez le sur le traitement des demandes de [confidentialité dans Data Lake](../catalog/privacy.md).