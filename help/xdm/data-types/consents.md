---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;consentement;préférences;préférences;confidentialitéOptOuts;marketingPreferences;optOutType;baseOfProcessing;consentement;consentement
title: Type de données Consentements et Préférences
description: Le type de données Consentement pour la confidentialité, la personnalisation et les préférences marketing est destiné à prendre en charge la collecte des autorisations et préférences client générées par les plateformes de gestion du consentement (CMP) et d’autres sources provenant de vos opérations de données.
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 3%

---

# [!UICONTROL Type de données Consentements et ] Préférences

Le type de données [!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] (ci-après appelé le type de données &quot;[!UICONTROL Consentements et préférences]&quot;) est un type de données [!DNL Experience Data Model] (XDM) destiné à prendre en charge la collecte des autorisations et des préférences des clients générées par les plateformes de gestion du consentement (CMP) et d’autres sources issues de vos opérations de données.

Ce document couvre la structure et l’utilisation prévue des champs fournis par le type de données [!UICONTROL Contenus et Préférences] .

## Conditions préalables {#prerequisites}

Ce document nécessite une compréhension pratique de XDM et de l’utilisation des schémas dans [!DNL Experience Platform]. Avant de poursuivre, consultez la documentation suivante :

* [Présentation du système XDM](http://www.adobe.com/go/xdm-home-en)
* [Principes de base de la composition des schémas](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Structure du type de données {#structure}

>[!IMPORTANT]
>
>Le type de données [!UICONTROL Contenus et Préférences] est conçu pour couvrir divers cas d’utilisation de la gestion du consentement et des préférences. Par conséquent, ce document décrit l’utilisation des champs du type de données en termes généraux et ne fait que des suggestions sur la manière dont vous devez interpréter l’utilisation de ces champs. Consultez votre équipe juridique de la confidentialité pour aligner la structure du type de données sur la manière dont votre organisation interprète et présente à vos clients ces choix de consentement et de préférence.

Le type de données [!UICONTROL Contenus et Préférences] fournit plusieurs champs utilisés pour capturer les informations **consentement** et **préférence**.

Un consentement est une option qui permet à un client de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, dans la mesure où certaines juridictions exigent l’obtention d’une autorisation avant que les données ne puissent être utilisées d’une manière particulière, ou exigent que le client ait la possibilité d’arrêter cette utilisation (opt-out) si un consentement positif n’est pas requis.

Une préférence est une option qui permet au client de spécifier comment gérer différents aspects de son expérience avec une marque. Elles se divisent en deux catégories :

* **Préférences** de personnalisation : Préférences concernant la manière dont la marque doit personnaliser les expériences diffusées à un client.
* **Préférences marketing** : Préférences concernant le fait qu’une marque soit autorisée à contacter un client par le biais de divers canaux.

La capture d’écran suivante montre comment la structure du type de données est représentée dans l’interface utilisateur de Platform :

![](../images/data-types/consents.png)

>[!TIP]
>
>Consultez le guide sur l’[exploration des ressources XDM](../ui/explore.md) vers pour savoir comment rechercher une ressource XDM et examiner sa structure dans l’interface utilisateur de Platform.

Le fichier JSON suivant illustre un exemple du type de données que le type de données [!UICONTROL Contenus et Préférences] peut traiter. Les sections suivantes contiennent des informations sur l’utilisation spécifique de chacun de ces champs.

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
>Vous pouvez générer des exemples de données JSON pour tout schéma XDM que vous définissez dans Experience Platform afin de mieux visualiser la manière dont vos données de consentement et de préférence client doivent être mappées. Pour plus d’informations, consultez la documentation suivante :
>
>* [Génération d’exemples de données dans l’interface utilisateur](../ui/sample.md)
* [Génération d’exemples de données dans l’API](../api/sample-data.md)


## `consents` {#choices}

`consents` contient plusieurs champs qui décrivent les consentements et les préférences d’un client. Ces champs sont décrits plus en détail dans les sous-sections ci-dessous.

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
| `val` | Choix du consentement fourni par le client pour ce cas d’utilisation. Voir l’ [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

### `adID`

`adID` représente le consentement du client pour savoir si un ID d’annonceur (IDFA ou GAID) peut être utilisé pour lier le client à l’ensemble des applications de cet appareil.

```json
"adID" : {
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
| `email` | Indique si le client accepte de recevoir des emails. |
| `push` | Indique si le client autorise la réception de notifications push. |
| `sms` | Indique si le client accepte de recevoir des SMS. |
| `val` | La préférence fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle doit se baser le cas d’utilisation marketing. Voir l’ [annexe](#choice-values) pour connaître les valeurs et les définitions acceptées. |
| `time` | Horodatage ISO 8601 du moment où la préférence marketing a changé, le cas échéant. Notez que si l’horodatage d’une préférence individuelle est identique à celui fourni sous `metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `reason` | Lorsqu’un client s’exclut d’un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle le client s’est désinscrit. |

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

## Ingestion des données à l’aide du type de données {#ingest}

Pour utiliser le type de données [!UICONTROL Contenus et Préférences] afin d’ingérer des données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce type de données.

Consultez le tutoriel sur la [création d’un schéma dans l’interface utilisateur](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment attribuer des types de données aux champs. Une fois que vous avez créé un schéma contenant un champ avec le type de données [!UICONTROL Contenus et Préférences] , reportez-vous à la section sur la [création d’un jeu de données](../../catalog/datasets/user-guide.md#create) dans le guide d’utilisation du jeu de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
Si vous souhaitez envoyer des données de consentement à [!DNL Real-time Customer Profile], vous devez créer un schéma compatible [!DNL Profile] basé sur la classe [!DNL XDM Individual Profile] qui contient le type de données [!UICONTROL Contenus et Préférences]. Le jeu de données que vous créez à partir de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux tutoriels ci-dessus pour connaître les étapes spécifiques aux [!DNL Real-time Customer Profile] exigences relatives aux schémas et aux jeux de données.
En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour prioriser le ou les jeux de données qui contiennent les dernières données de consentement et de préférence, afin que les profils client soient correctement mis à jour. Pour plus d’informations, consultez la présentation des [stratégies de fusion](../../rtcdp/profile/merge-policies.md) .

## Gestion des modifications du consentement et des préférences

Lorsqu’un client modifie ses consentements ou ses préférences sur votre site web, ces modifications doivent être collectées et appliquées immédiatement à l’aide du [SDK Web Adobe Experience Platform](../../edge/consent/supporting-consent.md). Si un client choisit de ne pas participer à la collecte de données, toute collecte de données doit immédiatement cesser. Si un client s’exclut de la personnalisation, aucune personnalisation ne doit être présente sur la page suivante qu’il consulte.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires concernant le type de données [!UICONTROL Contenus et Préférences] .

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

Pour afficher le schéma complet pour le type de données [!UICONTROL Contenus et Préférences], reportez-vous au [référentiel XDM officiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
