---
solution: Experience Platform
title: Groupe de champs de schéma de contenu et de préférences
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Contenus et Préférences .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '2316'
ht-degree: 2%

---

# [!UICONTROL Consentements et groupe de champs ] Préférences

[!UICONTROL Contient et ]privilégie un groupe de champs standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md), qui est utilisé pour capturer les informations de consentement et de préférence du client.

>[!NOTE]
>
>Ce groupe de champs n’étant compatible qu’avec [!DNL XDM Individual Profile], il ne peut pas être utilisé pour les schémas [!DNL XDM ExperienceEvent]. Si vous souhaitez inclure les données de consentement et de préférence dans votre schéma Événement d’expérience, ajoutez le [[!UICONTROL consentement pour la confidentialité, la personnalisation et les préférences marketing] type de données](../../data-types/consents.md) au schéma à l’aide d’un [groupe de champs personnalisé](../../ui/resources/field-groups.md#create) à la place.

## Structure du groupe de champs {#structure}

>[!IMPORTANT]
>
>Le groupe de champs [!UICONTROL Conférences et Préférences] est conçu pour couvrir un large éventail de cas d’utilisation de la gestion du consentement et des préférences. Par conséquent, ce document décrit l’utilisation des champs du groupe de champs en termes généraux et ne fait que des suggestions sur la manière dont vous devez interpréter l’utilisation de ces champs. Veuillez consulter votre équipe juridique de la confidentialité pour aligner la structure du groupe de champs avec la manière dont votre organisation interprète et présente à vos clients ces choix de consentement et de préférence.

Le groupe de champs [!UICONTROL Contenus et Préférences] fournit plusieurs champs utilisés pour capturer les informations **consentement** et **préférence**.

Un consentement est une option qui permet à un client de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, dans la mesure où certaines juridictions exigent l’obtention d’une autorisation avant que les données ne puissent être utilisées d’une manière particulière, ou exigent que le client ait la possibilité d’arrêter cette utilisation (opt-out) si un consentement positif n’est pas requis.

Une préférence est une option qui permet au client de spécifier comment gérer différents aspects de son expérience avec une marque. Elles se divisent en deux catégories :

* **Préférences** de personnalisation : Préférences concernant la manière dont la marque doit personnaliser les expériences diffusées à un client.
* **Préférences marketing** : Préférences concernant le fait qu’une marque soit autorisée à contacter un client par le biais de divers canaux.

La capture d’écran suivante montre comment la structure du groupe de champs est représentée dans l’interface utilisateur de Platform :

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consultez le guide sur l’[exploration des ressources XDM](../../ui/explore.md) vers pour savoir comment rechercher une ressource XDM et examiner sa structure dans l’interface utilisateur de Platform.

Le fichier JSON suivant illustre un exemple du type de données que le groupe de champs [!UICONTROL Contenus et Préférences] peut traiter. Les sections suivantes contiennent des informations sur l’utilisation spécifique de chacun de ces champs.

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
>Vous pouvez générer des exemples de données JSON pour tout schéma XDM que vous définissez dans Experience Platform afin de mieux visualiser la manière dont vos données de consentement et de préférence client doivent être mappées. Pour plus d’informations, consultez la documentation suivante :
>
>* [Génération d’exemples de données dans l’interface utilisateur](../../ui/sample.md)
* [Génération d’exemples de données dans l’API](../../api/sample-data.md)


## Cas d’utilisation des champs

Les cas d’utilisation prévus pour chacun de ces champs sont présentés dans les sections ci-dessous.

### `collect`

`collect` représente le consentement du client pour la collecte de ses données.

```json
"collect" : {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Choix du consentement fourni par le client pour ce cas d’utilisation. Voir l’ [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` représente le consentement du client pour que ses données puissent être partagées avec (ou vendues à) des tiers ou des tiers.

```json
"share" : {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Choix du consentement fourni par le client pour ce cas d’utilisation. Voir l’ [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` capture les préférences des clients concernant les façons dont leurs données peuvent être utilisées pour la personnalisation. Les clients peuvent se désabonner de cas d’utilisation de personnalisation spécifiques ou se désabonner entièrement de la personnalisation.

>[!IMPORTANT]
`personalize` ne couvre pas les cas d’utilisation marketing. Par exemple, si un client choisit de ne pas se personnaliser pour tous les canaux, il ne doit pas cesser de recevoir des communications par le biais de ces canaux. Au contraire, les messages qu&#39;ils reçoivent doivent être génériques et non basés sur leur profil.
Dans le même exemple, si un client choisit de ne pas participer au marketing direct pour tous les canaux (par l’intermédiaire de `marketing`, expliqué dans la [section suivante](#marketing)), ce client ne doit recevoir aucun message, même si la personnalisation est autorisée.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propriété | Description |
| --- | --- |
| `content` | Représente les préférences du client pour le contenu personnalisé de votre site web ou de votre application. |
| `val` | La préférence de personnalisation fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle la personnalisation doit se dérouler. Voir l’ [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

### `marketing` {#marketing}

`marketing` capture les préférences des clients concernant les finalités marketing auxquelles leurs données peuvent être utilisées. Les clients peuvent se désabonner de cas d’utilisation marketing spécifiques ou se désabonner entièrement du marketing direct.

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
| `preferred` | Indique le canal préféré du client pour la réception des communications. Voir l’ [annexe](#preferred-values) pour connaître les valeurs acceptées. |
| `any` | Représente les préférences du client pour le marketing direct dans son ensemble. La préférence de consentement fournie dans ce champ est considérée comme la préférence &quot;par défaut&quot; pour tout canal marketing, sauf si elle est remplacée par des sous-champs supplémentaires fournis sous `marketing`. Si vous envisagez d’utiliser des options de consentement plus granulaires, il est recommandé d’exclure ce champ.<br><br>Si la valeur est définie sur  `n`, tous les paramètres de personnalisation plus spécifiques doivent être ignorés. Si la valeur est définie sur `y`, toutes les options de personnalisation plus affinées doivent également être traitées comme `y`, sauf si elles sont explicitement définies sur `n`. Si la valeur n’est pas définie, les valeurs de chaque option de personnalisation doivent être honorées comme indiqué. |
| `email` | Indique si le client accepte de recevoir des emails. Le client peut également fournir des préférences pour les abonnements individuels dans ce canal. Pour plus d’informations, consultez la section [abonnements](#subscriptions) ci-dessous. |
| `push` | Indique si le client autorise la réception de notifications push. Le client peut également fournir des préférences pour les abonnements individuels dans ce canal. Pour plus d’informations, consultez la section [abonnements](#subscriptions) ci-dessous. |
| `sms` | Indique si le client accepte de recevoir des SMS. Le client peut également fournir des préférences pour les abonnements individuels dans ce canal. Pour plus d’informations, consultez la section [abonnements](#subscriptions) ci-dessous. |
| `val` | La préférence fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle doit se baser le cas d’utilisation marketing. Voir l’ [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |
| `time` | Horodatage ISO 8601 du moment où la préférence marketing a changé, le cas échéant. Notez que si l’horodatage d’une préférence individuelle est identique à celui fourni sous `metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `reason` | Lorsqu’un client s’exclut d’un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle le client s’est désinscrit. |

{style=&quot;table-layout:auto&quot;}

#### `subscriptions` {#subscriptions}

Les propriétés `email`, `push` et `sms` de l’objet `marketing` peuvent représenter les abonnements des clients pour ces canaux individuels. Pour ce faire, ajoutez une propriété `subscriptions` au canal marketing en question.

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
| `type` | Type d’abonnement. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne 15 caractères ou moins. |
| `subscribers` | Champ facultatif de type map qui représente un ensemble d’identifiants (tels que les adresses électroniques ou les numéros de téléphone) abonnés à un abonnement particulier. Chaque clé de cet objet représente l’identifiant en question et contient deux sous-propriétés : <ul><li>`time`: Horodatage ISO 8601 du moment où l’identité s’est abonnée, le cas échéant.</li><li>`source`: Source d’où provient l’abonné. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne 15 caractères ou moins.</li></ul> |

{style=&quot;table-layout:auto&quot;}


### `metadata`

`metadata` capture les métadonnées générales sur les consentements et préférences du client chaque fois qu’ils ont été mis à jour pour la dernière fois.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriété | Description |
| --- | --- |
| `time` | Horodatage ISO 8601 de la dernière mise à jour des consentements et préférences du client. Ce champ peut être utilisé au lieu d’appliquer des horodatages à des préférences individuelles afin de réduire la charge et la complexité. Le fait de fournir une valeur `time` sous une préférence individuelle remplace l’horodatage `metadata` de cette préférence particulière. |

{style=&quot;table-layout:auto&quot;}

### `idSpecific`

`idSpecific` peut être utilisé lorsqu’un consentement ou une préférence spécifique ne s’applique pas universellement à un client, mais est limité à un seul appareil ou à un seul identifiant. Par exemple, un client peut refuser de recevoir des emails à une adresse, tout en autorisant éventuellement l’envoi d’emails à une autre.

>[!IMPORTANT]
Les consentements et préférences au niveau du canal (c’est-à-dire ceux fournis sous `consents` en dehors de `idSpecific`) s’appliquent aux identifiants dans ce canal. Par conséquent, tous les consentements et préférences au niveau du canal influent directement sur le respect des paramètres équivalents d’ID ou spécifiques à l’appareil :
* Si le client s’est désabonné au niveau du canal, tous les consentements ou préférences équivalents dans `idSpecific` sont ignorés.
* Si le consentement ou la préférence au niveau du canal n’est pas définie, ou si le client s’est inscrit, les consentements ou préférences équivalents dans `idSpecific` sont respectés.


Chaque clé de l’objet `idSpecific` représente un espace de noms d’identité spécifique reconnu par le service Adobe Experience Platform Identity. Bien que vous puissiez définir vos propres espaces de noms personnalisés pour classer différents identifiants, il est recommandé d’utiliser l’un des espaces de noms standard fournis par Identity Service pour réduire les tailles de stockage pour Real-time Customer Profile. Pour plus d’informations sur les espaces de noms d’identité, consultez la [présentation des espaces de noms d’identité](../../../identity-service/namespaces.md) dans la documentation Identity Service.

Les clés de chaque objet d’espace de noms représentent les valeurs d’identité uniques pour lesquelles le client a défini des préférences. Chaque valeur d’identité peut contenir un ensemble complet de consentements et de préférences, formaté de la même manière que `consents`.

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

Dans les objets `marketing` fournis dans la section `idSpecific`, les champs `any` et `preferred` ne sont pas pris en charge. Ces champs ne peuvent être configurés qu’au niveau de l’utilisateur. De plus, les `idSpecific` préférences marketing pour `email`, `sms` et `push` ne prennent pas en charge les champs `subscriptions`.

Il existe également un consentement qui ne peut être fourni que dans la section `idSpecific` : `adID`. Ce champ est traité dans la sous-section ci-dessous.

#### `adID`

Le `adID` consentement représente le consentement du client pour savoir si un ID d’annonceur (IDFA ou GAID) peut être utilisé pour lier le client à travers les applications de cet appareil. Cette valeur ne peut être configurée que sous l’espace de noms d’identité `ECID` dans la section `idSpecific` et ne peut pas être définie pour d’autres espaces de noms ou au niveau de l’utilisateur pour ce groupe de champs.

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
Vous ne devez pas définir cette valeur directement, car le SDK Adobe Experience Platform Mobile la définit automatiquement le cas échéant.

## Ingestion de données à l’aide du groupe de champs {#ingest}

Pour utiliser le groupe de champs [!UICONTROL Contenus et Préférences] afin d’ingérer les données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce groupe de champs.

Consultez le tutoriel sur la [création d’un schéma dans l’interface utilisateur](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment attribuer des groupes de champs à des champs. Une fois que vous avez créé un schéma contenant un champ avec le groupe de champs [!UICONTROL Contenus et Préférences] , reportez-vous à la section sur la [création d’un jeu de données](../../../catalog/datasets/user-guide.md#create) dans le guide d’utilisation du jeu de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
Si vous souhaitez envoyer des données de consentement à [!DNL Real-time Customer Profile], vous devez créer un schéma compatible [!DNL Profile] basé sur la classe [!DNL XDM Individual Profile] qui contient le groupe de champs [!UICONTROL Contenus et Préférences]. Le jeu de données que vous créez à partir de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux tutoriels ci-dessus pour connaître les étapes spécifiques aux [!DNL Real-time Customer Profile] exigences relatives aux schémas et aux jeux de données.
En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour prioriser le ou les jeux de données qui contiennent les dernières données de consentement et de préférence, afin que les profils client soient correctement mis à jour. Pour plus d’informations, consultez la présentation des [stratégies de fusion](../../../rtcdp/profile/merge-policies.md) .

## Gestion des modifications du consentement et des préférences

Lorsqu’un client modifie ses consentements ou ses préférences sur votre site web, ces modifications doivent être collectées et appliquées immédiatement à l’aide du [SDK Web Adobe Experience Platform](../../../edge/consent/supporting-consent.md). Si un client choisit de ne pas participer à la collecte de données, toute collecte de données doit immédiatement cesser. Si un client s’exclut de la personnalisation, aucune personnalisation ne doit être présente sur la page suivante qu’il consulte.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires concernant le groupe de champs [!UICONTROL Contenus et Préférences] .

### Valeurs acceptées pour `val` {#choice-values}

Le tableau suivant décrit les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a donné son consentement ou sa préférence. En d’autres termes, ils ont le **consentement** pour l’utilisation de leurs données, comme indiqué par le consentement ou la préférence en question. |
| `n` | Non | Le client s’est désinscrit du consentement ou de la préférence. En d’autres termes, ils **ne donnent pas leur consentement à l’utilisation de leurs données comme indiqué par le consentement ou la préférence en question.** |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de consentement ou de préférence finale. Il est le plus souvent utilisé dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des emails, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un email pour vérifier qu’il a fourni l’adresse email correcte, auquel moment le consentement est mis à jour sur `y`.<br><br>Si ce consentement ou cette préférence n’utilise pas un processus de vérification à deux ensembles, alors le  `p` choix peut être utilisé pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui ne requièrent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client n’a pas explicitement exercé son droit d’opposition (en d’autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations de consentement ou de préférence du client sont inconnues. |
| `LI` | L&#39;intérêt légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiées l’emporte sur le préjudice potentiel qu’elles peuvent causer à l’individu. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec l’individu. |
| `CP` | Respect d’une obligation juridique | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations légales de l’entreprise. |
| `VI` | Intérêt vital de l’individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l’individu. |
| `PI` | Intérêt public | La collecte de données aux fins spécifiées est nécessaire pour effectuer une tâche dans l’intérêt public ou dans l’exercice de l’autorité officielle. |

{style=&quot;table-layout:auto&quot;}

### Valeurs acceptées pour `preferred` {#preferred-values}

Le tableau suivant décrit les valeurs acceptées pour `preferred` :

| Valeur | Description |
| --- | --- |
| `email` | Courriel messages. |
| `push` | Notifications push. |
| `inApp` | Les messages in-app. |
| `sms` | SMS. |
| `phone` | Interactions d’appel téléphonique. |
| `phyMail` | Courrier physique. |
| `inVehicle` | Messages dans le véhicule. |
| `inHome` | Messages internes. |
| `iot` | L&#39;Internet des objets (IoT) des messages. |
| `social` | Contenu des médias sociaux. |
| `other` | Un canal qui ne correspond pas à une catégorie standard. |
| `none` | Aucun canal préféré. |
| `unknown` | Le canal préféré est inconnu. |

{style=&quot;table-layout:auto&quot;}

### Schéma [!UICONTROL Conférences et préférences] complet {#full-schema}

Pour afficher le schéma complet du groupe de champs [!UICONTROL Contenus et Préférences], reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
