---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Traitement de la demande d’accès à des informations personnelles dans Real-time Customer Profile
topic: overview
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 25%

---


# Privacy request processing in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] processes customer requests to access, opt out of sale, or delete their personal data as delineated by privacy regulations such as the General Data Protection Regulation (GDPR) and [!DNL California Consumer Privacy Act] (CCPA).

This document covers essential concepts related to processing privacy requests for [!DNL Real-time Customer Profile].

## Prise en main

It is recommended that you have a working understanding of the following [!DNL Experience Platform] services before reading this guide:

* [[!DNL Privacy Service]](home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [[!DNL Real-time Customer Profile]](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] bridges customer identity data across systems and devices. [!DNL Identity Service] utilise les **espaces de noms d’identité** pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Identity Service conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

For more information about identity namespaces in [!DNL Experience Platform], see the [identity namespace overview](../identity-service/namespaces.md).

## Envoi de requêtes {#submit}

Les sections ci-dessous décrivent comment effectuer des demandes de confidentialité pour [!DNL Real-time Customer Profile] l’utilisation de l’ [!DNL Privacy Service] API ou de l’interface utilisateur. Before reading these sections, it is strongly recommended that you review the [Privacy Service API](../privacy-service/api/getting-started.md) or [Privacy Service UI](../privacy-service/ui/overview.md) documentation for complete steps on how to submit a privacy job, including how to properly format submitted user identity data in request payloads.

>[!IMPORTANT]
>
>Le Privacy Service ne peut traiter [!DNL Profile] les données qu’à l’aide d’une stratégie de fusion qui n’effectue pas d’assemblage d’identité. Si vous utilisez l’interface utilisateur pour vérifier si vos demandes de confidentialité sont en cours de traitement, veillez à utiliser une stratégie avec &quot;[!DNL None]&quot; comme type de raccordement [!UICONTROL d’] ID. En d’autres termes, vous ne pouvez pas utiliser de stratégie de fusion lorsque l’assemblage [!UICONTROL d’] ID est défini sur &quot;Graphiqueprivé&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Il est également important de noter que le temps qu&#39;une demande de protection des renseignements personnels peut prendre pour être remplie ne peut être garanti. Si des modifications surviennent dans vos [!DNL Profile] données alors qu’une requête est en cours de traitement, il est également impossible de garantir si ces enregistrements sont traités ou non.

### Utilisation de l’API

Lors de la création de demandes de tâche dans l’API, les identifiants fournis dans `userIDs` doivent utiliser un identifiant spécifique `namespace` et `type`. Un espace de nommage [d&#39;](#namespaces) identité valide reconnu par [!DNL Identity Service] doit être fourni pour la `namespace` valeur, tandis que la `type` valeur doit être soit `standard` soit `unregistered` (pour les espaces de nommage standard et personnalisés, respectivement).

>[!NOTE]
>
>Vous devrez peut-être fournir plusieurs identifiants pour chaque client, en fonction du graphique d’identité et de la manière dont vos fragments de profil sont distribués dans les jeux de données de la plateforme. Pour plus d’informations, voir la section suivante [profils](#fragments) .

En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. When making requests to the [!DNL Data Lake], the array must include the value &quot;ProfileService&quot;.

La demande suivante crée une nouvelle tâche de confidentialité pour les données d’un client unique dans la [!DNL Profile] boutique. Deux valeurs d&#39;identité sont fournies pour le client de la `userIDs` baie ; l&#39;un utilise l&#39;espace de nommage `Email` d&#39;identité standard, l&#39;autre un `Customer_ID` espace de nommage personnalisé. It also includes the product value for [!DNL Profile] (`ProfileService`) in the `include` array:

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

Dans le magasin de [!DNL Profile] données, les données personnelles d’un client individuel sont souvent constituées de plusieurs fragments de profil, qui sont associés à la personne via le graphique d’identité. Lors de l’envoi de requêtes de confidentialité à la [!DNL Profile] boutique, il est important de noter que les requêtes sont traitées uniquement au niveau du fragment de profil, plutôt que sur l’ensemble du profil.

Prenons l’exemple d’un cas où vous stockez des données d’attributs du client dans trois jeux de données distincts, qui utilisent des identifiants différents pour associer ces données à des clients individuels :

| Nom du jeu de données | Champ d&#39;identité Principal | Attributs stockés |
| --- | --- | --- |
| Jeu de données 1 | `customer_id` | `address` |
| Jeu de données 2 | `email_id` | `firstName`, `lastName` |
| Jeu de données 3 | `email_id` | `mlScore` |

L&#39;un des jeux de données utilise `customer_id` comme identifiant Principal, tandis que les deux autres utilisent `email_id`. Si vous deviez envoyer une demande de confidentialité (accès ou suppression) en utilisant uniquement `email_id` comme valeur d’ID utilisateur, seuls les attributs `firstName`, `lastName`et `mlScore` sont traités, mais `address` ne sont pas affectés.

Pour vous assurer que vos demandes de confidentialité traitent tous les attributs de client pertinents, vous devez fournir les valeurs d’identité Principales pour tous les jeux de données applicables dans lesquels ces attributs peuvent être stockés (jusqu’à neuf identifiants par client). Pour plus d’informations sur les champs d’identité couramment identifiés comme identités, consultez la section relative aux champs d’identité dans les [bases de la composition](../xdm/schema/composition.md#identity) des schémas.

>[!NOTE]
>
>Si vous utilisez des [sandbox](../sandboxes/home.md) différents pour stocker vos [!DNL Profile] données, vous devez effectuer une demande de confidentialité distincte pour chaque sandbox, en indiquant le nom de sandbox approprié dans l’ `x-sandbox-name` en-tête.

## Traitement des demandes de suppression

When [!DNL Experience Platform] receives a delete request from [!DNL Privacy Service], [!DNL Platform] sends confirmation to [!DNL Privacy Service] that the request has been received and affected data has been marked for deletion. Les enregistrements sont ensuite supprimés de la [!DNL Data Lake] boutique ou de la [!DNL Profile] boutique une fois la tâche de confidentialité terminée. Bien que la tâche de suppression soit toujours en cours de traitement, les données sont supprimées à l’écran et ne sont donc accessibles à aucun [!DNL Platform] service. Consultez la [[!DNL Privacy Service] documentation](../privacy-service/home.md#monitor) pour plus d’informations sur le suivi des états des tâches.

>[!IMPORTANT]
>
>Bien qu’une demande de suppression réussie supprime les données d’attribut collectées pour un client (ou un ensemble de clients), la demande ne supprime pas les associations établies dans le graphique d’identité.
>
>Par exemple, une requête de suppression qui utilise une requête de client `email_id` et `customer_id` supprime toutes les données d’attribut stockées sous ces identifiants. Toutefois, les données qui seront ensuite assimilées sous la même `customer_id` forme seront toujours associées aux données appropriées `email_id`, car l&#39;association existe toujours.

In future releases, [!DNL Platform] will send confirmation to [!DNL Privacy Service] after data has been physically deleted.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles dans [!DNL Experience Platform]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

For information on processing privacy requests for [!DNL Platform] resources not used by [!DNL Profile], see the document on [privacy request processing in the Data Lake](../catalog/privacy.md).