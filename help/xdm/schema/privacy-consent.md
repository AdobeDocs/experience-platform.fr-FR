---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: Type de données Contenus et Préférences
description: Le type de données Préférences de confidentialité/marketing (Consentement) est destiné à prendre en charge la collecte des autorisations et préférences des clients générées par les plateformes de gestion du consentement (CMP) et d’autres sources issues de vos opérations de données.
topic: guide
translation-type: tm+mt
source-git-commit: 1a4dd167ecd4f4f61ffe26af786b355e4561b30d
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 1%

---


# [!DNL Consents & Preferences] présentation du type de données

Le type de [!DNL Privacy/Marketing Preferences (Consent)] données (ci-après dénommé &quot;[!DNL Consents & Preferences] type de données&quot;) est un type de données [!DNL Experience Data Model] (XDM) destiné à prendre en charge la collecte des autorisations et préférences des clients générées par les plates-formes de gestion du consentement (CMP) et d’autres sources provenant de vos opérations de données.

Ce document couvre la structure et l&#39;utilisation prévue des champs fournis par le type de [!DNL Consents & Preferences] données.

## Conditions préalables  {#prerequisites}

Ce document nécessite une compréhension pratique de XDM et de l&#39;utilisation des schémas dans [!DNL Experience Platform]. Veuillez consulter la documentation suivante avant de continuer :

* [Présentation du système XDM](http://www.adobe.com/go/xdm-home-en)
* [Principes de base de la composition des schémas](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Structure du type de données {#structure}

>[!IMPORTANT]
>
>Le type de [!DNL Consents & Preferences] données est conçu pour couvrir une gamme de cas d&#39;utilisation du consentement et de la gestion des préférences. En conséquence, ce document décrit l&#39;utilisation des champs du type de données en termes généraux et ne fait que suggérer comment interpréter l&#39;utilisation de ces champs. Consultez votre équipe juridique de protection des renseignements personnels pour aligner la structure du type de données sur la façon dont votre organisation interprète et présente à vos clients ces choix de consentement et de préférence.

Le type de [!DNL Consents & Preferences] données fournit plusieurs champs utilisés pour capturer les informations de **consentement** et de **préférence** .

Un consentement est une option qui permet à un client de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, en ce sens que certaines juridictions exigent l&#39;obtention d&#39;une autorisation avant que les données puissent être utilisées d&#39;une manière particulière, ou exigent que le client ait la possibilité d&#39;arrêter cette utilisation (opt-out) si le consentement affirmatif n&#39;est pas requis.

Une préférence est une option qui permet au client de spécifier comment gérer différents aspects de son expérience avec une marque. Elles se situent dans deux catégories :

* **Préférences** de personnalisation : Préférences concernant la manière dont la marque doit personnaliser les expériences fournies à un client.
* **Préférences** marketing : Préférences concernant la possibilité pour une marque de contacter un client par le biais de différents canaux.

Le fichier JSON suivant présente un exemple du type de données que le type de [!DNL Consents & Preferences] données peut traiter. Les sections qui suivent fournissent des informations sur l&#39;utilisation spécifique de chacun de ces champs.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:any": {
        "xdm:val": "y",
      },
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>L&#39;exemple ci-dessus est destiné à illustrer la structure des données envoyées à [!DNL Platform] l&#39;aide du type de [!DNL Consents & Preferences] données, afin de donner un contexte au reste de ce document qui explique les principaux champs fournis par le type de données. Le schéma complet de la structure du type de données se trouve dans l&#39; [appendice](#full-schema) à des fins de référence.

## xdm:consentements {#choices}

`xdm:consents` contient plusieurs champs qui décrivent les consentements et préférences d’un client. Ces champs sont décrits plus en détail dans les sous-sections ci-dessous.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:any": {
      "xdm:val": "y",
    },
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:collection

`xdm:collect` représente le consentement du client pour la collecte de ses données.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `xdm:val` | Le choix de consentement fourni par le client pour ce cas d’utilisation. Consultez l&#39; [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### xdm:adID

`xdm:adID` représente le consentement du client quant à savoir si un identifiant publicitaire (IDFA ou GAID) peut être utilisé pour lier le client à l’ensemble des applications sur ce périphérique.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `xdm:val` | Le choix de consentement fourni par le client pour ce cas d’utilisation. Consultez l&#39; [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### xdm:share

`xdm:share` représente le consentement du client pour savoir si ses données peuvent être partagées avec (ou vendues à) des tiers ou des tiers.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `xdm:val` | Le choix de consentement fourni par le client pour ce cas d’utilisation. Consultez l&#39; [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### xdm:personnaliser {#personalize}

`xdm:personalize` capture les préférences des clients quant aux manières dont leurs données peuvent être utilisées pour la personnalisation. Les clients peuvent opt-out de cas d’utilisation spécifiques de la personnalisation ou opt-out de la personnalisation entièrement.

>[!IMPORTANT]
>
>`xdm:personalize` ne couvre pas les cas d’utilisation marketing. Par exemple, si un client choisit de ne pas personnaliser ses canaux, il ne doit pas cesser de recevoir des communications par l’intermédiaire de ces canaux. Au contraire, les messages qu&#39;ils reçoivent devraient être génériques et ne pas être basés sur leur profil.
>
>Dans le même exemple, si un client choisit de ne pas participer au marketing direct pour tous les canaux (par `xdm:marketing`, comme expliqué dans la section [](#marketing)suivante), il ne devrait pas recevoir de messages, même si la personnalisation est autorisée.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| Propriété | Description |
| --- | --- |
| `xdm:content` | Représente les préférences du client pour le contenu personnalisé de votre site Web ou de votre application. |
| `xdm:val` | La préférence de personnalisation fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n&#39;a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle la personnalisation doit se faire. Consultez l&#39; [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

### xdm:marketing {#marketing}

`xdm:marketing` capture les préférences des clients concernant les objectifs marketing auxquels leurs données peuvent être utilisées. Les clients peuvent opt-out de cas d’utilisation marketing spécifiques ou opt-out de marketing direct entièrement.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| Propriété | Description |
| --- | --- |
| `xdm:preferred` | Indique le canal préféré du client pour la réception des communications. Consultez l’ [annexe](#preferred-values) pour connaître les valeurs acceptées. |
| `xdm:any` | Représente les préférences du client pour le marketing direct dans son ensemble. La préférence de consentement fournie dans ce champ est considérée comme la préférence &quot;par défaut&quot; pour tout canal de marketing, sauf si elle est remplacée par d’autres sous-champs fournis sous `xdm:marketing`. Si vous prévoyez d’utiliser des options de consentement plus granulaires, il est recommandé d’exclure ce champ.<br><br>Si la valeur est définie sur `n`, tous les paramètres de personnalisation plus spécifiques doivent être ignorés. Si la valeur est définie sur `y`, toutes les options de personnalisation affinées doivent également être traitées comme `y`, sauf si elles sont explicitement définies sur `n`. Si la valeur n’est pas définie, les valeurs de chaque option de personnalisation doivent être respectées comme indiqué. |
| `xdm:email` | Indique si le client accepte de recevoir des messages électroniques. |
| `xdm:push` | Indique si le client autorise la réception de notifications Push. |
| `xdm:sms` | Indique si le client accepte de recevoir des messages texte. |
| `xdm:val` | La préférence fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n&#39;a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle le cas d&#39;utilisation du marketing doit se baser. Consultez l&#39; [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:time` | Horodatage ISO 8601 indiquant le moment où la préférence marketing a changé, le cas échéant. Notez que si l’horodatage d’une préférence individuelle est identique à celui fourni sous `xdm:metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `xdm:reason` | Lorsqu’un client choisit de ne pas participer à un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle il s’est désabonné. |

### xdm:idSpecific

`xdm:idSpecific` peut être utilisé lorsqu’un consentement ou une préférence particulier ne s’applique pas universellement à un client, mais est limité à un seul appareil ou à un seul ID. Par exemple, un client peut opt-out recevoir des courriers électroniques vers une adresse, tout en autorisant potentiellement les courriers électroniques vers une autre.

>[!IMPORTANT]
>
>Les consentements et les préférences au niveau du canal (c&#39;est-à-dire ceux qui sont fournis `xdm:consents` en dehors de `xdm:idSpecific`) s&#39;appliquent aux identifiants dans ce canal. Par conséquent, tous les consentements et préférences au niveau du canal ont un effet direct sur le respect de paramètres équivalents d’ID ou spécifiques au périphérique :
>
>* Si le client s’est désabonné au niveau du canal, les consentements ou préférences équivalents dans `xdm:idSpecific` sont ignorés.
>* Si le consentement ou la préférence au niveau du canal n&#39;est pas défini, ou si le client a opté pour, les consentements ou préférences équivalents dans `xdm:idSpecific` sont respectés.


Chaque clé de l&#39; `xdm:idSpecific` objet représente un espace de nommage d&#39;identité spécifique reconnu par le service d&#39;identité Adobe Experience Platform. Bien que vous puissiez définir vos propres espaces de nommage personnalisés pour classer les différents identifiants, il est recommandé d&#39;utiliser l&#39;un des espaces de nommage standard fournis par Identity Service pour réduire la taille des enregistrements pour le Profil client en temps réel. Pour plus d&#39;informations sur les espaces de nommage d&#39;identité, consultez la présentation [de l&#39;espace de nommage](../../identity-service/namespaces.md) d&#39;identité dans la documentation Identity Service.

Les clés de chaque objet d&#39;espace de nommage représentent les valeurs d&#39;identité uniques pour lesquelles le client a défini des préférences. Chaque valeur d’identité peut contenir un ensemble complet de consentements et de préférences, formatés de la même manière que `xdm:consents`le cas échéant.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:metadata

`xdm:metadata` capture les métadonnées générales sur les consentements et préférences du client chaque fois qu’il a été mis à jour pour la dernière fois.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| Propriété | Description |
| --- | --- |
| `xdm:time` | Horodatage de la dernière mise à jour du consentement et des préférences du client. Ce champ peut être utilisé au lieu d’appliquer des horodatages à des préférences individuelles afin de réduire la charge et la complexité. La définition d’une `xdm:time` valeur sous une préférence individuelle remplace l’ `xdm:metadata` horodatage de cette préférence particulière. |

## Invitation de données à l’aide du type de données {#ingest}

Pour utiliser le type de [!DNL Consents & Preferences] données pour importer les données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce type de données.

Consultez le didacticiel sur la [création d’un schéma dans l’interface utilisateur](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment affecter des types de données aux champs. Une fois que vous avez créé un schéma contenant un champ avec le type de [!DNL Consents & Preferences] données, reportez-vous à la section relative à la [création d&#39;un jeu](../../catalog/datasets/user-guide.md#create) de données dans le guide de l&#39;utilisateur du jeu de données, en suivant les étapes de création d&#39;un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-time Customer Profile], vous devez créer un schéma [!DNL Profile]activé basé sur la [!DNL XDM Individual Profile] [!DNL Consents & Preferences] classe contenant le type de données. Le jeu de données que vous créez en fonction de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux didacticiels ci-dessus pour connaître les étapes spécifiques liées aux [!DNL Real-time Customer Profile] exigences des schémas et des jeux de données.
>
>En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour classer par priorité les ensembles de données qui contiennent les dernières données de consentement et de préférence, afin que les profils clients soient mis à jour correctement. Pour plus d’informations, voir l’aperçu des stratégies [de](../../rtcdp/profile/merge-policies.md) fusion.

## Traitement des modifications du consentement et des préférences

Lorsqu’un client modifie son consentement ou ses préférences sur votre site Web, ces modifications doivent être collectées et appliquées immédiatement à l’aide du SDK [Web](../../edge/consent/supporting-consent.md)Adobe Experience Platform. Si un client choisit de ne pas participer à la collecte de données, toutes les collectes de données doivent cesser immédiatement. Si un client choisit de ne pas personnaliser, aucune personnalisation ne doit apparaître sur la page suivante qu’il visite.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires sur le type de [!DNL Consents & Preferences] données.

### Valeurs acceptées pour xdm:val {#choice-values}

Le tableau suivant présente les valeurs acceptées pour `xdm:val`:

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a opté pour le consentement ou la préférence. En d&#39;autres termes, ils **consentent** à l&#39;utilisation de leurs données comme indiqué par le consentement ou la préférence en question. |
| `n` | Non | Le client a choisi de ne pas donner son consentement ou sa préférence. En d&#39;autres termes, ils **ne consentent pas** à l&#39;utilisation de leurs données comme indiqué par le consentement ou la préférence en question. |
| `p` | Vérification en attente | Le système n&#39;a pas encore reçu de valeur de consentement ou de préférence finale. Il s&#39;agit le plus souvent d&#39;un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des courriers électroniques, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un courrier électronique pour vérifier qu’il a fourni l’adresse électronique correcte, auquel moment le consentement est mis à jour `y`.<br><br>Si ce consentement ou cette préférence n&#39;utilise pas un processus de vérification à deux étapes, le `p` choix peut être utilisé pour indiquer que le client n&#39;a pas encore répondu à l&#39;invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` la première page d’un site Web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui n&#39;exigent pas de consentement explicite, vous pouvez également l&#39;utiliser pour indiquer que le client n&#39;a pas explicitement choisi de se retirer (en d&#39;autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations relatives au consentement ou aux préférences du client sont inconnues. |
| `LI` | Intérêt légitime | L&#39;intérêt commercial légitime de recueillir et de traiter ces données à des fins déterminées l&#39;emporte sur le préjudice qu&#39;elles peuvent causer à la personne. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec la personne. |
| `CP` | Respect d&#39;une obligation légale | La collecte de données à des fins déterminées est nécessaire pour satisfaire aux obligations légales de l&#39;entreprise. |
| `VI` | Intérêts vitaux du particulier | La collecte de données à des fins déterminées est nécessaire pour protéger les intérêts vitaux de l&#39;individu. |
| `PI` | Intérêt public | La collecte de données à des fins déterminées est nécessaire pour réaliser une tâche dans l&#39;intérêt public ou dans l&#39;exercice de l&#39;autorité officielle. |

### Valeurs acceptées pour xdm:priority {#preferred-values}

Le tableau suivant présente les valeurs acceptées pour `xdm:preferred`:

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

### Schéma complet [!DNL Consents & Preferences] {#full-schema}

Pour vue le schéma complet du type de [!DNL Consents & Preferences] données, reportez-vous au référentiel [XDM](https://github.com/adobe/xdm/blob/master/components/datatypes/consentpreferences.schema.json)officiel.