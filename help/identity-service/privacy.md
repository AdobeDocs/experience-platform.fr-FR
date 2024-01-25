---
keywords: Experience Platform;accueil;rubriques populaires
title: Traitement des demandes d’accès à des informations personnelles dans Identity Service
description: Adobe Experience Platform Privacy Service traite les demandes des clients en matière dʼaccès, d’opt-out de vente ou de suppression de leurs données personnelles conformément aux nombreuses réglementations en matière de confidentialité. Ce document couvre les concepts essentiels associés au traitement des demandes d’accès à des informations personnelles pour Identity Service.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 64%

---

# Traitement des demandes dʼaccès à des informations personnelles dans [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes des clients en matière dʼaccès, d’opt-out de vente ou de suppression de leurs données personnelles conformément aux réglementations de confidentialité telles que le Règlement général sur la protection des données (RGPD) et le [!DNL California Consumer Privacy Act] (CCPA).

Ce document couvre les concepts essentiels associés au traitement des demandes d’accès à des informations personnelles pour [!DNL Identity Service] dans Adobe Experience Platform.

>[!NOTE]
>
>Ce guide porte uniquement sur la manière d’effectuer des demandes d’accès à des informations personnelles pour la banque de données d’identité dans Experience Platform. Si vous prévoyez également d’effectuer des demandes d’accès à des informations personnelles pour le lac de données Platform ou [!DNL Real-Time Customer Profile], reportez-vous au guide sur la [traitement des demandes d’accès à des informations personnelles dans le lac de données](../catalog/privacy.md) et au guide sur [traitement des demandes d’accès à des informations personnelles pour Profile](../profile/privacy.md) en plus de ce tutoriel.
>
>Pour savoir comment effectuer des demandes d’accès à des informations personnelles pour d’autres applications Adobe Experience Cloud, reportez-vous à la [documentation du Privacy Service](../privacy-service/experience-cloud-apps.md).

## Prise en main

Une connaissance concrète des services [!DNL Experience Platform] suivants est recommandée avant la lecture de ce guide :

* [[!DNL Privacy Service]](../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [[!DNL Real-Time Customer Profile]](home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] rapproche les données dʼidentité client entre les systèmes et les appareils. [!DNL Identity Service] utilise les **espaces de noms d’identité** pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse e-mail (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus dʼinformations sur les espaces de noms dʼidentité dans [!DNL Experience Platform], consultez la [présentation de lʼespace de noms dʼidentité](../identity-service/features/namespaces.md).

## Envoi de requêtes {#submit}

Les sections ci-dessous décrivent comment effectuer des demandes d’accès à des informations personnelles pour [!DNL Identity Service] en utilisant l’API ou l’interface utilisateur [!DNL Privacy Service]. Avant de lire ces sections, il est vivement recommandé de consulter l’[API Privacy Service](../privacy-service/api/getting-started.md) ou la documentation de l’[interface utilisateur Privacy Service](../privacy-service/ui/overview.md) pour obtenir des instructions complètes sur la manière d’envoyer une tâche concernant la confidentialité, y compris sur la manière de formater correctement les données d’identité utilisateur envoyées dans les payloads de requête.

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, les identifiants fournis dans `userIDs` doivent utiliser un `namespace` et `type`. Un [espace de noms d’identité](#namespaces) valide reconnu par [!DNL Identity Service] doit être fourni pour la variable `namespace`, tandis que la variable `type` doit être `standard` ou `unregistered` (pour les espaces de noms standard et personnalisés, respectivement).

En outre, le tableau `include` de la payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Lorsque vous réalisez des requêtes vers [!DNL Identity], le tableau doit inclure la valeur `Identity`.

La requête suivante crée une tâche de confidentialité dans le cadre du RGPD pour les données d’un seul client dans la banque [!DNL Identity]. Deux valeurs d’identité sont fournies pour le client dans le tableau `userIDs` ; une utilisant la norme `Email` espace de noms d’identité et l’autre à l’aide d’un espace de noms `ECID`, il inclut également la valeur de produit pour [!DNL Identity] (`Identity`) dans le tableau `include` :

>[!TIP]
>
>Lorsque vous supprimez un espace de noms personnalisé à l’aide de l’API, vous devez spécifier le symbole d’identité comme espace de noms, au lieu du nom d’affichage.

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

### Utiliser l’interface utilisateur

>[!TIP]
>
>Lorsque vous supprimez un espace de noms personnalisé à l’aide de l’interface utilisateur, vous devez spécifier le symbole d’identité comme espace de noms, au lieu du nom d’affichage. En outre, vous ne pouvez pas supprimer les espaces de noms personnalisés dans l’interface utilisateur pour les sandbox hors production.

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à sélectionner **[!UICONTROL Identité]** sous **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées dans [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Traitement des demandes de suppression

Lorsquʼ[!DNL Experience Platform] reçoit une requête DELETE de la part de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] pour confirmer que la requête a été reçue et que les données concernées ont été marquées pour suppression. La suppression de l’identité individuelle est basée sur l’espace de noms et/ou la valeur d’identifiant fournis. En outre, la suppression a lieu pour tous les environnements de test associés à une organisation donnée.

Selon que vous avez également inclus ou non Real-time Customer Profile (`ProfileService`) et le lac de données (`aepDataLake`) en tant que produits dans votre demande d’accès à des informations personnelles (`identity`), différents ensembles de données liés à l’identité sont supprimés du système à des moments potentiellement différents :

| Produits inclus | Effets |
| --- | --- |
| `identity` only | L’identité fournie est supprimée dès que Platform envoie la confirmation que la demande de suppression a été reçue. Le profil construit à partir de ce graphique d’identités reste, mais ne sera pas mis à jour lorsque de nouvelles données seront ingérées, car les associations d’identités sont désormais supprimées. Les données associées au profil restent également dans le lac de données. |
| `identity` et `ProfileService` | L’identité fournie est supprimée dès que Platform envoie la confirmation que la demande de suppression a été reçue. Les données associées au profil restent dans le lac de données. |
| `identity` et `aepDataLake` | L’identité fournie est supprimée dès que Platform envoie la confirmation que la demande de suppression a été reçue. Le profil construit à partir de ce graphique d’identités reste, mais ne sera pas mis à jour lorsque de nouvelles données seront ingérées, car les associations d’identités sont désormais supprimées.<br><br>Lorsque le produit du lac de données répond que la demande a été reçue et qu’il est en cours de traitement, les données associées au profil sont supprimées de manière réversible et ne sont donc accessibles à aucun [!DNL Platform] service. Une fois la tâche terminée, les données sont complètement supprimées du lac de données. |
| `identity`, `ProfileService`, et `aepDataLake` | L’identité fournie est supprimée dès que Platform envoie la confirmation que la demande de suppression a été reçue.<br><br>Lorsque le produit du lac de données répond que la demande a été reçue et qu’il est en cours de traitement, les données associées au profil sont supprimées de manière réversible et ne sont donc accessibles à aucun [!DNL Platform] service. Une fois la tâche terminée, les données sont complètement supprimées du lac de données. |

Voir [[!DNL Privacy Service] documentation](../privacy-service/home.md#monitor) pour plus d’informations sur les états des tâches de suivi.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Identity Service]. Pour plus d’informations sur le traitement des requêtes de confidentialité pour d’autres [!DNL Experience Cloud] applications, voir le document sur [[!DNL Privacy Service] et [!DNL Experience Cloud] applications](../privacy-service/experience-cloud-apps.md).
