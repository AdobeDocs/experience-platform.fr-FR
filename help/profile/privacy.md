---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Traitement des demandes d’accès à des informations personnelles dans Real-time Customer Profile
type: Documentation
description: Adobe Experience Platform Privacy Service traite les demandes des clients en matière dʼaccès, de retrait du consentement à la vente ou de suppression de leurs données personnelles conformément aux nombreuses réglementations en matière de confidentialité. Ce document couvre les concepts essentiels associés au traitement des demandes d’accès à des informations personnelles pour Real-time Customer Profile.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 159a46fa227207bf161100e50bc286322ba2d00b
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 31%

---

# Traitement des demandes dʼaccès à des informations personnelles dans [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente, ou les effacer comme le stipulent les réglementations de confidentialité telles que le Règlement général sur la protection des données (RGPD) et le [!DNL California Consumer Privacy Act] (CCPA).

Ce document couvre les concepts essentiels associés au traitement des demandes d’accès à des informations personnelles pour [!DNL Real-time Customer Profile] dans Adobe Experience Platform.

>[!NOTE]
>
>Ce guide porte uniquement sur la manière d’effectuer des demandes d’accès à des informations personnelles pour le magasin de données Profile dans Experience Platform. Si vous prévoyez également d’effectuer des demandes d’accès à des informations personnelles pour le lac de données de Platform, reportez-vous au guide sur la [traitement des demandes d’accès à des informations personnelles dans le lac de données](../catalog/privacy.md) en plus de ce tutoriel.
>
>Pour savoir comment effectuer des demandes d’accès à des informations personnelles pour d’autres applications Adobe Experience Cloud, reportez-vous à la [documentation du Privacy Service](../privacy-service/experience-cloud-apps.md).

## Prise en main

Une connaissance concrète des services [!DNL Experience Platform] suivants est recommandée avant la lecture de ce guide :

* [[!DNL Privacy Service]](../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [[!DNL Real-time Customer Profile]](home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] rapproche les données dʼidentité client entre les systèmes et les appareils. [!DNL Identity Service] utilise les **espaces de noms d’identité** pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse e-mail (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus dʼinformations sur les espaces de noms dʼidentité dans [!DNL Experience Platform], consultez la [présentation de lʼespace de noms dʼidentité](../identity-service/namespaces.md).

## Envoi de requêtes {#submit}

Les sections ci-dessous décrivent comment effectuer des demandes d’accès à des informations personnelles pour [!DNL Real-time Customer Profile] en utilisant l’API ou l’interface utilisateur [!DNL Privacy Service]. Avant de lire ces sections, il est vivement conseillé de consulter la section [API Privacy Service](../privacy-service/api/getting-started.md) ou [Interface utilisateur du Privacy Service](../privacy-service/ui/overview.md) documentation pour obtenir des instructions complètes sur la manière d’envoyer une tâche de confidentialité, y compris sur la manière de formater correctement les données d’identité utilisateur envoyées dans les payloads de requête.

>[!IMPORTANT]
>
>Privacy Service ne peut traiter que [!DNL Profile] données utilisant une stratégie de fusion qui n’effectue pas de combinaison d’identités. Voir la section sur [limites des stratégies de fusion](#merge-policy-limitations) pour plus d’informations.
>
>Il est également important de noter que le temps nécessaire à l’exécution d’une demande d’accès à des informations personnelles ne peut pas être garanti. Si des modifications se produisent dans votre [!DNL Profile] pendant le traitement d’une demande, il n’est pas non plus garanti que ces enregistrements soient ou non traités.

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, les identifiants fournis dans `userIDs` doivent utiliser un `namespace` et `type`. Un [espace de noms d’identité](#namespaces) valide reconnu par [!DNL Identity Service] doit être fourni pour la variable `namespace`, tandis que la variable `type` doit être `standard` ou `unregistered` (pour les espaces de noms standard et personnalisés, respectivement).

>[!NOTE]
>
>Vous devrez peut-être fournir plusieurs identifiants pour chaque client, en fonction du graphique d’identités et de la manière dont vos fragments de profil sont distribués dans les jeux de données Platform. Voir la section suivante [fragments de profil](#fragments) pour plus d’informations.

En outre, le tableau `include` de la payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Pour supprimer les données de profil associées à une identité, le tableau doit inclure la valeur `ProfileService`. Pour supprimer les associations de graphiques d’identités du client, le tableau doit inclure la valeur `identity`.

>[!NOTE]
>
>Voir la section sur [demandes de profil et demandes d’identité](#profile-v-identity) plus loin dans ce document pour plus d’informations sur les effets de l’utilisation de `ProfileService` et `identity` dans le `include` tableau.

La requête suivante crée une tâche de confidentialité pour les données d’un seul client dans la variable [!DNL Profile] magasin. Deux valeurs d’identité sont fournies pour le client dans la variable `userIDs` tableau ; une utilisant la norme `Email` espace de noms d’identité, et l’autre à l’aide d’un espace de noms personnalisé `Customer_ID` espace de noms. Elle inclut également la valeur de produit pour [!DNL Profile] (`ProfileService`) dans la variable `include` tableau :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform traite les demandes d’accès à des informations personnelles dans toutes les [sandbox](../sandboxes/home.md) appartenant à votre organisation. Par conséquent, tout en-tête `x-sandbox-name` inclus dans la demande est ignoré par le système. 

### Utiliser l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à sélectionner **[!UICONTROL Lac de données AEP]** et/ou **[!UICONTROL Profil]** under **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées dans le lac de données ou [!DNL Real-time Customer Profile], respectivement.

![Une requête de tâche d’accès en cours de création dans l’interface utilisateur, avec l’option Profil sélectionnée sous Produits](./images/privacy/product-value.png)

## Fragments de profil dans les demandes d’accès à des informations personnelles {#fragments}

Dans le [!DNL Profile] entrepôt de données, les données personnelles d’un client individuel sont souvent composées de plusieurs fragments de profil, qui sont associés à la personne via le graphique d’identités. Lors de l’envoi de requêtes de confidentialité à la variable [!DNL Profile] magasin, il est important de noter que les requêtes sont traitées uniquement au niveau du fragment de profil, plutôt que sur l’ensemble du profil.

Prenons l’exemple d’une situation où vous stockez des données d’attributs du client dans trois jeux de données distincts, qui utilisent différents identifiants pour associer ces données à des clients individuels :

| Nom du jeu de données | Champ d’identité Principal | Attributs stockés |
| --- | --- | --- |
| Jeu de données 1 | `customer_id` | `address` |
| Jeu de données 2 | `email_id` | `firstName`, `lastName` |
| Jeu de données 3 | `email_id` | `mlScore` |

L’un des jeux de données utilise `customer_id` comme identifiant Principal, alors que les deux autres utilisent `email_id`. Si vous envoyez une demande d’accès à des informations personnelles (accès ou suppression) en utilisant uniquement `email_id` comme valeur d’identifiant utilisateur, seule la variable `firstName`, `lastName`, et `mlScore` Les attributs sont traités, tandis que `address` ne serait pas affecté.

Pour vous assurer que vos demandes d’accès à des informations personnelles traitent tous les attributs du client pertinents, vous devez fournir les Principales valeurs d’identité pour tous les jeux de données applicables où ces attributs peuvent être stockés (jusqu’à neuf identifiants par client). Consultez la section sur les champs d’identité dans la [principes de base de la composition des schémas](../xdm/schema/composition.md#identity) pour plus d’informations sur les champs généralement marqués comme identités.

## Traitement des demandes de suppression {#delete}

Lorsquʼ[!DNL Experience Platform] reçoit une requête DELETE de la part de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] pour confirmer que la requête a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite supprimés une fois la tâche de confidentialité terminée.

Selon que vous avez également inclus ou non Identity Service (`identity`) et le lac de données (`aepDataLake`) en tant que produits dans votre demande d’accès à des informations personnelles pour Profile (`ProfileService`), différents ensembles de données liés au profil sont supprimés du système à des moments potentiellement différents :

| Produits inclus | Effets |
| --- | --- |
| `ProfileService` only | Le profil est immédiatement supprimé dès que Platform envoie la confirmation que la demande de suppression a été reçue. Cependant, le graphique d’identités du profil reste inchangé et le profil peut éventuellement être reconstitué lorsque de nouvelles données avec les mêmes identités sont ingérées. Les données associées au profil restent également dans le lac de données. |
| `ProfileService` et `identity` | Le profil et son graphique d’identités associé sont immédiatement supprimés dès que Platform envoie la confirmation que la demande de suppression a été reçue. Les données associées au profil restent dans le lac de données. |
| `ProfileService` et `aepDataLake` | Le profil est immédiatement supprimé dès que Platform envoie la confirmation que la demande de suppression a été reçue. Cependant, le graphique d’identités du profil reste inchangé et le profil peut éventuellement être reconstitué lorsque de nouvelles données avec les mêmes identités sont ingérées.<br><br>Lorsque le produit du lac de données répond que la demande a été reçue et qu’il est en cours de traitement, les données associées au profil sont supprimées de manière réversible et ne sont donc accessibles à aucun [!DNL Platform] service. Une fois la tâche terminée, les données sont complètement supprimées du lac de données. |
| `ProfileService`, `identity`, et `aepDataLake` | Le profil et son graphique d’identités associé sont immédiatement supprimés dès que Platform envoie la confirmation que la demande de suppression a été reçue.<br><br>Lorsque le produit du lac de données répond que la demande a été reçue et qu’il est en cours de traitement, les données associées au profil sont supprimées de manière réversible et ne sont donc accessibles à aucun [!DNL Platform] service. Une fois la tâche terminée, les données sont complètement supprimées du lac de données. |

Reportez-vous à la section [[!DNL Privacy Service] documentation](../privacy-service/home.md#monitor) pour plus d’informations sur les états des tâches de suivi.

### Requêtes de profil et requêtes d’identité {#profile-v-identity}

Si une requête de suppression est effectuée pour Profile (`ProfileService`), mais pas Identity Service (`identity`), la tâche résultante supprime les données d’attribut collectées pour un client (ou un ensemble de clients), mais ne supprime pas les associations établies dans le graphique d’identités.

Par exemple, une requête de suppression qui utilise la variable `email_id` et `customer_id` supprime toutes les données d’attribut stockées sous ces ID. Cependant, toutes les données qui sont ensuite ingérées sous la même `customer_id` sera toujours associé au `email_id`, car l’association existe toujours.

Pour supprimer le profil et toutes les associations d’identité pour un client donné, veillez à inclure Profile et Identity Service en tant que produits cibles dans vos demandes de suppression.

### Limites des stratégies de fusion {#merge-policy-limitations}

Privacy Service ne peut traiter que [!DNL Profile] données utilisant une stratégie de fusion qui n’effectue pas de combinaison d’identités. Si vous utilisez l’interface utilisateur pour confirmer que vos demandes d’accès à des informations personnelles sont en cours de traitement, assurez-vous que vous utilisez une stratégie avec **[!DNL None]** comme son [!UICONTROL Combinaison d’identifiants] type. En d’autres termes, vous ne pouvez pas utiliser une stratégie de fusion dans laquelle [!UICONTROL Combinaison d’identifiants] est défini sur [!UICONTROL Graphique privé].
>![Le groupement d’identifiants de la stratégie de fusion est défini sur Aucun.](./images/privacy/no-id-stitch.png)
>
## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Experience Platform]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

Pour plus d’informations sur le traitement des demandes d’accès à des informations personnelles pour [!DNL Platform] ressources non utilisées par [!DNL Profile], voir le document sur [traitement des demandes d’accès à des informations personnelles dans le lac de données](../catalog/privacy.md).
