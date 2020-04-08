---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Traitement des demandes de confidentialité dans Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# Traitement des demandes de confidentialité dans Data Lake

Le service de confidentialité d’Adobe Experience Platform traite les demandes des clients d’accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux règles de confidentialité, telles que le Règlement général sur la protection des données (RDDC) et la Loi sur la protection des renseignements personnels des consommateurs (LPCA) de Californie.

Ce couvre les concepts essentiels liés au traitement des demandes de confidentialité pour les données des clients stockées dans Data Lake.

## Prise en main

Il est recommandé de bien comprendre les services Experience Platform suivants avant de lire ce guide :

* [Privacy Service](../privacy-service/home.md): Gère les demandes des clients pour accéder aux applications Adobe Experience Cloud, les exclure de la vente ou les supprimer.
* [Service](home.md)de catalogue : Système d’enregistrement pour l’emplacement et la lignée des données dans la plateforme d’expérience. Fournit une API qui peut être utilisée pour mettre à jour les métadonnées des jeux de données.
* [Système](../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.

## Ajout de libellés de confidentialité aux jeux de données {#privacy-labels}

Pour qu’un jeu de données soit traité dans une demande de confidentialité pour le lac Data, il faut lui donner des étiquettes de confidentialité. Les étiquettes de confidentialité indiquent les champs du  associé d&#39;un jeu de données qui s&#39;appliquent au  que vous prévoyez d&#39;envoyer dans les demandes de confidentialité.

Cette section explique comment ajouter des étiquettes de confidentialité à un jeu de données en vue de l’utiliser dans des demandes de confidentialité de Data Lake. Pour commencer, tenez compte du jeu de données suivant :

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

La `schemaMetadata` propriété du jeu de données contient un `gdpr` tableau, qui est actuellement vide. Pour ajouter des libellés de confidentialité au jeu de données, ce tableau doit être mis à jour à l’aide d’une requête PATCH dans l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catalogue.

>[!NOTE] Bien que la baie soit nommée `gdpr`, l&#39;ajout d&#39;étiquettes lui permettra d&#39;effectuer des demandes de travail de confidentialité pour les règlements du RDPC et de l&#39;ACCP.

**Format API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` du jeu de données à mettre à jour. |

**Requête**

Dans cet exemple, un jeu de données inclut une adresse électronique dans le `personalEmail.address` champ. Pour que ce champ serve d’identificateur aux demandes de confidentialité de Data Lake, une étiquette qui utilise un  de  non enregistré doit être ajoutée à son `gdpr` tableau.

La requête suivante ajoute un libellé de confidentialité qui affecte le   &quot;email_label&quot; au `personalEmail.address` champ.

>[!IMPORTANT] Lors de l’exécution d’une opération PATCH sur la `schemaMetadata` propriété d’un jeu de données, veillez à copier toutes les sous-propriétés existantes dans la charge utile de requête. Si vous excluez des valeurs existantes de la charge utile, elles seront supprimées du jeu de données.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Propriété | Description |
| --- | --- |
| `namespace` | Un tableau répertoriant les   à associer au champ spécifié dans `path`.   sont utilisés pour identifier les champs liés à la confidentialité lors de l’ [envoi de demandes](#submit) d’accès ou de suppression dans l’API de Privacy Service. |
| `path` | Chemin d’accès au champ dans l’ associé du jeu de données qui s’applique au `namespace`. Idéalement, les libellés de confidentialité ne doivent être appliqués qu’aux champs &quot;feuille&quot; (champs sans sous-champs). |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 (OK) avec l’ID du jeu de données fourni dans la charge utile. L’utilisation de l’ID pour rechercher à nouveau le jeu de données révèle que les libellés de confidentialité ont été ajoutés.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Étiquetage des champs de type de mappage imbriqués

Il est important de noter qu’il existe deux types de champs de type carte imbriqués qui ne prennent pas en charge l’étiquetage de confidentialité :

* Champ de type de mappage dans un champ de type de tableau
* Un champ de type de mappage dans un autre champ de type de mappage

Le traitement des tâches de confidentialité pour l’un ou l’autre des deux exemples ci-dessus échouera. C’est pourquoi il est recommandé d’éviter d’utiliser des champs de type de mappage imbriqués pour stocker des données client privées. Les ID de consommateur pertinents doivent être stockés sous la forme d’un type de données non mappé dans le `identityMap` champ (qui est lui-même un champ de type mappage) pour les jeux de données basés sur des enregistrements, ou `endUserID` le champ pour les jeux de données basés sur des séries chronologiques.

## Envoi de requêtes {#submit}

>[!NOTE] Cette section explique comment formater les demandes de protection de la vie privée pour le lac Data. Il est vivement recommandé de consulter l’API [](../privacy-service/api/getting-started.md) Privacy Service ou la documentation de l’interface utilisateur [de](../privacy-service/ui/overview.md) Privacy Service pour obtenir des instructions complètes sur la manière d’envoyer une tâche de confidentialité, y compris sur la manière de formater correctement les données d’identité utilisateur envoyées dans les charges de demande.

La section suivante explique comment effectuer des demandes de confidentialité pour Data Lake à l’aide de l’API ou de l’interface utilisateur de Privacy Service.

### Utilisation de l’API

Lors de la création de demandes de tâche dans l’API, les demandes `userIDs` fournies doivent utiliser une valeur spécifique `namespace` et `type` en fonction du magasin de données auquel elles s’appliquent. Les ID de Data Lake doivent utiliser &quot;non inscrit&quot; pour leur `type` valeur et une `namespace` valeur correspondant à l’une des étiquettes [de](#privacy-labels) confidentialité ajoutées aux jeux de données applicables.

En outre, le `include` tableau de la charge utile de requête doit inclure les valeurs de produit pour les différents entrepôts de données auxquels la demande est effectuée. Lorsque vous faites des demandes au lac Data, le tableau doit inclure la valeur &quot;aepDataLake&quot;.

La requête suivante crée une nouvelle tâche de confidentialité pour Data Lake, à l’aide du  non enregistré &quot;email_label&quot; . Il inclut également la valeur du produit pour le lac Data dans la `include` baie :

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

### Utilisation de l’interface utilisateur

Lors de la création de demandes d’emploi dans l’interface utilisateur, veillez à sélectionner **AEP Data Lake** et/ou le **de produits** sous _Produits_ afin de traiter les tâches pour les données stockées dans le  de données Data Lake ou dans le client en temps réel, respectivement.

<img src="images/privacy/product-value.png" width="450"><br>

## Supprimer le traitement de requête

Lorsque la plateforme d’expérience reçoit une demande de suppression de la part de Privacy Service, la plate-forme envoie une confirmation au service de confidentialité pour confirmer que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite retirés du lac Data dans les sept jours. Pendant cette période de sept jours, les données sont supprimées à l’écran et ne sont donc accessibles à aucun service de plateforme.

Dans les prochaines versions, Platform enverra une confirmation à Privacy Service une fois les données physiquement supprimées.

## Étapes suivantes

En lisant ce , vous avez été familiarisé avec les concepts importants liés au traitement des demandes de protection de la vie privée pour le lac Data. Il est recommandé de continuer à lire la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d’identité et créer des tâches de confidentialité.

Consultez le  sur le traitement des demandes de [confidentialité pour le](../profile/privacy.md) client en temps réel pour connaître les étapes du traitement des demandes de confidentialité pour le magasin d&#39; de la solution.