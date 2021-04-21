---
keywords: Experience Platform ; profil ; profil client en temps réel ; résolution des problèmes ; API ; consentement ; consentement ; préférences ; Préférences ; confidentialité ; OptOuts ; marketingPreferences ; optOutType ; baseOfProcessing ; consentement ; Consent
title: Type de données Contenus et Préférences
description: Le type de données Consentement pour la confidentialité, la personnalisation et les préférences marketing est destiné à prendre en charge la collecte des autorisations et préférences des clients générées par les plates-formes de gestion du consentement (CMP) et d’autres sources issues de vos opérations de données.
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 2%

---

# [!DNL Consents & Preferences] type de données

Le type de données [!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] (ci-après dénommé le &quot;[!DNL Consents & Preferences] type de données&quot;) est un type de données [!DNL Experience Data Model] (XDM) destiné à prendre en charge la collecte des autorisations et préférences des clients générées par les plateformes de gestion du consentement (CMP) et d&#39;autres sources issues de vos opérations de données.

Ce document couvre la structure et l&#39;utilisation prévue des champs fournis par le type de données [!DNL Consents & Preferences].

## Conditions préalables {#prerequisites}

Ce document exige une compréhension pratique de XDM et l&#39;utilisation des schémas dans [!DNL Experience Platform]. Veuillez consulter la documentation suivante avant de continuer :

* [Présentation du système XDM](http://www.adobe.com/go/xdm-home-en)
* [Principes de base de la composition des schémas](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Structure du type de données {#structure}

>[!IMPORTANT]
>
>Le type de données [!DNL Consents & Preferences] est conçu pour couvrir une gamme de cas d&#39;utilisation du consentement et de la gestion des préférences. En conséquence, ce document décrit l&#39;utilisation des champs du type de données en termes généraux et ne fait que suggérer comment interpréter l&#39;utilisation de ces champs. Consultez votre équipe juridique de protection des renseignements personnels pour aligner la structure du type de données sur la façon dont votre organisation interprète et présente à vos clients ces choix de consentement et de préférence.

Le type de données [!DNL Consents & Preferences] fournit plusieurs champs utilisés pour capturer les informations **consentement** et **préférence**.

Un consentement est une option qui permet à un client de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, en ce sens que certaines juridictions exigent l&#39;obtention d&#39;une autorisation avant que les données puissent être utilisées d&#39;une manière particulière, ou exigent que le client ait la possibilité d&#39;arrêter cette utilisation (opt-out) si le consentement affirmatif n&#39;est pas requis.

Une préférence est une option qui permet au client de spécifier comment gérer différents aspects de son expérience avec une marque. Elles se situent dans deux catégories :

* **Préférences** de personnalisation : Préférences concernant la manière dont la marque doit personnaliser les expériences fournies à un client.
* **Préférences** marketing : Préférences concernant la possibilité pour une marque de contacter un client par le biais de différents canaux.

La capture d’écran suivante montre comment la structure du type de données est représentée dans l’interface utilisateur de la plate-forme :

![](../images/data-types/consents.png)

>[!TIP]
>
>Consultez le guide sur [l&#39;exploration des ressources XDM](../ui/explore.md) pour savoir comment rechercher une ressource XDM et examiner sa structure dans l&#39;interface utilisateur de la plate-forme.

Le fichier JSON suivant présente un exemple du type de données que le type de données [!DNL Consents & Preferences] peut traiter. Les sections qui suivent fournissent des informations sur l&#39;utilisation spécifique de chacun de ces champs.

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
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
>* [Générer des données d’exemple dans l’interface utilisateur](../ui/sample.md)
>* [Générer des données d’exemple dans l’API](../api/sample-data.md)


## `consents` {#choices}

`consents` contient plusieurs champs qui décrivent les consentements et préférences d’un client. Ces champs sont décrits plus en détail dans les sous-sections ci-dessous.

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

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

### `adID`

`adID` représente le consentement du client quant à savoir si un identifiant publicitaire (IDFA ou GAID) peut être utilisé pour lier le client à l’ensemble des applications sur ce périphérique.

```json
"adID" : {
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
| `email` | Indique si le client accepte de recevoir des messages électroniques. |
| `push` | Indique si le client autorise la réception de notifications Push. |
| `sms` | Indique si le client accepte de recevoir des messages texte. |
| `val` | La préférence fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n&#39;a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle le cas d&#39;utilisation du marketing doit se baser. Voir l&#39;[annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |
| `time` | Horodatage ISO 8601 indiquant le moment où la préférence marketing a changé, le cas échéant. Notez que si l&#39;horodatage d&#39;une préférence individuelle est identique à celui fourni sous `metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `reason` | Lorsqu’un client choisit de ne pas participer à un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle il s’est désabonné. |

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

## Invitation de données à l’aide du type de données {#ingest}

Pour utiliser le type de données [!DNL Consents & Preferences] pour importer les données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce type de données.

Consultez le didacticiel sur la création d&#39;un schéma dans l&#39;interface utilisateur](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment affecter des types de données à des champs. [ Une fois que vous avez créé un schéma contenant un champ avec le type de données [!DNL Consents & Preferences], reportez-vous à la section [création d&#39;un jeu de données](../../catalog/datasets/user-guide.md#create) du guide de l&#39;utilisateur du jeu de données, en suivant les étapes de création d&#39;un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-time Customer Profile], vous devez créer un schéma activé [!DNL Profile] en fonction de la classe [!DNL XDM Individual Profile] qui contient le type de données [!DNL Consents & Preferences]. Le jeu de données que vous créez en fonction de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux didacticiels ci-dessus pour connaître les étapes spécifiques liées aux [!DNL Real-time Customer Profile] exigences relatives aux schémas et aux jeux de données.
>
>En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour classer par priorité les ensembles de données qui contiennent les dernières données de consentement et de préférence, afin que les profils clients soient mis à jour correctement. Pour plus d&#39;informations, consultez l&#39;aperçu des [stratégies de fusion](../../rtcdp/profile/merge-policies.md).

## Traitement des modifications du consentement et des préférences

Lorsqu’un client modifie son consentement ou ses préférences sur votre site Web, ces modifications doivent être collectées et appliquées immédiatement à l’aide du [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Si un client choisit de ne pas participer à la collecte de données, toutes les collectes de données doivent cesser immédiatement. Si un client choisit de ne pas personnaliser, aucune personnalisation ne doit apparaître sur la page suivante qu’il visite.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires concernant le type de données [!DNL Consents & Preferences].

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

Pour vue le schéma complet du type de données [!DNL Consents & Preferences], consultez le [référentiel XDM officiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
