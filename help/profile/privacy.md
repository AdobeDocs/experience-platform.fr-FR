---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Traitement des demandes de confidentialité dans le Profil client en temps réel
topic-legacy: overview
type: Documentation
description: Adobe Experience Platform Privacy Service traite les demandes d’accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux nombreuses réglementations en matière de confidentialité. Ce document couvre les concepts essentiels associés au traitement des demandes d’accès à des informations personnelles pour Real-time Customer Profile.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 25%

---

# Traitement de la demande de confidentialité dans [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes des clients d&#39;accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux règlements sur la protection de la vie privée tels que le Règlement général sur la protection des données (RGPD) et [!DNL California Consumer Privacy Act] (ACCP).

Ce document couvre les concepts essentiels liés au traitement des demandes de confidentialité pour [!DNL Real-time Customer Profile].

## Prise en main

Il est recommandé de bien comprendre les services [!DNL Experience Platform] suivants avant de lire ce guide :

* [[!DNL Privacy Service]](home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [[!DNL Real-time Customer Profile]](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] relie les données d&#39;identité des clients entre les systèmes et les périphériques. [!DNL Identity Service] utilise les **espaces de noms d’identité** pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus d&#39;informations sur les espaces de nommage d&#39;identité dans [!DNL Experience Platform], consultez la [présentation de l&#39;espace de nommage d&#39;identité](../identity-service/namespaces.md).

## Envoi de requêtes {#submit}

Les sections ci-dessous décrivent comment effectuer des demandes de confidentialité pour [!DNL Real-time Customer Profile] à l&#39;aide de l&#39;API ou de l&#39;interface utilisateur [!DNL Privacy Service]. Avant de lire ces sections, il est vivement recommandé de consulter la documentation [API du Privacy Service](../privacy-service/api/getting-started.md) ou [IU du Privacy Service](../privacy-service/ui/overview.md) pour connaître les étapes complètes de l’envoi d’une tâche de confidentialité, y compris la manière de formater correctement les données d’identité de l’utilisateur envoyées dans les charges de demande.

>[!IMPORTANT]
>
>Le Privacy Service ne peut traiter que les données [!DNL Profile] à l&#39;aide d&#39;une stratégie de fusion qui n&#39;effectue pas de raccordement d&#39;identité. Si vous utilisez l’interface utilisateur pour vérifier si vos demandes de confidentialité sont en cours de traitement, veillez à utiliser une stratégie avec &quot;[!DNL None]&quot; comme type [!UICONTROL d’assemblage d’identifiants]. En d’autres termes, vous ne pouvez pas utiliser une stratégie de fusion où [!UICONTROL l’assemblage d’identifiants] est défini sur &quot;[!UICONTROL Graphique privé]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Il est également important de noter que le temps qu&#39;une demande de protection des renseignements personnels peut mettre à exécution ne peut être garanti. Si des modifications se produisent dans vos données [!DNL Profile] alors qu&#39;une requête est en cours de traitement, il n&#39;est pas non plus garanti que ces enregistrements sont ou non traités.

### Utilisation de l’API

Lors de la création de demandes de travaux dans l&#39;API, les identifiants fournis dans `userIDs` doivent utiliser des `namespace` et `type` spécifiques. Un espace de nommage d&#39;identité [valide](#namespaces) reconnu par [!DNL Identity Service] doit être fourni pour la valeur `namespace`, tandis que `type` doit être `standard` ou `unregistered` (pour les espaces de nommage standard et personnalisés, respectivement).

>[!NOTE]
>
>Vous devrez peut-être fournir plusieurs identifiants pour chaque client, en fonction du graphique d’identité et de la manière dont vos fragments de profil sont distribués dans les jeux de données de la plateforme. Pour plus d’informations, voir la section suivante [fragments de profil](#fragments).

En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Lors de l&#39;envoi de requêtes à [!DNL Data Lake], le tableau doit inclure la valeur &quot;ProfileService&quot;.

La demande suivante crée une nouvelle tâche de confidentialité pour les données d&#39;un client unique dans la boutique [!DNL Profile]. Deux valeurs d&#39;identité sont fournies pour le client dans la baie `userIDs`; l&#39;un utilise l&#39;espace de nommage d&#39;identité `Email` standard, l&#39;autre un espace de nommage `Customer_ID` personnalisé. Il inclut également la valeur de produit pour [!DNL Profile] (`ProfileService`) dans la baie `include` :

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
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Utilisation de l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à bien sélectionner **[!UICONTROL AEP]** et/ou **[!UICONTROL Profile]** sous **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées respectivement dans le lac de données ou dans .[!DNL Data Lake][!DNL Real-time Customer Profile]

<img src="images/privacy/product-value.png" width="450"><br>

## Fragments de profil dans les demandes de confidentialité {#fragments}

Dans le magasin de données [!DNL Profile], les données personnelles d&#39;un client individuel sont souvent constituées de plusieurs fragments de profil, qui sont associés à la personne par le biais du graphique d&#39;identité. Lors de l’envoi de demandes de confidentialité au magasin [!DNL Profile], il est important de noter que les demandes sont traitées uniquement au niveau du fragment de profil, plutôt que sur l’ensemble du profil.

Prenons l’exemple d’un cas où vous stockez des données d’attributs du client dans trois jeux de données distincts, qui utilisent des identifiants différents pour associer ces données à des clients individuels :

| Nom du jeu de données | Champ d&#39;identité Principal | Attributs stockés |
| --- | --- | --- |
| Jeu de données 1 | `customer_id` | `address` |
| Jeu de données 2 | `email_id` | `firstName`, `lastName` |
| Jeu de données 3 | `email_id` | `mlScore` |

L&#39;un des jeux de données utilise `customer_id` comme identifiant Principal, tandis que les deux autres utilisent `email_id`. Si vous deviez envoyer une demande de confidentialité (accès ou suppression) en utilisant uniquement `email_id` comme valeur d&#39;ID utilisateur, seuls les attributs `firstName`, `lastName` et `mlScore` seraient traités, alors que `address` ne seraient pas affectés.

Pour vous assurer que vos demandes de confidentialité traitent tous les attributs de client pertinents, vous devez fournir les valeurs d’identité Principales pour tous les jeux de données applicables dans lesquels ces attributs peuvent être stockés (jusqu’à neuf identifiants par client). Consultez la section sur les champs d&#39;identité dans les [bases de la composition des schémas](../xdm/schema/composition.md#identity) pour plus d&#39;informations sur les champs couramment marqués comme identités.

>[!NOTE]
>
>Si vous utilisez des [sandbox](../sandboxes/home.md) différents pour stocker vos données [!DNL Profile], vous devez faire une demande de confidentialité distincte pour chaque sandbox, en indiquant le nom de sandbox approprié dans l&#39;en-tête `x-sandbox-name`.

## Traitement des demandes de suppression

Lorsque [!DNL Experience Platform] reçoit une demande de suppression de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite supprimés du magasin [!DNL Data Lake] ou [!DNL Profile] une fois la tâche de confidentialité terminée. Bien que la tâche de suppression soit toujours en cours de traitement, les données sont supprimées à l’écran et ne sont donc accessibles à aucun service [!DNL Platform]. Consultez la [[!DNL Privacy Service] documentation](../privacy-service/home.md#monitor) pour plus d&#39;informations sur le suivi des états des tâches.

>[!IMPORTANT]
>
>Bien qu’une demande de suppression réussie supprime les données d’attribut collectées pour un client (ou un ensemble de clients), la demande ne supprime pas les associations établies dans le graphique d’identité.
>
>Par exemple, une demande de suppression qui utilise les attributs `email_id` et `customer_id` d&#39;un client supprime toutes les données d&#39;attribut stockées sous ces identifiants. Cependant, toute donnée qui est ensuite assimilée sous la même `customer_id` sera toujours associée à la `email_id` appropriée, car l&#39;association existe toujours.

Dans les prochaines versions, [!DNL Platform] enverra une confirmation à [!DNL Privacy Service] une fois les données physiquement supprimées.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Experience Platform]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

Pour plus d&#39;informations sur le traitement des demandes de confidentialité pour les ressources [!DNL Platform] non utilisées par [!DNL Profile], consultez le document sur le traitement des demandes de confidentialité [dans Data Lake](../catalog/privacy.md).
