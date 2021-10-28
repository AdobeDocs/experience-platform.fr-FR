---
keywords: Experience Platform;accueil;rubriques populaires
title: Traitement des demandes d’accès à des informations personnelles dans Identity Service
description: Adobe Experience Platform Privacy Service traite les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les supprimer, comme le stipulent de nombreuses réglementations de confidentialité. Ce document couvre les concepts essentiels liés au traitement des demandes d’accès à des informations personnelles pour Identity Service.
source-git-commit: 49f5de6c4711120306bfc3e6759ed4e83e8a19c2
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 43%

---


# Traitement des demandes d’accès à des informations personnelles dans [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes des clients d’accéder à leurs données personnelles, de s’exclure de la vente ou de les supprimer, conformément aux réglementations de confidentialité telles que le Règlement général sur la protection des données (RGPD) et [!DNL California Consumer Privacy Act] (CCPA).

Ce document couvre les concepts essentiels liés au traitement des demandes d’accès à des informations personnelles pour [!DNL Identity Service] dans Adobe Experience Platform.

>[!NOTE]
>
>Ce guide porte uniquement sur la manière d’effectuer des demandes d’accès à des informations personnelles pour l’entrepôt de données Identity dans Experience Platform. Si vous prévoyez également d’effectuer des demandes d’accès à des informations personnelles pour le lac de données de Platform ou [!DNL Real-time Customer Profile], reportez-vous au guide sur la [traitement des demandes d’accès à des informations personnelles dans le lac de données](../catalog/privacy.md) et au guide sur [traitement des demandes d’accès à des informations personnelles pour Profile](../profile/privacy.md) en plus de ce tutoriel.
>
>Pour savoir comment effectuer des demandes d’accès à des informations personnelles pour d’autres applications Adobe Experience Cloud, reportez-vous à la [documentation du Privacy Service](../privacy-service/experience-cloud-apps.md).

## Prise en main

Une connaissance concrète des services [!DNL Experience Platform] suivants est recommandée avant la lecture de ce guide :

* [[!DNL Privacy Service]](../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [[!DNL Real-time Customer Profile]](home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] rapproche les données dʼidentité client entre les systèmes et les appareils. [!DNL Identity Service]**utilise les espaces de noms d’identité pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine.** Un espace de noms peut représenter un concept générique tel qu’une adresse e-mail (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus dʼinformations sur les espaces de noms dʼidentité dans [!DNL Experience Platform], consultez la [présentation de lʼespace de noms dʼidentité](../identity-service/namespaces.md).

## Envoi de requêtes {#submit}

Les sections ci-dessous décrivent comment effectuer des demandes d’accès à des informations personnelles pour [!DNL Identity Service] en utilisant la variable [!DNL Privacy Service] API ou interface utilisateur. Avant de lire ces sections, il est vivement conseillé de consulter la section [API Privacy Service](../privacy-service/api/getting-started.md) ou [Interface utilisateur du Privacy Service](../privacy-service/ui/overview.md) documentation pour obtenir des instructions complètes sur la manière d’envoyer une tâche de confidentialité, y compris sur la manière de formater correctement les données utilisateur dans les payloads de requête.

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, les identifiants fournis dans `userIDs` doit utiliser un `namespace` et `type`. Un valide [namespace d’identité](#namespaces) reconnu par [!DNL Identity Service] doit être fourni pour la variable `namespace` , tandis que la variable `type` doit être `standard` ou `unregistered` (pour les espaces de noms standard et personnalisés, respectivement).

En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Lors de l’envoi de requêtes à [!DNL Identity], le tableau doit inclure la valeur `Identity`.

La requête suivante crée une tâche de confidentialité dans le cadre du RGPD pour les données d’un seul client dans la variable [!DNL Identity] magasin. Deux valeurs d’identité sont fournies pour le client dans la variable `userIDs` tableau ; une utilisant la norme `Email` espace de noms d’identité, et l’autre à l’aide d’un `ECID` namespace , il inclut également la valeur de produit pour [!DNL Identity] (`Identity`) dans la variable `include` tableau :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### Utilisation de l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à sélectionner **[!UICONTROL Identité]** under **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées dans [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Traitement des demandes de suppression

Lorsquʼ[!DNL Experience Platform] reçoit une requête DELETE de la part de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] pour confirmer que la requête a été reçue et que les données concernées ont été marquées pour suppression. La suppression de l’identité individuelle est basée sur l’espace de noms et/ou la valeur d’identifiant fournis. En outre, la suppression a lieu pour tous les environnements de test associés à une organisation IMS donnée.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Identity Service]. Pour plus d’informations sur le traitement des demandes d’accès à des informations personnelles pour d’autres [!DNL Experience Cloud] applications, voir le document sur [[!DNL Privacy Service] and [!DNL Experience Cloud] applications](../privacy-service/experience-cloud-apps.md).