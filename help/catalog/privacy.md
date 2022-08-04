---
keywords: Experience Platform;accueil;rubriques populaires;confidentialité du lac de données;espaces de noms dʼidentité;confidentialité;lac de données
solution: Experience Platform
title: Traitement des demandes dʼaccès à des informations personnelles dans le lac de données
topic-legacy: overview
description: Adobe Experience Platform Privacy Service traite les demandes des clients dʼaccès, de retrait du consentement à la vente ou de suppression de leurs données personnelles conformément aux réglementations légales et organisationnelles en matière de confidentialité. Ce document couvre les concepts essentiels liés au traitement des demandes d’accès à des informations personnelles pour les données clients stockées dans le lac de données.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 159a46fa227207bf161100e50bc286322ba2d00b
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 77%

---

# Traitement des demandes d’accès à des informations personnelles dans le lac de données

Adobe Experience Platform [!DNL Privacy Service] traite les demandes des clients dʼaccès, de retrait du consentement à la vente ou de suppression de leurs données personnelles conformément aux réglementations légales et organisationnelles en matière de confidentialité.

Ce document couvre les concepts essentiels liés au traitement des demandes d’accès à des informations personnelles pour les données clients stockées dans le lac de données.

>[!NOTE]
>
>Ce guide porte uniquement sur la manière d’effectuer des demandes d’accès à des informations personnelles pour le lac de données en Experience Platform. Si vous prévoyez également d’effectuer des demandes d’accès à des informations personnelles pour la banque de données du profil client en temps réel, reportez-vous au guide sur le [traitement des demandes d’accès à des informations personnelles pour le profil](../profile/privacy.md) en plus de ce tutoriel.
>
>Pour savoir comment effectuer des demandes d’accès à des informations personnelles pour d’autres applications Adobe Experience Cloud, reportez-vous à la [documentation du Privacy Service](../privacy-service/experience-cloud-apps.md).

## Prise en main

Une connaissance concrète des services [!DNL Experience Platform] suivants est recommandée avant la lecture de ce guide :

* [[!DNL Privacy Service]](../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md) : système dʼenregistrement de lʼemplacement et de la traçabilité des données dans [!DNL Experience Platform]. Fournit une API qui peut être utilisée pour mettre à jour les métadonnées des jeux de données.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] rapproche les données dʼidentité client entre les systèmes et les appareils. [!DNL Identity Service] utilise les espaces de noms d’identité pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse e-mail (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

[!DNL Identity Service] conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus dʼinformations sur les espaces de noms dʼidentité dans [!DNL Experience Platform], consultez la [présentation de lʼespace de noms dʼidentité](../identity-service/namespaces.md).

## Ajouter des données dʼidentité aux jeux de données

Lors de la création de demandes d’accès à des informations personnelles pour le lac de données, des valeurs d’identité valides (et leurs espaces de noms associés) doivent être fournies pour chaque client afin de localiser ses données et de les traiter en conséquence. Par conséquent, tous les jeux de données qui font lʼobjet de demandes dʼaccès à des informations personnelles doivent contenir un descripteur dʼidentité dans leur schéma XDM associé.

>[!NOTE]
>
>Les jeux de données basés sur les schémas qui ne prennent pas en charge les métadonnées des descripteurs dʼidentité (tels que les jeux de données ad hoc) ne peuvent actuellement pas être traités lors des demandes dʼaccès à des informations personnelles.

Cette section vous explique étape par étape comment ajouter un descripteur dʼidentité au schéma XDM dʼun jeu de données existant. Si vous disposez déjà dʼun jeu de données avec un descripteur dʼidentité, vous pouvez passer à la [section suivante](#nested-maps).

>[!IMPORTANT]
>
>Lorsque vous décidez des champs de schéma à définir en tant quʼidentités, gardez à lʼesprit les [limites de lʼutilisation de champs imbriqués de type map](#nested-maps).

Il existe deux méthodes pour ajouter un descripteur dʼidentité à un schéma de jeu de données :

* [Utilisation de l’interface utilisateur](#identity-ui)
* [Utilisation de l’API](#identity-api)

### Utilisation de l’interface utilisateur {#identity-ui}

Dans lʼinterface utilisateur dʼ[!DNL Experience Platform ], lʼespace de travail **[!UICONTROL Schémas]** vous permet de modifier vos schémas XDM existants. Pour ajouter un descripteur dʼidentité à un schéma, sélectionnez le schéma dans la liste et suivez les étapes pour [définir un champ de schéma en tant que champ dʼidentité](../xdm/tutorials/create-schema-ui.md#identity-field) dans le tutoriel de [!DNL Schema Editor].

Une fois que vous avez défini les champs appropriés dans le schéma en tant que champs dʼidentité, vous pouvez passer à la section suivante sur lʼ[envoi de demandes dʼaccès à des informations personnelles](#submit).

### Utilisation de l’API {#identity-api}

>[!NOTE]
>
>Cette section suppose que vous connaissez la valeur unique de lʼidentifiant URI du schéma XDM de votre jeu de données. Si vous ne connaissez pas cette valeur, vous pouvez la récupérer à lʼaide de lʼAPI [!DNL Catalog Service]. Après avoir lu la section [prise en main](./api/getting-started.md) du guide du développeur, suivez les étapes décrites dans la section pour [répertorier](./api/list-objects.md) ou [rechercher des objets ](./api/look-up-object.md) [!DNL Catalog] pour trouver votre jeu de données. Lʼidentifiant de schéma se trouve sous `schemaRef.id`
>
>Cette section suppose également que vous savez comment effectuer des appels vers l’API Registre de schémas. Pour obtenir des informations importantes sur lʼutilisation de lʼAPI, y compris la connaissance de votre `{TENANT_ID}` et du concept des conteneurs, consultez la section [prise en main](../xdm/api/getting-started.md) du guide API. 

Vous pouvez ajouter un descripteur dʼidentité au schéma XDM dʼun jeu de données en envoyant une requête POST au point d’entrée `/descriptors` de lʼAPI [!DNL Schema Registry].

**Format d’API**

```http
POST /descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité dans un champ « adresse e-mail » d’un exemple de schéma.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `@type` | Le type de descripteur en cours de création. Pour les descripteurs dʼidentité, la valeur doit être « xdm:descriptorIdentity ». |
| `xdm:sourceSchema` | Lʼidentifiant URI unique du schéma XDM de votre jeu de données. |
| `xdm:sourceVersion` | Version du schéma XDM spécifiée dans `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Chemin du champ de schéma auquel le descripteur est appliqué. |
| `xdm:namespace` | Lʼun des [espaces de noms dʼidentité standard](../privacy-service/api/appendix.md#standard-namespaces) reconnus par [!DNL Privacy Service], ou un espace de noms personnalisé défini par votre organisation. |
| `xdm:property` | « xdm:id » ou « xdm:code », selon lʼespace de noms utilisé sous `xdm:namespace`. |
| `xdm:isPrimary` | Une valeur booléenne facultative. Lorsque la valeur est « true », cela indique que le champ est une identité principale. Les schémas ne peuvent contenir qu’une seule identité principale. La valeur par défaut est « false » si elle nʼest pas incluse. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails du nouveau descripteur.

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
>Cette section explique comment formater les demandes d’accès à des informations personnelles pour le lac de données. Il est vivement recommandé de consulter la documentation de lʼ[[!DNL Privacy Service] interface utilisateur](../privacy-service/ui/overview.md) ou de lʼ[[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) pour obtenir des instructions complètes sur la manière dʼenvoyer une tâche concernant la confidentialité, y compris sur la manière de formater correctement les données dʼidentité utilisateur envoyées dans les payloads de requête.

La section suivante explique comment effectuer des demandes d’accès à des informations personnelles pour le lac de données à l’aide de la variable [!DNL Privacy Service] Interface utilisateur ou API.

>[!IMPORTANT]
>
>Le délai de traitement dʼune demande dʼaccès à des informations personnelles ne peut être garanti. Si des modifications se produisent dans le lac de données alors qu’une demande est toujours en cours de traitement, le fait que ces enregistrements soient traités ou non ne peut pas non plus être garanti.

### Utiliser l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à sélectionner **[!UICONTROL Lac de données AEP]** under **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées dans le lac de données.

![Image montrant le produit de lac de données sélectionné dans la boîte de dialogue de création de demande d’accès à des informations personnelles](./images/privacy/product-value.png)

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, tout `userIDs` fourni doit utiliser un `namespace` et un `type` spécifiques en fonction de la banque de données concernée. Les identifiants du lac de données doivent utiliser `unregistered` pour leur `type` et une `namespace` qui correspond à l’une des valeurs [étiquettes de confidentialité](#privacy-labels) qui ont été ajoutés aux jeux de données applicables.

En outre, le tableau `include` de la payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Lors de l’envoi de requêtes au lac de données, le tableau doit inclure la valeur `aepDataLake`.

La requête suivante crée une nouvelle tâche de confidentialité pour le lac de données, en utilisant le paramètre non enregistré `email_label` espace de noms. Elle inclut également la valeur du produit pour le lac de données dans la variable `include` tableau :

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

>[!IMPORTANT]
>
>Platform traite les demandes d’accès à des informations personnelles dans toutes les [sandbox](../sandboxes/home.md) appartenant à votre organisation. Par conséquent, tout en-tête `x-sandbox-name` inclus dans la demande est ignoré par le système. 

## Traitement des demandes de suppression

Lorsquʼ[!DNL Experience Platform] reçoit une requête DELETE de la part de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] pour confirmer que la requête a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite retirés du lac de données dans les sept jours. Pendant cette période de sept jours, les données subissent une suppression réversible, elles ne sont donc accessibles par aucun service [!DNL Platform].

Si vous avez également inclus `ProfileService` ou `identity` dans la demande d’accès à des informations personnelles, les données qui lui sont associées sont traitées séparément. Voir la section sur [traitement des requêtes de suppression pour Profile](../profile/privacy.md#delete) pour plus d’informations.

## Étapes suivantes

En lisant ce document, vous avez découvert les concepts importants liés au traitement des demandes d’accès à des informations personnelles pour le lac de données. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

Consultez le document à propos du [traitement des requêtes de confidentialité pour Real-time Customer ](../profile/privacy.md) afin de connaître les étapes du traitement des demandes d’accès à des informations personnelles pour la banque de [!DNL Profile] profils.

## Annexe

La section suivante contient des informations supplémentaires sur le traitement des demandes d’accès à des informations personnelles dans le lac de données.

### Étiquetage des champs imbriqués de type map {#nested-maps}

Il faut souligner qu’il existe deux types de champs imbriqués de type map qui ne prennent pas en charge l’étiquetage de confidentialité :

* Champ de type map dans un champ de type tableau
* Champ de type map dans un autre champ de type map

Le traitement des tâches concernant la confidentialité pour l’un ou l’autre des deux exemples ci-dessus échouera. C’est pourquoi il est recommandé d’éviter d’utiliser des champs imbriqués de type map pour stocker des données clients privées. Les identifiants clients pertinents doivent être stockés sous la forme d’un type de données non mappé dans le champ `identityMap` (lui-même un champ de type map) pour les jeux de données basés sur des enregistrements, ou dans le champ `endUserID` pour les jeux de données basés sur des séries temporelles.
