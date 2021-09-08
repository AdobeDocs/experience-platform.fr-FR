---
description: Utilisez le contenu de cette page avec le reste des options de configuration pour les destinations partenaires. Cette page traite du format de message des données exportées de Adobe Experience Platform vers des destinations, tandis que l’autre page traite des détails relatifs à la connexion et à l’authentification à votre destination.
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: Format du message
source-git-commit: d60933d2083b7befcfa8beba4b1630f372c08cfa
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 3%

---

# Format du message

## Conditions préalables - Concepts Adobe Experience Platform {#prerequisites}

Pour comprendre le processus du côté Adobe, familiarisez-vous avec les concepts Experience Platform suivants :

* **Modèle de données d’expérience (XDM)**. [Présentation de XDM ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) et   [création d’un schéma XDM dans Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Classe**. [Créez et modifiez des classes dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **Groupe de champs**. [](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) Définition d’un groupe de champs et  [plus d’informations sur les groupes de champs](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group).
* **IdentityMap**. La carte des identités représente une carte de toutes les identités des utilisateurs finaux dans Adobe Experience Platform. Voir `xdm:identityMap` dans le [dictionnaire des champs XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. L’attribut XDM [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) indique les segments dont un profil est membre. Pour connaître les trois valeurs différentes du champ `status`, lisez la documentation sur le [groupe de champs de schéma Détails de l’adhésion au segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Présentation {#overview}

Utilisez le contenu de cette page avec le reste des options de configuration [pour les destinations partenaires](./configuration-options.md). Cette page traite du format de message des données exportées de Adobe Experience Platform vers des destinations, tandis que l’autre page traite des détails relatifs à la connexion et à l’authentification à votre destination.

Adobe Experience Platform exporte des données vers un nombre important de destinations, dans divers formats de données. Voici quelques exemples de types de destinations : plateformes publicitaires (Google), réseaux sociaux (Facebook), emplacements de stockage dans le cloud (Amazon S3, Azure Event Hubs).

Experience Platform peut ajuster le format du message exporté pour qu’il corresponde au format attendu de votre côté. Pour comprendre cette personnalisation, les concepts suivants sont importants :
* Le schéma XDM source (1) et cible (2) dans Adobe Experience Platform
* le format du message du côté partenaire (3), et
* Couche de transformation entre les deux, que vous pouvez définir en créant un [modèle de transformation des messages](./message-format.md#using-templating).

![Schéma vers transformation JSON](./assets/transformations-3-steps.png)

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable.

Les utilisateurs qui souhaitent activer des données vers votre destination doivent mapper les champs qu’ils utilisent pour leurs jeux de données dans Experience Platform à un schéma qui se traduit par le format attendu de votre destination. Adobe crée un groupe de champs personnalisé que votre entreprise doit ajouter au schéma cible. Les champs du groupe de champs dépendent des champs d’attribut de profil que vous pouvez recevoir.

**Schéma XDM source (1)** : Cela fait référence au schéma qu’un client utilise dans Experience Platform. Dans Experience Platform, à l’[étape de mappage](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) du workflow d’activation de destination, les clients mappent les champs de leur schéma source au schéma cible de votre destination (2).

**Schéma XDM cible (2)** : En fonction du schéma standard JSON (3) que vous partagez avec Adobe, l’équipe en Adobe crée un schéma personnalisé pour votre destination. Notez que dans une [future phase du projet](./overview.md#phased-approach), vous pourrez créer le schéma personnalisé pour votre destination vous-même.

**Schéma standard JSON de vos attributs de profil de destination (3)**: Partagez avec nous un  [schéma JSON ](https://json-schema.org/learn/miscellaneous-examples.html) de tous les attributs de profil pris en charge par votre plateforme et de leurs types (par exemple : objet, chaîne, tableau). Les champs d’exemple que votre destination peut prendre en charge peuvent être `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`, etc.

En fonction des transformations de schéma décrites ci-dessus, voici comment la structure d’un message change entre le schéma XDM source et l’exemple de schéma du côté partenaire :

![Exemple de message de transformations](./assets/transformations-with-examples.png)

<br> 


## Prise en main - transformation de trois attributs de base {#getting-started}

Pour démontrer le processus de transformation, l’exemple ci-dessous utilise trois attributs de profil courants dans Adobe Experience Platform : **prénom**, **nom** et **adresse électronique**.

>[!NOTE]
>
>Le client mappe les attributs du schéma XDM source au schéma XDM du partenaire dans l’interface utilisateur de Adobe Experience Platform, à l’étape **Mapping** du [workflow d’activation de destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping).

Supposons que votre plateforme puisse recevoir un format de message du type :

```curl
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

## Utilisation d’une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments {#using-templating}

Adobe utilise un langage de modèle similaire à [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) pour transformer les champs du schéma XDM en un format pris en charge par votre destination.

Cette section fournit plusieurs exemples de la manière dont ces transformations sont effectuées, du schéma XDM d’entrée au modèle, et de la sortie dans des formats de payload acceptés par votre destination. Les exemples ci-dessous sont triés par complexité croissante, comme suit :

1. Exemples de transformation simples. Découvrez comment le modèle fonctionne avec des transformations simples pour les attributs de profil [](./message-format.md#attributes), [Appartenance au segment](./message-format.md#segment-membership) et les champs [Identité](./message-format.md#identities).
2. Exemples de modèles plus complexes combinant les champs ci-dessus : [Créez un modèle qui envoie des segments et des identités](./message-format.md#segments-and-identities) et [Créez un modèle qui envoie des segments, des identités et des attributs de profil](./message-format.md#segments-identities-attributes).
3. Exploration approfondie, montrant deux exemples de modèles de partenaires de l’industrie.

### Attributs de profil {#attributes}

Pour transformer les attributs de profil exportés vers votre destination, reportez-vous aux exemples de code et JSON ci-dessous.


>[!IMPORTANT]
>
>Pour obtenir la liste de tous les attributs de profil disponibles dans Adobe Experience Platform, consultez le [dictionnaire de champs XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).



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
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles `""` avant d’insérer le modèle dans la [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, voir le chapitre 9 de la [norme JSON](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

### abonnement au segment {#segment-membership}

L’attribut XDM [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) indique les segments dont un profil est membre.
Pour connaître les trois valeurs différentes du champ `status`, lisez la documentation sur le [groupe de champs de schéma Détails de l’adhésion au segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
        "status": "existing"
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
        "status": "existing"
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
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles `""` avant d’insérer le modèle dans la [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, voir le chapitre 9 de la [norme JSON](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

Pour plus d’informations sur les identités dans Experience Platform, consultez la [présentation de l’espace de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr).

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
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles `""` avant d’insérer le modèle dans la [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, voir le chapitre 9 de la [norme JSON](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
              "status": "existing"
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
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles `""` avant d’insérer le modèle dans la [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, voir le chapitre 9 de la [norme JSON](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

La `json` ci-dessous représente les données exportées depuis Adobe Experience Platform.

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
              "status": "existing"
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
>Pour tous les modèles que vous utilisez, vous devez ajouter une séquence d’échappement aux caractères interdits, tels que les guillemets doubles `""` avant d’insérer le modèle dans la [configuration du serveur de destination](./server-and-template-configuration.md#template-specs). Pour plus d’informations sur l’échappement de guillemets doubles, voir le chapitre 9 de la [norme JSON](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

La `json` ci-dessous représente les données exportées depuis Adobe Experience Platform.

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

### Référence : Contexte et fonctions utilisés dans les modèles de transformation

Le contexte fourni au modèle contient `input` (les profils/données exportés dans cet appel) et `destination` (les données sur la destination vers laquelle l’Adobe envoie des données, valides pour tous les profils).

Le tableau ci-dessous fournit des descriptions des fonctions dans les exemples ci-dessus.

| Fonction | Description |
|---------|----------|
| `input.profile` | Le profil, représenté sous la forme [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Suit le schéma XDM du partenaire mentionné plus haut sur cette page. |
| `destination.segmentAliases` | Mappage des identifiants de segment dans l’espace de noms Adobe Experience Platform aux alias de segment dans le système du partenaire. |
| `destination.segmentNames` | Mappage des noms de segment dans l’espace de noms Adobe Experience Platform aux noms de segment dans le système du partenaire. |
| `addedSegments(listOfSegments)` | Renvoie uniquement les segments dont l’état est `realized` ou `existing`. |
| `removedSegments(listOfSegments)` | Renvoie uniquement les segments dont l’état est `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
