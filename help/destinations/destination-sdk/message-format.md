---
description: Cette page traite du format du message et de la transformation des profils dans les données exportées de Adobe Experience Platform vers les destinations.
title: Format des messages
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 4%

---

# Format des messages

## Conditions préalables - Concepts Adobe Experience Platform {#prerequisites}

Pour comprendre le format des messages, le processus de configuration et de transformation des profils du côté Adobe, familiarisez-vous avec les concepts Experience Platform suivants :

* **Modèle de données d’expérience (XDM)**. [Présentation de XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) et  [Création d’un schéma XDM dans Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=fr).
* **Classe**. [Création et modification de classes dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. La carte des identités représente une carte de toutes les identités des utilisateurs finaux dans Adobe Experience Platform. Voir `xdm:identityMap` dans le [Dictionnaire des champs XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. Le [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) L’attribut XDM indique les segments dont un profil est membre. Pour les trois valeurs différentes de la variable `status` , lisez la documentation sur [Groupe de champs Détails de l’appartenance à un segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Aperçu {#overview}

Utilisez le contenu de cette page avec le reste de la variable [options de configuration pour les destinations partenaires](./configuration-options.md). Cette page traite du format du message et de la transformation des profils dans les données exportées de Adobe Experience Platform vers les destinations. L’autre page traite des détails relatifs à la connexion et à l’authentification à votre destination.

Adobe Experience Platform exporte des données vers un nombre important de destinations, dans divers formats de données. Les plateformes publicitaires (Google), les réseaux sociaux (Facebook) et les emplacements de stockage dans le cloud (Amazon S3, Azure Event Hubs) constituent quelques exemples de types de destinations.

Experience Platform peut ajuster le format du message des profils exportés pour qu’il corresponde au format attendu de votre côté. Pour comprendre cette personnalisation, les concepts suivants sont importants :
* Le schéma XDM source (1) et cible (2) dans Adobe Experience Platform
* le format de message attendu du côté partenaire (3), et
* La couche de transformation entre le schéma XDM et le format de message attendu, que vous pouvez définir en créant un [modèle de transformation des messages](./message-format.md#using-templating).

![Schéma vers transformation JSON](./assets/transformations-3-steps.png)

Experience Platform utilise des schémas XDM pour décrire la structure des données de manière cohérente et réutilisable.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Schéma XDM source (1)**: Cet élément fait référence au schéma que les clients utilisent dans Experience Platform. Dans Experience Platform, dans la variable [étape de mappage](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) Dans le workflow d’activation de destination, les clients mappent les champs de leur schéma XDM au schéma cible de votre destination (2).

**Schéma XDM Target (2)**: En fonction du schéma standard JSON (3) du format attendu de votre destination et des attributs que votre destination peut interpréter, vous pouvez définir des attributs de profil et des identités dans votre schéma XDM cible. Vous pouvez le faire dans la configuration des destinations, dans la variable [schemaConfig](./destination-configuration.md#schema-configuration) et [identityNamespaces](./destination-configuration.md#identities-and-attributes) objets.

**Schéma standard JSON de vos attributs de profil de destination (3)**: Cet exemple représente une [Schéma JSON](https://json-schema.org/learn/miscellaneous-examples.html) de tous les attributs de profil pris en charge par votre plateforme et de leurs types (par exemple : objet, chaîne, tableau). Exemples de champs que votre destination peut prendre en charge `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`, etc. Vous avez besoin d’un [modèle de transformation des messages](./message-format.md#using-templating) pour adapter les données exportées depuis l’Experience Platform au format souhaité.

En fonction des transformations de schéma décrites ci-dessus, voici comment une configuration de profil change entre le schéma XDM source et un exemple de schéma du côté partenaire :

![Exemple de message de transformations](./assets/transformations-with-examples.png)

## Prise en main - transformation de trois attributs de base {#getting-started}

Pour démontrer le processus de transformation des profils, l’exemple ci-dessous utilise trois attributs de profil courants dans Adobe Experience Platform : **prénom**, **last name**, et **adresse email**.

>[!NOTE]
>
>Le client mappe les attributs du schéma XDM source au schéma XDM partenaire dans l’interface utilisateur de Adobe Experience Platform, dans la variable **Mappage** de la [Activation du workflow de destination](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

Supposons que votre plateforme puisse recevoir un format de message du type :

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

Au niveau du format du message, les transformations correspondantes sont les suivantes :

| Attribut dans le schéma XDM du partenaire côté Adobe | Transformation | Attribut dans le message HTTP de votre côté |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Structure de profil dans Experience Platform {#profile-structure}

Pour comprendre les exemples ci-dessous dans la page, il est important de connaître la structure d’un profil dans Experience Platform.

Les profils comportent 3 sections :

* `segmentMembership` (toujours présente sur un profil)
   * cette section contient tous les segments présents sur le profil. Les segments peuvent avoir l’un des deux états suivants : `realized` ou `exited`.
* `identityMap` (toujours présente sur un profil)
   * cette section contient toutes les identités présentes sur le profil (email, Google GAID, Apple IDFA, etc.) et que l’utilisateur a mappées pour l’exportation dans le workflow d’activation.
* attributs (selon la configuration de la destination, ils peuvent être présents sur le profil). Il existe également une légère différence entre les attributs prédéfinis et les attributs de forme libre :
   * pour *Attributs de forme libre*, ils contiennent un `.value` chemin si l’attribut est présent sur le profil (voir `lastName` de l’exemple 1). S’ils ne sont pas présents sur le profil, ils ne contiendront pas la variable `.value` path (voir `firstName` de l’exemple 1).
   * pour *attributs prédéfinis*, ils ne contiennent pas de balise `.value` chemin d’accès. Tous les attributs mappés présents sur un profil seront présents dans le mappage des attributs. Ceux qui ne sont pas présents ne seront pas présents (voir Exemple 2 - la section `firstName` n’existe pas sur le profil).

Voir ci-dessous deux exemples de profils en Experience Platform :

### Exemple 1 avec `segmentMembership`, `identityMap` Attributs et pour les attributs de forme libre {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Exemple 2 avec `segmentMembership`, `identityMap` Attributs et pour les attributs prédéfinis {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Utiliser une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments {#using-templating}

Utilisation d’Adobes [Modèles de saisie](https://pebbletemplates.io/), un langage de modèle similaire à [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), pour transformer les champs du schéma XDM Experience Platform en un format pris en charge par votre destination.

Cette section fournit plusieurs exemples de la manière dont ces transformations sont effectuées : du schéma XDM d’entrée au modèle et de sortie dans des formats de payload acceptés par votre destination. Les exemples ci-dessous sont présentés par une complexité croissante, comme suit :

1. Exemples de transformation simples. Découvrez comment le modèle fonctionne avec des transformations simples pour [Attributs de profil](./message-format.md#attributes), [abonnement au segment](./message-format.md#segment-membership), et [Identité](./message-format.md#identities) champs.
2. Exemples de modèles plus complexes combinant les champs ci-dessus : [Créer un modèle qui envoie des segments et des identités](./message-format.md#segments-and-identities) et [Créer un modèle qui envoie des segments, des identités et des attributs de profil](./message-format.md#segments-identities-attributes).
3. Modèles contenant la clé d’agrégation. Lorsque vous utilisez [agrégation configurable](./destination-configuration.md#configurable-aggregation) dans la configuration de destination, Experience Platform groupe les profils exportés vers votre destination en fonction de critères tels que l’identifiant du segment, l’état du segment ou les espaces de noms d’identité.

### Attributs de profil {#attributes}

Pour transformer les attributs de profil exportés vers votre destination, reportez-vous aux exemples de code et JSON ci-dessous.

>[!IMPORTANT]
>
>Pour obtenir la liste de tous les attributs de profil disponibles dans Adobe Experience Platform, reportez-vous à la section [Dictionnaire des champs XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


**Entrée**

Profil 1 :

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Profil 2 :

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Modèle**

>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Résultat**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### Appartenance à un segment {#segment-membership}

Le [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) L’attribut XDM indique les segments dont un profil est membre.
Pour les trois valeurs différentes de la variable `status` , lisez la documentation sur [Groupe de champs Détails de l’appartenance à un segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

**Entrée**

Profil 1 :

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Profil 2 :

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Modèle**


>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Résultat**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identités {#identities}

Pour plus d’informations sur les identités dans Experience Platform, voir [Présentation de l’espace de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr).

**Entrée**

Profil 1 :

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Profil 2 :

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Modèle**


>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Résultat**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### Créer un modèle qui envoie des segments et des identités {#segments-and-identities}

Cette section fournit un exemple de transformation couramment utilisée entre le schéma XDM d’Adobe et le schéma de destination du partenaire.
L’exemple ci-dessous montre comment transformer le format d’adhésion et d’identités au segment et les générer vers votre destination.

**Entrée**

Profil 1 :

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profil 2 :

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Modèle**

>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering segments by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Résultat**

Le `json` ci-dessous représente les données exportées depuis Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Créer un modèle qui envoie des segments, des identités et des attributs de profil {#segments-identities-attributes}

Cette section fournit un exemple de transformation couramment utilisée entre le schéma XDM d’Adobe et le schéma de destination du partenaire.

Un autre cas d’utilisation courant consiste à exporter des données contenant l’appartenance à un segment, des identités (par exemple : adresse électronique, numéro de téléphone, identifiant publicitaire) et attributs de profil. Pour exporter les données de cette manière, reportez-vous à l’exemple ci-dessous :

**Entrée**

Profil 1 :

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profil 2 :

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Modèle**

>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Résultat**

Le `json` ci-dessous représente les données exportées depuis Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Inclure la clé d&#39;agrégation dans votre modèle pour accéder aux profils exportés regroupés selon différents critères {#template-aggregation-key}

Lorsque vous utilisez [agrégation configurable](./destination-configuration.md#configurable-aggregation) dans la configuration de destination, vous pouvez regrouper les profils exportés vers votre destination en fonction de critères tels que l’identifiant du segment, l’alias du segment, l’appartenance au segment ou les espaces de noms d’identité.

Dans le modèle de transformation des messages, vous pouvez accéder aux clés d&#39;agrégation mentionnées ci-dessus, comme illustré dans les exemples des sections suivantes. Utilisez des clés d’agrégation pour structurer le message HTTP exporté hors Experience Platform afin qu’il corresponde aux limites de format et de taux attendues par votre destination.

#### Utiliser la clé d’agrégation des identifiants de segment dans le modèle {#aggregation-key-segment-id}

Si vous utilisez [agrégation configurable](./destination-configuration.md#configurable-aggregation) et défini `includeSegmentId` sur true, les profils dans les messages HTTP exportés vers votre destination sont regroupés par identifiant de segment. Reportez-vous à la section ci-dessous pour accéder à l’identifiant de segment dans le modèle.

**Entrée**

Tenez compte des quatre profils ci-dessous, où :
* les deux premiers font partie du segment avec l’identifiant de segment. `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* le troisième profil fait partie du segment avec l’identifiant de segment `8f812592-3f06-416b-bd50-e7831848a31a`
* le quatrième profil fait partie des deux segments ci-dessus.

Profil 1 :

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 2 :

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 3 :

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 4 :

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Modèle**

>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Remarquez ci-dessous comment `audienceId` est utilisé dans le modèle pour accéder aux identifiants de segment. Cet exemple suppose que vous utilisez `audienceId` pour l’adhésion au segment dans votre taxonomie de destination. Vous pouvez utiliser n’importe quel autre nom de champ en fonction de votre propre taxonomie.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Résultat**

Lorsqu’ils sont exportés vers votre destination, les profils sont divisés en deux groupes, en fonction de leur identifiant de segment.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Utiliser la clé d’agrégation des alias de segment dans le modèle {#aggregation-key-segment-alias}

Si vous utilisez [agrégation configurable](./destination-configuration.md#configurable-aggregation) et défini `includeSegmentId` sur true, vous pouvez également accéder à l’alias du segment dans le modèle.

Ajoutez la ligne ci-dessous au modèle pour accéder aux profils exportés regroupés par alias de segment.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Utiliser la clé d’agrégation de l’état du segment dans le modèle {#aggregation-key-segment-status}

Si vous utilisez [agrégation configurable](./destination-configuration.md#configurable-aggregation) et défini `includeSegmentId` et `includeSegmentStatus` sur true, vous pouvez accéder à l’état du segment dans le modèle. Ainsi, vous pouvez regrouper les profils dans les messages HTTP exportés vers votre destination selon que les profils doivent être ajoutés ou supprimés des segments.

Les valeurs possibles sont les suivantes :

* réalisé
* existant
* exited

Ajoutez la ligne ci-dessous au modèle pour ajouter ou supprimer des profils des segments, en fonction des valeurs ci-dessus :

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Utiliser la clé d’agrégation de l’espace de noms d’identité dans le modèle {#aggregation-key-identity}

Vous trouverez ci-dessous un exemple où la variable [agrégation configurable](./destination-configuration.md#configurable-aggregation) dans la configuration de destination est définie pour agréger les profils exportés par espaces de noms d’identité, dans le formulaire `"namespaces": ["email", "phone"]` et `"namespaces": ["GAID", "IDFA"]`. Reportez-vous à la section `groups` du paramètre [référence de l’API de configuration de destination](./destination-configuration-api.md) pour plus d’informations sur ce groupement.

**Entrée**

Profil 1 :

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

Profil 2 :

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Modèle**

>[!IMPORTANT]
>
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles. `""` avant d’insérer le modèle dans le [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, reportez-vous au chapitre 9 de la section [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Notez que `input.aggregationKey.identityNamespaces` est utilisé dans le modèle ci-dessous

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Résultat**

Lorsqu’ils sont exportés vers votre destination, les profils sont divisés en deux groupes, en fonction de leurs espaces de noms d’identité. Les courriers électroniques et les téléphones se trouvent dans un groupe, tandis que GAID et IDFA en sont dans un autre.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### Utiliser la clé d&#39;agrégation dans un modèle d&#39;URL {#aggregation-key-url-template}

Selon votre cas d’utilisation, vous pouvez également utiliser les clés d’agrégation décrites ici dans une URL, comme illustré ci-dessous :

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Référence : Contexte et fonctions utilisés dans les modèles de transformation {#reference}

Le contexte fourni au modèle contient `input`  (les profils/données exportés au cours de cet appel) et `destination` (données relatives à la destination vers laquelle l’Adobe envoie des données, valides pour tous les profils).

Le tableau ci-dessous fournit des descriptions des fonctions dans les exemples ci-dessus.

| Fonction | Description |
|---------|----------|
| `input.profile` | Le profil, représenté sous la forme [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Suit le schéma XDM du partenaire mentionné plus haut sur cette page. |
| `destination.segmentAliases` | Mappage des identifiants de segment dans l’espace de noms Adobe Experience Platform aux alias de segment dans le système du partenaire. |
| `destination.segmentNames` | Mappage des noms de segment dans l’espace de noms Adobe Experience Platform aux noms de segment dans le système du partenaire. |
| `addedSegments(listOfSegments)` | Renvoie uniquement les segments ayant un état `realized`. |
| `removedSegments(listOfSegments)` | Renvoie uniquement les segments ayant un état `exited`. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment les données exportées hors d’Experience Platform sont transformées. Lisez ensuite les pages suivantes pour acquérir des connaissances sur la création de modèles de transformation de messages pour votre destination :

* [Créer et tester un modèle de transformation de message](/help/destinations/destination-sdk/create-template.md)
* [Opérations de l’API pour le rendu du modèle](/help/destinations/destination-sdk/render-template-api.md)
* [Fonctions de transformation prises en charge dans Destination SDK](/help/destinations/destination-sdk/supported-functions.md)
