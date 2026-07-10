---
title: Modèle CSV vers le point d’entrée de l’API de conversion de schéma
description: Le point d’entrée /rpc/csv2schema de l’API Schema Registry vous permet d’utiliser des modèles CSV pour créer automatiquement des schémas de modèle de données d’expérience (XDM).
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
TQID: https://experienceleague.adobe.com/5kR3-cOBH1lBfzP0iuY-Z3wmxJh4DlG2jWOBWh5CRRs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 858
ht-degree: 6%

---

# Modèle CSV vers le point d’entrée de l’API de conversion de schéma

Le point d’entrée `/rpc/csv2schema` de l’API [!DNL Schema Registry] vous permet de créer automatiquement un schéma de modèle de données d’expérience (XDM) à l’aide d’un fichier CSV comme modèle. Grâce à ce point d’entrée, vous pouvez créer des modèles pour importer en bloc des champs de schéma et réduire le travail manuel sur l’API ou l’interface utilisateur.

## Prise en main

Le point d’entrée `/rpc/csv2schema` fait partie de l’[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry). Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API Adobe Experience Platform.

Le point d&#39;entrée `/rpc/csv2schema` fait partie des appels de procédure distante (RPC) pris en charge par le [!DNL Schema Registry]. Contrairement aux autres points d&#39;entrée de l&#39;API [!DNL Schema Registry], les points d&#39;entrée RPC ne nécessitent pas d&#39;en-têtes supplémentaires tels que `Accept` ou `Content-Type`, et n&#39;utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l’espace de noms `/rpc`, comme illustré dans les appels d’API ci-dessous.

## Exigences relatives aux fichiers CSV

Pour utiliser ce point d’entrée, vous devez d’abord créer un fichier CSV avec les en-têtes de colonne appropriés et les valeurs correspondantes. Certaines colonnes sont obligatoires, tandis que les autres sont facultatives. Le tableau ci-dessous décrit ces colonnes et leur rôle dans la construction du schéma.

| Position de l’en-tête CSV | Nom de l’en-tête CSV | Obligatoire / Facultatif | Description |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Facultatif | Lorsqu’il est inclus et défini sur `true`, indique que le champ n’est pas prêt pour le chargement de l’API et qu’il doit être ignoré. |
| 2 | `isCustom` | Obligatoire | Indique si le champ est un champ personnalisé ou non. |
| 3 | `fieldGroupId` | Facultatif | ID du groupe de champs auquel un champ personnalisé doit être associé. |
| 4 | `fieldGroupName` | (Voir la description) | Nom du groupe de champs auquel associer ce champ.<br><br>Facultatif pour les champs personnalisés n’étendant pas les champs standard existants. Si rien n’est indiqué, le système attribue automatiquement le nom.<br><br>Obligatoire pour les champs standard ou les champs personnalisés étendant des groupes de champs standard, qui est utilisé pour interroger le `fieldGroupId`. |
| 5 | `fieldPath` | Obligatoire | Chemin d’accès complet de la notation par points XDE pour le champ. Pour inclure tous les champs d’un groupe de champs standard (comme indiqué sous `fieldGroupName`), définissez la valeur sur `ALL`. |
| 6 | `displayName` | Facultatif | Titre ou nom d’affichage convivial du champ. Peut également être un alias pour le titre s’il en existe un. |
| 7 | `fieldDescription` | Facultatif | Description du champ. Peut également être un alias pour la description, le cas échéant. |
| 8 | `dataType` | (Voir la description) | Indique le [type de données de base](../schema/field-constraints.md#basic-types) pour le champ. Obligatoire pour tous les champs personnalisés.<br><br>Si `dataType` est défini sur `object`, `properties` ou `$ref` doit également être défini pour la même ligne, mais pas les deux. |
| 9 | `isRequired` | Facultatif | Indique si le champ est obligatoire pour l’ingestion de données. |
| 10 | `isArray` | Facultatif | Indique si le champ est un tableau de son `dataType` indiqué. |
| 11 | `isIdentity` | Facultatif | Indique si le champ est un champ d’identité. |
| 12 | `identityNamespace` | Obligatoire si `isIdentity` est vrai | [espace de noms d’identité](../../identity-service/features/namespaces.md) pour le champ d’identité. |
| 13 | `isPrimaryIdentity` | Facultatif | Indique si le champ est l’identité principale du schéma. |
| 14 | `minimum` | Facultatif | (Pour les champs numériques uniquement) Valeur minimale du champ. |
| 15 | `maximum` | Facultatif | (Pour les champs numériques uniquement) Valeur maximale du champ. |
| 16 | `enum` | Facultatif | Liste des valeurs d’énumération du champ, exprimées sous la forme d’un tableau (`[value1,value2,value3]`, par exemple). |
| 17 | `stringPattern` | Facultatif | (Pour les champs de chaîne uniquement) Modèle RegEx auquel la valeur de chaîne doit correspondre pour réussir la validation lors de l’ingestion des données. |
| 18 | `format` | Facultatif | (Pour les champs de chaîne uniquement) Format du champ de chaîne. |
| 19 | `minLength` | Facultatif | (Pour les champs de chaîne uniquement) Longueur minimale du champ de chaîne. |
| 20 | `maxLength` | Facultatif | (Pour les champs de chaîne uniquement) Longueur maximale du champ de chaîne. |
| 21 | `properties` | (Voir la description) | Obligatoire si `dataType` est défini sur `object` et `$ref` n’est pas défini. Cela définit le corps de l’objet comme une chaîne JSON (par exemple, `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Voir la description) | Obligatoire si `dataType` est défini sur `object` et `properties` n’est pas défini. Cela définit le `$id` de l’objet référencé pour le type d’objet (par exemple, `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Facultatif | Lorsque `isIgnored` est défini sur `true`, cette colonne est utilisée pour fournir les informations d’en-tête du schéma. |

{style="table-layout:auto"}

Reportez-vous au [modèle CSV](../assets/sample-csv-template.csv) suivant pour déterminer comment votre fichier CSV doit être formaté.

## Création d’une payload d’exportation à partir d’un fichier CSV

Une fois que vous avez configuré votre modèle CSV, vous pouvez envoyer le fichier au point d’entrée `/rpc/csv2schema` et le convertir en payload d’exportation.

**Format d’API**

```http
POST /rpc/csv2schema
```

**Requête**

Le payload de la requête doit utiliser les données de formulaire comme format. Les champs de formulaire obligatoires sont affichés ci-dessous.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Propriété | Description |
| --- | --- |
| `csv-file` | Chemin d’accès au modèle CSV stocké sur votre ordinateur local. |
| `schema-class-id` | `$id` de la classe XDM [class](../schema/composition.md#class) que ce schéma utilisera. |
| `schema-name` | Nom d’affichage du schéma. |
| `schema-description` | Description du schéma. |

**Réponse**

Une réponse réussie renvoie une payload d’exportation générée à partir du fichier CSV. La payload prend la forme d’un tableau, et chaque élément du tableau est un objet qui représente un composant XDM dépendant pour le schéma. Sélectionnez la section ci-dessous pour afficher un exemple complet de payload d’exportation générée à partir d’un fichier CSV.

+++ Exemple de payload de réponse

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## Importer la payload du schéma

Après avoir généré la payload d’exportation à partir du fichier CSV, vous pouvez envoyer cette payload au point d’entrée `/rpc/import` pour générer le schéma.

Pour plus d’informations sur la génération de schémas à partir de payloads d’exportation[&#128279;](./import.md) consultez le  guide de point d’entrée d’importation .

