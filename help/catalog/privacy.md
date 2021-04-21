---
keywords: Experience Platform ; accueil ; sujets populaires ; confidentialité des données sur les lacs ; espaces de nommage d'identité ; confidentialité ; données sur le lac
solution: Experience Platform
title: Traitement des demandes de confidentialité dans Data Lake
topic-legacy: overview
description: Adobe Experience Platform Privacy Service traite les demandes d’accès, de opt-out de vente ou de suppression de leurs données personnelles conformément aux réglementations légales et organisationnelles en matière de confidentialité. Ce document couvre les concepts fondamentaux liés au traitement des demandes d’accès à des informations personnelles concernant les données clients stockées dans le lac de données.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 35%

---

# Traitement de la demande de confidentialité dans [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] traite les demandes des clients d&#39;accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux réglementations légales et organisationnelles en matière de confidentialité.

Ce document couvre les concepts essentiels liés au traitement des demandes de confidentialité pour les données client stockées dans [!DNL Data Lake].

## Prise en main

Il est recommandé de bien comprendre les services [!DNL Experience Platform] suivants avant de lire ce guide :

* [[!DNL Privacy Service]](../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): Système d’enregistrement pour l’emplacement et le lignage des données dans  [!DNL Experience Platform]. Fournit une API qui peut être utilisée pour mettre à jour les métadonnées des jeux de données.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
* [[!DNL Identity Service]](../identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.

## Compréhension des espaces de noms d’identité {#namespaces}

Adobe Experience Platform [!DNL Identity Service] relie les données d&#39;identité des clients entre les systèmes et les périphériques. [!DNL Identity Service] utilise les espaces de noms d’identité pour fournir un contexte aux valeurs d’identité en les reliant à leur système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

[!DNL Identity Service] conserve un stock d’espaces de nom d’identité définis globalement (standard) et par l’utilisateur (personnalisés). Les espaces de noms standard sont disponibles pour toutes les organisations (par exemple, « E-mail » et « ECID »), tandis que votre organisation peut aussi créer des espaces de noms personnalisés adaptés à ses besoins spécifiques.

Pour plus d&#39;informations sur les espaces de nommage d&#39;identité dans [!DNL Experience Platform], consultez la [présentation de l&#39;espace de nommage d&#39;identité](../identity-service/namespaces.md).

## Ajouter des données d&#39;identité aux jeux de données

Lors de la création de requêtes de confidentialité pour [!DNL Data Lake], des valeurs d&#39;identité valides (et leurs espaces de nommage associés) doivent être fournies pour chaque client afin de localiser ses données et de les traiter en conséquence. Par conséquent, tous les jeux de données qui font l’objet de demandes de confidentialité doivent contenir un descripteur d’identité dans leur schéma XDM associé.

>[!NOTE]
>
>Les jeux de données basés sur des schémas qui ne prennent pas en charge les métadonnées des descripteurs d’identité (tels que les jeux de données ad hoc) ne peuvent pas actuellement être traités dans les demandes de confidentialité.

Cette section décrit les étapes à suivre pour ajouter un descripteur d&#39;identité au schéma XDM d&#39;un jeu de données existant. Si vous disposez déjà d’un jeu de données avec un descripteur d’identité, vous pouvez passer à la section [suivante](#nested-maps).

>[!IMPORTANT]
>
>Lorsque vous décidez des champs de schéma à définir en tant qu’identités, gardez à l’esprit les [limites de l’utilisation de champs de type de mappage imbriqués](#nested-maps).

Il existe deux méthodes pour ajouter un descripteur d&#39;identité à un schéma de jeux de données :

* [Utilisation de l’interface utilisateur](#identity-ui)
* [Utilisation de l’API](#identity-api)

### Utilisation de l’interface utilisateur {#identity-ui}

Dans l&#39;interface utilisateur [!DNL Experience Platform ], l&#39;espace de travail **[!UICONTROL Schémas]** vous permet de modifier vos schémas XDM existants. Pour ajouter un descripteur d&#39;identité à un schéma, sélectionnez le schéma dans la liste et suivez les étapes pour [définir un champ de schéma en tant que champ d&#39;identité](../xdm/tutorials/create-schema-ui.md#identity-field) dans le didacticiel [!DNL Schema Editor].

Une fois que vous avez défini les champs appropriés du schéma comme champs d’identité, vous pouvez passer à la section suivante sur [l’envoi de demandes de confidentialité](#submit).

### Utilisation de l’API {#identity-api}

>[!NOTE]
>
>Cette section suppose que vous connaissez la valeur d&#39;ID URI unique du schéma XDM de votre jeu de données. Si vous ne connaissez pas cette valeur, vous pouvez la récupérer à l’aide de l’API [!DNL Catalog Service]. Après avoir lu la section [prise en main](./api/getting-started.md) du guide du développeur, suivez les étapes décrites dans la section [énumération](./api/list-objects.md) ou [recherche d&#39;objets ](./api/look-up-object.md) [!DNL Catalog] pour trouver votre jeu de données. L&#39;ID de schéma se trouve sous `schemaRef.id`
>
> Cette section comprend des appels à l&#39;API de registre du Schéma. Pour obtenir des informations importantes sur l&#39;utilisation de l&#39;API, y compris la connaissance de votre `{TENANT_ID}` et du concept de conteneur, consultez la section [prise en main](../xdm/api/getting-started.md) du guide du développeur.

Vous pouvez ajouter un descripteur d&#39;identité au schéma XDM d&#39;un jeu de données en envoyant une requête de POST au point de terminaison `/descriptors` de l&#39;API [!DNL Schema Registry].

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
| `xdm:namespace` | L&#39;un des [espaces de nommage d&#39;identité standard](../privacy-service/api/appendix.md#standard-namespaces) reconnus par [!DNL Privacy Service], ou un espace de nommage personnalisé défini par votre organisation. |
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
>Cette section explique comment formater les demandes de confidentialité pour [!DNL Data Lake]. Il est vivement recommandé de consulter la documentation [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) ou [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) pour connaître les étapes complètes de l’envoi d’une tâche de confidentialité, y compris la manière de formater correctement les données d’identité utilisateur envoyées dans les charges de demande.

La section suivante décrit comment effectuer des demandes de confidentialité pour [!DNL Data Lake] à l&#39;aide de l&#39;interface utilisateur ou de l&#39;API [!DNL Privacy Service].

>[!IMPORTANT]
>
>Le temps qu&#39;une demande de protection des renseignements personnels peut prendre pour être traitée ne peut pas être garanti. Si des changements se produisent dans Data Lake alors qu’une demande est en cours de traitement, il n’est pas non plus possible de garantir que ces dossiers sont traités ou non.

### Utilisation de l’interface utilisateur

Lors de la création de requêtes de tâche dans l’interface utilisateur, veillez à bien sélectionner **[!UICONTROL AEP]** et/ou **[!UICONTROL Profile]** sous **[!UICONTROL Produits]** afin de traiter les tâches pour les données stockées respectivement dans le lac de données ou dans .[!DNL Data Lake][!DNL Real-time Customer Profile]

<img src="images/privacy/product-value.png" width="450"><br>

### Utilisation de l’API

Lors de la création de requêtes de tâche dans l’API, tout `userIDs` fourni doit utiliser un `namespace` et un `type` spécifiques en fonction de la banque de données concernée. Les identifiants de [!DNL Data Lake] doivent utiliser &quot;non inscrit&quot; pour leur valeur `type` et une valeur `namespace` qui correspond à l&#39;une des [étiquettes de confidentialité](#privacy-labels) qui ont été ajoutées aux jeux de données applicables.

En outre, le tableau `include` du payload de requête doit inclure les valeurs de produit pour les différentes banques de données vers lesquelles la requête est effectuée. Lorsque vous envoyez des requêtes à [!DNL Data Lake], le tableau doit inclure la valeur `aepDataLake`.

La demande suivante crée une nouvelle tâche de confidentialité pour [!DNL Data Lake], à l&#39;aide de l&#39;espace de nommage &quot;email_label&quot; non enregistré. Il inclut également la valeur de produit pour [!DNL Data Lake] dans la baie `include` :

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

Lorsque [!DNL Experience Platform] reçoit une demande de suppression de [!DNL Privacy Service], [!DNL Platform] envoie une confirmation à [!DNL Privacy Service] que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite supprimés du [!DNL Data Lake] dans un délai de sept jours. Pendant cette période de sept jours, les données sont supprimées à l&#39;écran et ne sont donc accessibles à aucun service [!DNL Platform].

Dans les prochaines versions, [!DNL Platform] enverra une confirmation à [!DNL Privacy Service] une fois les données physiquement supprimées.

## Étapes suivantes

En lisant ce document, vous avez été initié aux concepts importants liés au traitement des demandes de confidentialité pour le [!DNL Data Lake]. Il est recommandé de continuer la lecture de la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches concernant la confidentialité.

Consultez le document à propos du [traitement des requêtes de confidentialité pour Real-time Customer ](../profile/privacy.md) afin de connaître les étapes du traitement des demandes d’accès à des informations personnelles pour la banque de profils.[!DNL Profile]

## Annexe

La section suivante contient des informations supplémentaires pour le traitement des demandes de confidentialité dans [!DNL Data Lake].

### Étiquetage des champs imbriqués de type map {#nested-maps}

Il faut souligner qu’il existe deux types de champs imbriqués de type map qui ne prennent pas en charge l’étiquetage de confidentialité :

* Champ de type map dans un champ de type tableau
* Champ de type map dans un autre champ de type map

Le traitement des tâches concernant la confidentialité pour l’un ou l’autre des deux exemples ci-dessus échouera. C’est pourquoi il est recommandé d’éviter d’utiliser des champs imbriqués de type map pour stocker des données clients privées. Les identifiants clients pertinents doivent être stockés sous la forme d’un type de données non mappé dans le champ `identityMap` (lui-même un champ de type map) pour les jeux de données basés sur des enregistrements, ou dans le champ `endUserID` pour les jeux de données basés sur des séries temporelles.
