---
solution: Experience Platform
title: Mélange Confidentialité/Personnalisation/Préférences marketing (Contenus)
topic: aperçu
description: Ce document fournit une vue d’ensemble du mixin Confidentialité/Personnalisation/Préférences marketing (Contenus).
translation-type: tm+mt
source-git-commit: 8c5ab298bad69305358ae961ebaf7836a90a0eaa
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 1%

---


# [!UICONTROL Confidentialité/Personnalisation/Préférences marketing (Contenus)] mixin

[!UICONTROL Préférences de confidentialité/personnalisation/marketing (consents)]  (ci-après dénommés  [!DNL Privacy & Consents] mixin) est un mélange standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md), qui est utilisé pour capturer les informations de consentement et de préférence des clients.

>[!NOTE]
>
>Comme ce mixin n&#39;est compatible qu&#39;avec [!DNL XDM Individual Profile], il ne peut pas être utilisé pour les schémas [!DNL XDM ExperienceEvent]. Si vous souhaitez inclure des données de consentement et de préférence dans votre schéma de Événement d’expérience, ajoutez le [[!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] type de données](../../data-types/consents.md) au schéma en utilisant plutôt un [mixin personnalisé](../../ui/resources/mixins.md#create).

## Structure mixte {#structure}

>[!IMPORTANT]
>
>Le mixin [!DNL Consents & Preferences] est conçu pour couvrir une gamme de cas d&#39;utilisation du consentement et de la gestion des préférences. Par conséquent, ce document décrit l&#39;utilisation des champs du mixin en termes généraux et ne fait que des suggestions sur la façon d&#39;interpréter l&#39;utilisation de ces champs. Veuillez consulter votre équipe juridique en matière de protection des renseignements personnels afin d&#39;aligner la structure du mixin sur la façon dont votre organisation interprète et présente à vos clients ces choix de consentement et de préférence.

Le mixin [!DNL Consents & Preferences] fournit plusieurs champs utilisés pour capturer les informations **consentement** et **préférence**.

Un consentement est une option qui permet à un client de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, en ce sens que certaines juridictions exigent l&#39;obtention d&#39;une autorisation avant que les données puissent être utilisées d&#39;une manière particulière, ou exigent que le client ait la possibilité d&#39;arrêter cette utilisation (opt-out) si le consentement affirmatif n&#39;est pas requis.

Une préférence est une option qui permet au client de spécifier comment gérer différents aspects de son expérience avec une marque. Elles se situent dans deux catégories :

* **Préférences** de personnalisation : Préférences concernant la manière dont la marque doit personnaliser les expériences fournies à un client.
* **Préférences** marketing : Préférences concernant la possibilité pour une marque de contacter un client par le biais de différents canaux.

La capture d’écran suivante montre comment la structure du mixin est représentée dans l’interface utilisateur de la plate-forme :

![](../../images/mixins/consent.png)

>[!TIP]
>
>Consultez le guide sur [l&#39;exploration des ressources XDM](../../ui/explore.md) pour savoir comment rechercher une ressource XDM et examiner sa structure dans l&#39;interface utilisateur de la plate-forme.

Le fichier JSON suivant présente un exemple du type de données que le mixin [!DNL Consents & Preferences] peut traiter. Les sections qui suivent fournissent des informations sur l&#39;utilisation spécifique de chacun de ces champs.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Vous pouvez générer des données JSON d’exemple pour n’importe quel schéma XDM que vous définissez dans l’Experience Platform afin de mieux visualiser comment vos données de préférences et de consentement des clients doivent être mises en correspondance. Pour plus d’informations, consultez la documentation suivante :
>
>* [Générer des données d’exemple dans l’interface utilisateur](../../ui/sample.md)
>* [Générer des données d’exemple dans l’API](../../api/sample-data.md)


## Cas d&#39;utilisation sur le terrain

Les cas d&#39;utilisation prévus pour chacun de ces champs sont présentés dans les sections ci-dessous.

### `collect`

`collect` représente le consentement du client pour la collecte de ses données.

```json
"collect" : {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Le choix de consentement fourni par le client pour ce cas d’utilisation. Voir l&#39;[annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### `share`

`share` représente le consentement du client pour savoir si ses données peuvent être partagées avec (ou vendues à) des tiers ou des tiers.

```json
"share" : {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Le choix de consentement fourni par le client pour ce cas d’utilisation. Voir l&#39;[annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### `personalize` {#personalize}

`personalize` capture les préférences des clients quant aux manières dont leurs données peuvent être utilisées pour la personnalisation. Les clients peuvent opt-out de cas d’utilisation spécifiques de la personnalisation ou opt-out de la personnalisation entièrement.

>[!IMPORTANT]
>
>`personalize` ne couvre pas les cas d’utilisation marketing. Par exemple, si un client choisit de ne pas personnaliser ses canaux, il ne doit pas cesser de recevoir des communications par l’intermédiaire de ces canaux. Au contraire, les messages qu&#39;ils reçoivent devraient être génériques et ne pas être basés sur leur profil.
>
>Dans le même exemple, si un client choisit de ne pas participer au marketing direct pour tous les canaux (par `marketing`, comme expliqué dans la section [suivante](#marketing)), il ne doit recevoir aucun message, même si la personnalisation est autorisée.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propriété | Description |
| --- | --- |
| `content` | Représente les préférences du client pour le contenu personnalisé de votre site Web ou de votre application. |
| `val` | La préférence de personnalisation fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n&#39;a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle la personnalisation doit se faire. Voir l&#39;[annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### `marketing` {#marketing}

`marketing` capture les préférences des clients concernant les objectifs marketing auxquels leurs données peuvent être utilisées. Les clients peuvent opt-out de cas d’utilisation marketing spécifiques ou opt-out de marketing direct entièrement.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Propriété | Description |
| --- | --- |
| `preferred` | Indique le canal préféré du client pour la réception des communications. Voir l&#39;[annexe](#preferred-values) pour connaître les valeurs acceptées. |
| `any` | Représente les préférences du client pour le marketing direct dans son ensemble. La préférence de consentement fournie dans ce champ est considérée comme la préférence &quot;par défaut&quot; pour tout canal marketing, sauf si elle est remplacée par des sous-champs supplémentaires fournis sous `marketing`. Si vous prévoyez d’utiliser des options de consentement plus granulaires, il est recommandé d’exclure ce champ.<br><br>Si la valeur est définie sur  `n`, tous les paramètres de personnalisation plus spécifiques doivent être ignorés. Si la valeur est définie sur `y`, toutes les options de personnalisation affinées doivent également être traitées comme `y`, sauf si elle est explicitement définie sur `n`. Si la valeur n’est pas définie, les valeurs de chaque option de personnalisation doivent être respectées comme indiqué. |
| `email` | Indique si le client accepte de recevoir des messages électroniques. Le client peut également fournir des préférences pour des abonnements individuels dans ce canal. Pour plus d&#39;informations, consultez la section [abonnements](#subscriptions) ci-dessous. |
| `push` | Indique si le client autorise la réception de notifications Push. Le client peut également fournir des préférences pour des abonnements individuels dans ce canal. Pour plus d&#39;informations, consultez la section [abonnements](#subscriptions) ci-dessous. |
| `sms` | Indique si le client accepte de recevoir des messages texte. Le client peut également fournir des préférences pour des abonnements individuels dans ce canal. Pour plus d&#39;informations, consultez la section [abonnements](#subscriptions) ci-dessous. |
| `val` | La préférence fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n&#39;a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle le cas d&#39;utilisation du marketing doit se baser. Voir l&#39;[annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |
| `time` | Horodatage ISO 8601 indiquant le moment où la préférence marketing a changé, le cas échéant. Notez que si l&#39;horodatage d&#39;une préférence individuelle est identique à celui fourni sous `metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `reason` | Lorsqu’un client choisit de ne pas participer à un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle il s’est désabonné. |

#### `subscriptions` {#subscriptions}

Les propriétés `email`, `push` et `sms` de l&#39;objet `marketing` peuvent représenter les abonnements du client pour ces canaux individuels. Pour ce faire, vous ajoutez une propriété `subscriptions` au canal marketing en question.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `type` | Type d’abonnement. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne au moins 15 caractères. |
| `subscribers` | Champ facultatif de type de mappage qui représente un ensemble d’identifiants (tels que des adresses électroniques ou des numéros de téléphone) qui se sont abonnés à un abonnement particulier. Chaque clé de cet objet représente l’identifiant en question et contient deux sous-propriétés : <ul><li>`time`: Un horodatage ISO 8601 indiquant le moment où l&#39;identité s&#39;est abonnée, le cas échéant.</li><li>`source`: Source d’où provient l’abonné. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne au moins 15 caractères.</li></ul> |


### `metadata`

`metadata` capture les métadonnées générales sur les consentements et préférences du client chaque fois qu’il a été mis à jour pour la dernière fois.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriété | Description |
| --- | --- |
| `time` | Un horodatage ISO 8601 pour la dernière fois que l&#39;un des consentements et préférences du client a été mis à jour. Ce champ peut être utilisé au lieu d’appliquer des horodatages à des préférences individuelles afin de réduire la charge et la complexité. La valeur `time` sous une préférence individuelle remplace l&#39;horodatage `metadata` de cette préférence particulière. |

### `idSpecific`

`idSpecific` peut être utilisé lorsqu’un consentement ou une préférence particulier ne s’applique pas universellement à un client, mais est limité à un seul appareil ou à un seul ID. Par exemple, un client peut opt-out recevoir des courriers électroniques vers une adresse, tout en autorisant potentiellement les courriers électroniques vers une autre.

>[!IMPORTANT]
>
>Les consentements et préférences au niveau du canal (c&#39;est-à-dire ceux fournis en vertu de `consents` en dehors de `idSpecific`) s&#39;appliquent aux identifiants dans ce canal. Par conséquent, tous les consentements et préférences au niveau du canal ont un effet direct sur le respect de paramètres équivalents d’ID ou spécifiques au périphérique :
>
>* Si le client s&#39;est désabonné au niveau du canal, tous les consentements ou préférences équivalents dans `idSpecific` sont ignorés.
>* Si le consentement ou la préférence au niveau du canal n&#39;est pas défini, ou si le client a opté pour, les consentements ou préférences équivalents dans `idSpecific` sont respectés.


Chaque clé de l&#39;objet `idSpecific` représente un espace de nommage d&#39;identité spécifique reconnu par Adobe Experience Platform Identity Service. Bien que vous puissiez définir vos propres espaces de nommage personnalisés pour classer les différents identifiants, il est recommandé d&#39;utiliser l&#39;un des espaces de nommage standard fournis par Identity Service pour réduire la taille des enregistrements pour le Profil client en temps réel. Pour plus d&#39;informations sur les espaces de nommage d&#39;identité, consultez l&#39;[aperçu de l&#39;espace de nommage d&#39;identité](../../../identity-service/namespaces.md) dans la documentation Identity Service.

Les clés de chaque objet d&#39;espace de nommage représentent les valeurs d&#39;identité uniques pour lesquelles le client a défini des préférences. Chaque valeur d&#39;identité peut contenir un ensemble complet de consentements et de préférences, formaté de la même manière que `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Dans les objets `marketing` fournis dans la section `idSpecific`, les champs `any` et `preferred` ne sont pas pris en charge. Ces champs ne peuvent être configurés qu’au niveau de l’utilisateur. En outre, les préférences marketing `idSpecific` pour `email`, `sms` et `push` ne prennent pas en charge les champs `subscriptions`.

Il existe également un consentement qui ne peut être fourni que dans la section `idSpecific` : `adID`. Ce champ est couvert dans la sous-section ci-dessous.

#### `adID`

Le consentement `adID` représente le consentement du client quant à savoir si un identifiant publicitaire (IDFA ou GAID) peut être utilisé pour relier le client entre les applications sur ce périphérique. Cette valeur ne peut être configurée que sous l&#39;espace de nommage d&#39;identité `ECID` dans la section `idSpecific` et ne peut pas être définie pour d&#39;autres espaces de nommage ou au niveau de l&#39;utilisateur pour ce mixin.

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Vous ne devez pas définir directement cette valeur, car le kit Adobe Experience Platform Mobile SDK la définit automatiquement, le cas échéant.

## Incorporation de données à l’aide du mixin {#ingest}

Pour utiliser le mixin [!DNL Consents & Preferences] pour ingérer les données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce mixin.

Consultez le didacticiel sur la création d&#39;un schéma dans l&#39;interface utilisateur](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment affecter des mixins à des champs. [ Une fois que vous avez créé un schéma contenant un champ avec le mixin [!DNL Consents & Preferences], reportez-vous à la section [création d&#39;un jeu de données](../../../catalog/datasets/user-guide.md#create) dans le guide de l&#39;utilisateur du jeu de données, en suivant les étapes de création d&#39;un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-time Customer Profile], vous devez créer un schéma compatible [!DNL Profile] basé sur la classe [!DNL XDM Individual Profile] contenant le mixin [!DNL Consents & Preferences]. Le jeu de données que vous créez en fonction de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux didacticiels ci-dessus pour connaître les étapes spécifiques liées aux [!DNL Real-time Customer Profile] exigences relatives aux schémas et aux jeux de données.
>
>En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour classer par priorité les ensembles de données qui contiennent les dernières données de consentement et de préférence, afin que les profils clients soient mis à jour correctement. Pour plus d&#39;informations, consultez l&#39;aperçu des [stratégies de fusion](../../../rtcdp/profile/merge-policies.md).

## Traitement des modifications du consentement et des préférences

Lorsqu’un client modifie son consentement ou ses préférences sur votre site Web, ces modifications doivent être collectées et appliquées immédiatement à l’aide du [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Si un client choisit de ne pas participer à la collecte de données, toutes les collectes de données doivent cesser immédiatement. Si un client choisit de ne pas personnaliser, aucune personnalisation ne doit apparaître sur la page suivante qu’il visite.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires concernant le mixin [!DNL Consents & Preferences].

### Valeurs acceptées pour `val` {#choice-values}

Le tableau suivant présente les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a opté pour le consentement ou la préférence. En d&#39;autres termes, ils ont &lt; a0/>donné **leur consentement à l&#39;utilisation de leurs données, tel qu&#39;indiqué par le consentement ou la préférence en question.** |
| `n` | Non | Le client a choisi de ne pas donner son consentement ou sa préférence. En d&#39;autres termes, ils **n&#39;acceptent pas l&#39;utilisation de leurs données comme l&#39;indique le consentement ou la préférence en question.** |
| `p` | Vérification en attente | Le système n&#39;a pas encore reçu de valeur de consentement ou de préférence finale. Il s&#39;agit le plus souvent d&#39;un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des courriers électroniques, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un courrier électronique pour vérifier qu’il a fourni l’adresse électronique correcte, auquel moment le consentement est mis à jour sur `y`.<br><br>Si ce consentement ou cette préférence n&#39;utilise pas un processus de vérification à deux étapes, le  `p` choix peut être utilisé pour indiquer que le client n&#39;a pas encore répondu à l&#39;invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur `p` sur la première page d’un site Web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui n&#39;exigent pas de consentement explicite, vous pouvez également l&#39;utiliser pour indiquer que le client n&#39;a pas explicitement choisi de se retirer (en d&#39;autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations relatives au consentement ou aux préférences du client sont inconnues. |
| `LI` | Intérêt légitime | L&#39;intérêt commercial légitime de recueillir et de traiter ces données à des fins déterminées l&#39;emporte sur le préjudice qu&#39;elles peuvent causer à la personne. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec la personne. |
| `CP` | Respect d&#39;une obligation légale | La collecte de données à des fins déterminées est nécessaire pour satisfaire aux obligations légales de l&#39;entreprise. |
| `VI` | Intérêts vitaux du particulier | La collecte de données à des fins déterminées est nécessaire pour protéger les intérêts vitaux de l&#39;individu. |
| `PI` | Intérêt public | La collecte de données à des fins déterminées est nécessaire pour réaliser une tâche dans l&#39;intérêt public ou dans l&#39;exercice de l&#39;autorité officielle. |

### Valeurs acceptées pour `preferred` {#preferred-values}

Le tableau suivant présente les valeurs acceptées pour `preferred` :

| Valeur | Description |
| --- | --- |
| `email` | Canal Email. |
| `push` | Notifications push. |
| `inApp` | Les messages in-app. |
| `sms` | SMS. |
| `phone` | Interactions d’appel téléphonique. |
| `phyMail` | Courrier physique. |
| `inVehicle` | Messages embarqués. |
| `inHome` | Messages internes. |
| `iot` | Internet des messages d&#39;objets (IoT). |
| `social` | Contenu des médias sociaux. |
| `other` | Canal qui ne correspond pas à une catégorie standard. |
| `none` | Aucun canal préféré. |
| `unknown` | Le canal préféré est inconnu. |

### Schéma [!DNL Consents & Preferences] complet {#full-schema}

Pour vue le schéma complet du mixin [!DNL Consents & Preferences], consultez le [référentiel XDM officiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
