---
keywords: Experience Platform;home;popular topics;data lake privacy;identity namespaces;privacy;data lake
solution: Experience Platform
title: Traitement des demandes d’accès à des informations personnelles dans le lac de données
topic: overview
description: adobe experience platform privacy service traite les demandes d’accès, de opt-out de vente ou de suppression de leurs données personnelles conformément aux réglementations légales et organisationnelles en matière de confidentialité. Ce document couvre les concepts fondamentaux liés au traitement des demandes d’accès à des informations personnelles concernant les données clients stockées dans le lac de données.
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 32%

---


# Traitement de la demande de confidentialité dans [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes d’accès, de opt-out de vente ou de suppression de leurs données personnelles conformément aux réglementations légales et de confidentialité de l’entreprise.

This document covers essential concepts related to processing privacy requests for customer data stored in the [!DNL Data Lake].

## Prise en main

It is recommended that you have a working understanding of the following [!DNL Experience Platform] services before reading this guide:

* [[ !Privacy Service DNL]](../privacy-service/home.md): Gère les demandes des clients pour accéder aux applications Adobe Experience Cloud, les exclure de la vente ou supprimer leurs données personnelles.
* [[ !Service de catalogue DNL]](home.md): Système d’enregistrement pour l’emplacement et le lignage des données dans [!DNL Experience Platform]. Fournit une API qui peut être utilisée pour mettre à jour les métadonnées des jeux de données.
* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
* [[ !Service d&#39;identité DNL]](../identity-service/home.md): Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] bridges customer identity data across systems and devices. [!DNL Identity Service] utilise les **[!UICONTROL espaces de noms d’identité]** pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

[!DNL Identity Service] conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

For more information about identity namespaces in [!DNL Experience Platform], see the [identity namespace overview](../identity-service/namespaces.md).

## ajouter des données d&#39;identité aux jeux de données

Lors de la création de demandes de confidentialité pour les [!DNL Data Lake]clients, des valeurs d&#39;identité valides (et leurs espaces de nommage associés) doivent être fournies pour chaque client afin de localiser ses données et de les traiter en conséquence. Par conséquent, tous les jeux de données qui font l’objet de demandes de confidentialité doivent contenir un descripteur **[!UICONTROL d’]** identité dans leur schéma XDM associé.

>[!NOTE]
>
>Les jeux de données basés sur des schémas qui ne prennent pas en charge les métadonnées des descripteurs d’identité (tels que les jeux de données ad hoc) ne peuvent pas actuellement être traités dans les demandes de confidentialité.

Cette section décrit les étapes à suivre pour ajouter un descripteur d&#39;identité au schéma XDM d&#39;un jeu de données existant. Si vous disposez déjà d’un jeu de données avec un descripteur d’identité, vous pouvez passer à la section [](#nested-maps)suivante.

>[!IMPORTANT]
>
>Lorsque vous décidez des champs de schéma à définir en tant qu’identités, gardez à l’esprit les [limites de l’utilisation de champs](#nested-maps)de type mappage imbriqués.

Il existe deux méthodes pour ajouter un descripteur d&#39;identité à un schéma de jeux de données :

* [Utilisation de l’interface utilisateur](#identity-ui)
* [Utilisation de l’API](#identity-api)

### Utilisation de l’interface utilisateur {#identity-ui}

Dans l&#39;interface [!DNL Experience Platform ]utilisateur, l&#39;espace de travail _[!UICONTROL Schémas]_ vous permet de modifier vos schémas XDM existants. Pour ajouter un descripteur d&#39;identité à un schéma, sélectionnez le schéma dans la liste et suivez les étapes pour [définir un champ de schéma en tant que champ](../xdm/tutorials/create-schema-ui.md#identity-field) d&#39;identité dans le [!DNL Schema Editor] didacticiel.

Une fois que vous avez défini les champs appropriés dans le schéma en tant que champs d’identité, vous pouvez passer à la section suivante lors de l’ [envoi des demandes](#submit)de confidentialité.

### Utilisation de l’API {#identity-api}

>[!NOTE]
>
>Cette section suppose que vous connaissez la valeur d&#39;ID URI unique du schéma XDM de votre jeu de données. Si vous ne connaissez pas cette valeur, vous pouvez la récupérer à l’aide de l’ [!DNL Catalog Service] API. Après avoir lu la section [prise en main](./api/getting-started.md) du guide du développeur, suivez les étapes décrites dans la section pour [répertorier](./api/list-objects.md) ou [rechercher](./api/look-up-object.md) des objets [!DNL Catalog] pour trouver votre jeu de données. L&#39;ID de schéma se trouve sous `schemaRef.id`
>
> Cette section comprend des appels à l&#39;API de registre du Schéma. Pour obtenir des informations importantes sur l’utilisation de l’API, y compris la connaissance de votre concept `{TENANT_ID}` et du concept de conteneur, consultez la section [prise en main](../xdm/api/getting-started.md) du guide du développeur.

Vous pouvez ajouter un descripteur d&#39;identité au schéma XDM d&#39;un jeu de données en envoyant une requête de POST au point de `/descriptors` terminaison dans l&#39; [!DNL Schema Registry] API.

**Format d’API**

```http
POST /descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité dans un champ « adresse électronique » d’un exemple de schéma.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de création. Pour les descripteurs d’identité, la valeur doit être &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | ID URI unique du schéma XDM de votre jeu de données. |
| `xdm:sourceVersion` | Version du schéma XDM spécifiée dans `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Chemin d’accès au champ de schéma auquel le descripteur est appliqué. |
| `xdm:namespace` | L&#39;un des espaces de nommage [d&#39;identité](../privacy-service/api/appendix.md#standard-namespaces) standard reconnus par [!DNL Privacy Service]ou un espace de nommage personnalisé défini par votre organisation. |
| `xdm:property` | &quot;xdm:id&quot; ou &quot;xdm:code&quot;, selon l’espace de nommage utilisé sous `xdm:namespace`. |
| `xdm:isPrimary` | Une valeur booléenne facultative. Lorsque la valeur est true, cela indique que le champ est une identité Principale. Les schémas ne peuvent contenir qu’une seule identité principale. La valeur par défaut est false si elle n’est pas incluse. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et les détails du descripteur nouvellement créé.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Envoi de requêtes {#submit}

>[!NOTE]
>
>This section covers how to format privacy requests for the [!DNL Data Lake]. It is strongly recommended that you review the [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) or [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) documentation for complete steps on how to submit a privacy job, including how to properly format submitted user identity data in request payloads.

La section suivante décrit comment effectuer des demandes de confidentialité pour l’ [!DNL Data Lake] utilisation de l’ [!DNL Privacy Service] interface utilisateur ou de l’API.

### Utilisation de l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à bien sélectionner **[!UICONTROL AEP]** et/ou **[!UICONTROL Profile]** sous _[!UICONTROL Produits]_ afin de traiter les tâches pour les données stockées respectivement dans le lac de données ou dans .[!DNL Data Lake][!DNL Real-time Customer Profile]

<img src="images/privacy/product-value.png" width="450"><br>

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, tout `userIDs` fourni doit utiliser un `namespace` et un `type` spécifiques en fonction de la banque de données concernée. IDs for the [!DNL Data Lake] must use &quot;unregistered&quot; for their `type` value, and a `namespace` value that matches one the [privacy labels](#privacy-labels) that have been added to applicable datasets.

En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. When making requests to the [!DNL Data Lake], the array must include the value `aepDataLake`.

The following request creates a new privacy job for the [!DNL Data Lake], using the unregistered &quot;email_label&quot; namespace. It also includes the product value for the [!DNL Data Lake] in the `include` array:

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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## Traitement des demandes de suppression

When [!DNL Experience Platform] receives a delete request from [!DNL Privacy Service], [!DNL Platform] sends confirmation to [!DNL Privacy Service] that the request has been received and affected data has been marked for deletion. The records are then removed from the [!DNL Data Lake] within seven days. During that seven-day window, the data is soft-deleted and is therefore not accessible by any [!DNL Platform] service.

In future releases, [!DNL Platform] will send confirmation to [!DNL Privacy Service] after data has been physically deleted.

## Étapes suivantes

By reading this document, you have been introduced to the important concepts involved with processing privacy requests for the [!DNL Data Lake]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

Consultez le document à propos du [traitement des requêtes de confidentialité pour Real-time Customer ](../profile/privacy.md) afin de connaître les étapes du traitement des demandes d’accès à des informations personnelles pour la banque de profils.[!DNL Profile]

## Annexe

La section suivante contient des informations supplémentaires pour le traitement des demandes de confidentialité dans le [!DNL Data Lake].

### Étiquetage des champs imbriqués de type map {#nested-maps}

Il faut souligner qu’il existe deux types de champs imbriqués de type map qui ne prennent pas en charge l’étiquetage de confidentialité :

* Champ de type map dans un champ de type tableau
* Champ de type map dans un autre champ de type map

Le traitement des tâches concernant la confidentialité pour l’un ou l’autre des deux exemples ci-dessus échouera. C’est pourquoi il est recommandé d’éviter d’utiliser des champs imbriqués de type map pour stocker des données clients privées. Les identifiants clients pertinents doivent être stockés sous la forme d’un type de données non mappé dans le champ `identityMap` (lui-même un champ de type map) pour les jeux de données basés sur des enregistrements, ou dans le champ `endUserID` pour les jeux de données basés sur des séries temporelles.