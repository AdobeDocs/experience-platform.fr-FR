---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Traitement des demandes de confidentialité dans le Profil client en temps réel
topic: overview
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# Traitement des demandes de confidentialité dans le Profil client en temps réel

Le service de confidentialité d’Adobe Experience Platform traite les demandes d’accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux règles de confidentialité telles que le Règlement général sur la protection des données (RGPD) et la Loi sur la protection des données des consommateurs de Californie (CCPA).

Ce document couvre les concepts essentiels liés au traitement des demandes de confidentialité pour le Profil client en temps réel.

## Prise en main

Avant de lire ce guide, il est recommandé de bien comprendre les services Experience Platform suivants :

* [Privacy Service](home.md): Gère les demandes des clients pour accéder aux applications Adobe Experience Cloud, les exclure de la vente ou les supprimer.
* [Service](../identity-service/home.md)d&#39;identité : Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.
* [Profil](../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

## Comprendre les espaces de nommage d&#39;identité {#namespaces}

Adobe Experience Platform Identity Service relie les données d’identité des clients entre les systèmes et les périphériques. Identity Service utilise des espaces de nommage **** d&#39;identité pour fournir un contexte aux valeurs d&#39;identité en les rattachant à leur système d&#39;origine. Un espace de nommage peut représenter un concept générique tel qu’une adresse électronique (&quot;Adresse électronique&quot;) ou associer l’identité à une application spécifique, telle qu’un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou un Adobe Cible ID (&quot;TNTID&quot;).

Identity Service conserve un stock d&#39;espaces de nommage d&#39;identité définis globalement (standard) et définis par l&#39;utilisateur (personnalisés). Les espaces de nommage standard sont disponibles pour toutes les organisations (par exemple, &quot;Courriel&quot; et &quot;ECID&quot;), tandis que votre organisation peut également créer des espaces de nommage personnalisés en fonction de ses besoins particuliers.

Pour plus d’informations sur les espaces de nommage d’identité dans la plate-forme d’expérience, voir la présentation [de l’espace de nommage](../identity-service/namespaces.md)d’identité.

## Envoi de requêtes {#submit}

>[!NOTE] Cette section explique comment créer des requêtes de confidentialité pour le stockage de données de Profil. Il est vivement recommandé de consulter l’API [de](../privacy-service/api/getting-started.md) Privacy Service ou la documentation de l’interface utilisateur [de](../privacy-service/ui/overview.md) Privacy Service pour connaître les étapes complètes de l’envoi d’une tâche de confidentialité, y compris la manière de formater correctement les données d’identité d’utilisateur envoyées dans les charges de demande.

La section suivante décrit comment effectuer des demandes de confidentialité pour le Profil client en temps réel et Data Lake à l’aide de l’API ou de l’interface utilisateur de Privacy Service.

### Utilisation de l’API

Lors de la création de demandes de travaux dans l’API, les demandes `userIDs` fournies doivent utiliser un code spécifique `namespace` et `type` selon le magasin de données auquel elles s’appliquent. Les identifiants de la boutique de Profils doivent utiliser &quot;standard&quot; ou &quot;personnalisé&quot; pour leur `type` valeur et un espace de nommage [d&#39;](#namespaces) identité valide reconnu par Identity Service pour leur `namespace` valeur.


En outre, le `include` tableau de la charge utile de la demande doit inclure les valeurs de produit des différents entrepôts de données auxquels la demande est envoyée. Lorsque vous effectuez des demandes à Data Lake, la baie doit inclure la valeur &quot;ProfileService&quot;.

La demande suivante crée une nouvelle tâche de confidentialité pour le Profil client en temps réel, à l’aide de l’espace de nommage d’identité &quot;E-mail&quot; standard. Il inclut également la valeur du produit pour le Profil dans la `include` baie :

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

Lors de la création de demandes d&#39;emploi dans l&#39;interface utilisateur, veillez à sélectionner **AEP Data Lake** et/ou **Profil** sous _Produits_ afin de traiter les tâches pour les données stockées dans Data Lake ou dans le Profil client en temps réel, respectivement.

<img src="images/privacy/product-value.png" width="450"><br>

## Supprimer le traitement de demande

Lorsqu’Experience Platform reçoit une demande de suppression de Privacy Service, Platform envoie une confirmation à Privacy Service que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les dossiers sont ensuite retirés du magasin Data Lake ou du magasin de Profils dans les sept jours. Pendant cette période de sept jours, les données sont supprimées à l&#39;écran et ne sont donc accessibles à aucun service de plateforme.

Dans les prochaines versions, Platform enverra une confirmation à Privacy Service après la suppression physique des données.

## Étapes suivantes

En lisant ce document, vous avez été initié aux concepts importants liés au traitement des demandes de confidentialité dans Experience Platform. Il est recommandé de continuer à lire la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d&#39;identité et créer des tâches de confidentialité.

Pour plus d&#39;informations sur le traitement des demandes de confidentialité pour les ressources de la plateforme non utilisées par le Profil, consultez le document sur le traitement des demandes de [confidentialité dans Data Lake](../catalog/privacy.md).