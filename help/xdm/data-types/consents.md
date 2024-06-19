---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;consentement;préférences;préférences;confidentialitéOptOuts;marketingPreferences;optOutType;baseOfProcessing;consentement;consentement
title: Type de données Consentements et Préférences
description: Le type de données Consentement pour la confidentialité, la personnalisation et les préférences marketing est destiné à prendre en charge la collecte des autorisations et préférences client générées par les plateformes de gestion du consentement (CMP) et d’autres sources provenant de vos opérations de données.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2278'
ht-degree: 1%

---

# [!UICONTROL Consentements et préférences] type de données

La variable [!UICONTROL Consentement pour la confidentialité, la personnalisation et les préférences marketing] type de données (ci-après appelé &quot;[!UICONTROL Consentements et préférences] type de données&quot;) est un [!DNL Experience Data Model] Type de données (XDM) destiné à prendre en charge la collecte des autorisations et préférences client générées par les plateformes de gestion du consentement (CMP) et d’autres sources provenant de vos opérations de données.

Ce document couvre la structure et l&#39;utilisation prévue des champs fournis par le [!UICONTROL Consentements et préférences] type de données.

## Conditions préalables {#prerequisites}

Ce document nécessite une compréhension pratique de XDM et de l’utilisation des schémas dans [!DNL Experience Platform]. Avant de poursuivre, consultez la documentation suivante :

* [Présentation du système XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr)
* [Principes de base de la composition des schémas](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Structure du type de données {#structure}

>[!IMPORTANT]
>
>La variable [!UICONTROL Consentements et préférences] le type de données est conçu pour couvrir un éventail de cas d’utilisation de la gestion des préférences et des consentements. Par conséquent, ce document décrit l’utilisation des champs du type de données en termes généraux et ne fait que des suggestions sur la manière dont vous devez interpréter l’utilisation de ces champs. Consultez votre équipe juridique de la confidentialité pour aligner la structure du type de données sur la manière dont votre organisation interprète et présente à vos clients ces choix de consentement et de préférence.

La variable [!UICONTROL Consentements et préférences] le type de données fournit plusieurs champs utilisés pour la capture. **consentement** et **préférence** informations.

Un consentement est une option qui permet à un client de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, dans la mesure où certaines juridictions exigent l’obtention d’une autorisation avant que les données ne puissent être utilisées d’une manière particulière, ou exigent que le client ait la possibilité d’arrêter cette utilisation (opt-out) si un consentement positif n’est pas requis.

Une préférence est une option qui permet au client de spécifier comment gérer différents aspects de son expérience avec une marque. Elles se divisent en deux catégories :

* **Préférences de personnalisation**: préférences concernant la manière dont la marque doit personnaliser les expériences diffusées à un client.
* **Préférences marketing**: préférences permettant à une marque de contacter un client par le biais de divers canaux.

La capture d’écran suivante montre comment la structure du type de données est représentée dans l’interface utilisateur de Platform :

![](../images/data-types/consents.png)

>[!TIP]
>
>Consultez le guide sur la [exploration des ressources XDM](../ui/explore.md) pour savoir comment rechercher une ressource XDM et examiner sa structure dans l’interface utilisateur de Platform.

Le fichier JSON suivant illustre un exemple du type de données que la variable [!UICONTROL Consentements et préférences] le type de données peut être traité. Les sections suivantes contiennent des informations sur l’utilisation spécifique de chacun de ces champs.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
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
>* [Génération d’exemples de données dans l’API](../api/sample-data.md)

## `consents` {#choices}

`consents` contient plusieurs champs qui décrivent les consentements et les préférences d’un client. Ces champs sont décrits plus en détail dans les sous-sections ci-dessous.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
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
"collect": {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Choix du consentement fourni par le client pour ce cas d’utilisation. Voir [annexe](#choice-values) pour les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `adID`

`adID` représente le consentement du client pour savoir si un ID d’annonceur peut être utilisé pour lier le client à l’ensemble des applications de cet appareil.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `idType` | Le type d’ID de publicité, soit `IDFA` pour Apple ID pour les annonceurs ou `GAID` pour Google Advertiser ID, également appelé Android Advertiser ID (AAID). |
| `val` | Choix du consentement fourni par le client pour ce cas d’utilisation. Voir [annexe](#choice-values) pour les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `share`

`share` représente le consentement du client pour que ses données puissent être partagées avec (ou vendues à) des tiers ou des tiers.

```json
"share": {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Choix du consentement fourni par le client pour ce cas d’utilisation. Voir [annexe](#choice-values) pour les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` capture les préférences des clients concernant les façons dont leurs données peuvent être utilisées pour la personnalisation. Les clients peuvent se désabonner de cas d’utilisation de personnalisation spécifiques ou se désabonner entièrement de la personnalisation.

>[!IMPORTANT]
>
>`personalize` ne couvre pas les cas d’utilisation marketing. Par exemple, si un client choisit de ne pas se personnaliser pour tous les canaux, il ne doit pas cesser de recevoir des communications par le biais de ces canaux. Au contraire, les messages qu&#39;ils reçoivent doivent être génériques et non basés sur leur profil.
>
>Par le même exemple, si un client choisit de ne pas participer au marketing direct pour tous les canaux (via `marketing`, expliqué dans la section [section suivante](#marketing)), ce client ne doit recevoir aucun message, même si la personnalisation est autorisée.

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
| `val` | La préférence de personnalisation fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle la personnalisation doit se dérouler. Voir [annexe](#choice-values) pour les valeurs et définitions acceptées. |

{style="table-layout:auto"}

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
| `preferred` | Indique le canal préféré du client pour la réception des communications. Voir [annexe](#preferred-values) pour les valeurs acceptées. |
| `any` | Représente les préférences du client pour le marketing direct dans son ensemble. La préférence de consentement fournie dans ce champ est considérée comme la préférence &quot;par défaut&quot; pour tout canal marketing, sauf si elle est remplacée par des sous-champs supplémentaires fournis sous `marketing`. Si vous envisagez d’utiliser des options de consentement plus granulaires, il est recommandé d’exclure ce champ.<br><br>Si la valeur est définie sur `n`, tous les paramètres de personnalisation plus spécifiques doivent être ignorés. Si la valeur est définie sur `y`, toutes les options de personnalisation plus affinées doivent également être traitées comme `y`, sauf si défini explicitement sur `n`. Si la valeur n’est pas définie, les valeurs de chaque option de personnalisation doivent être honorées comme indiqué. |
| `email` | Indique si le client accepte de recevoir des emails. |
| `push` | Indique si le client autorise la réception de notifications push. |
| `sms` | Indique si le client accepte de recevoir des SMS. |
| `val` | La préférence fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas à être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle doit se baser le cas d’utilisation marketing. Voir [annexe](#choice-values) pour les valeurs et définitions acceptées. |
| `time` | Horodatage ISO 8601 du moment où la préférence marketing a changé, le cas échéant. Notez que si l’horodatage d’une préférence individuelle est identique à celui fourni sous `metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `reason` | Lorsqu’un client s’exclut d’un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle le client s’est désinscrit. |

{style="table-layout:auto"}

### `metadata`

`metadata` capture les métadonnées générales sur les consentements et préférences du client chaque fois qu’ils ont été mis à jour pour la dernière fois.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriété | Description |
| --- | --- |
| `time` | Horodatage ISO 8601 de la dernière mise à jour des consentements et préférences du client. Ce champ peut être utilisé au lieu d’appliquer des horodatages à des préférences individuelles afin de réduire la charge et la complexité. Fournir une `time` la valeur sous une préférence individuelle remplace la valeur `metadata` horodatage de cette préférence particulière. |

{style="table-layout:auto"}

## Ingestion des données à l’aide du type de données {#ingest}

Pour utiliser la variable [!UICONTROL Consentements et préférences] type de données pour ingérer des données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma qui contient ce type de données.

Voir le tutoriel sur [création d’un schéma dans l’interface utilisateur](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment attribuer des types de données à des champs. Une fois que vous avez créé un schéma contenant un champ avec la propriété [!UICONTROL Consentements et préférences] type de données, voir la section sur [création d’un jeu de données](../../catalog/datasets/user-guide.md#create) dans le guide d’utilisation du jeu de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-Time Customer Profile], vous devez créer une [!DNL Profile]Schéma activé en fonction de la variable [!DNL XDM Individual Profile] qui contient la classe [!UICONTROL Consentements et préférences] type de données. Le jeu de données que vous créez à partir de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux tutoriels liés ci-dessus pour connaître les étapes spécifiques liées à [!DNL Real-Time Customer Profile] conditions requises pour les schémas et les jeux de données.
>
>En outre, vous devez également vous assurer que vos stratégies de fusion sont configurées pour prioriser le ou les jeux de données qui contiennent les dernières données de consentement et de préférence, afin que les profils client soient correctement mis à jour. Consultez la présentation sur [stratégies de fusion](../../rtcdp/profile/merge-policies.md) pour plus d’informations.

## Gestion des modifications du consentement et des préférences

Lorsqu’un client modifie ses consentements ou ses préférences sur votre site web, ces modifications doivent être collectées et appliquées immédiatement à l’aide de la variable [SDK Web Adobe Experience Platform](../../web-sdk/commands/setconsent.md). Si un client choisit de ne pas participer à la collecte de données, toute collecte de données doit immédiatement cesser. Si un client s’exclut de la personnalisation, aucune personnalisation ne doit être présente sur la page suivante qu’il consulte.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires concernant la variable [!UICONTROL Consentements et préférences] type de données.

### Valeurs acceptées pour `val` {#choice-values}

Le tableau suivant décrit les valeurs acceptées pour `val`:

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui (inclusion) | Le client a donné son consentement ou sa préférence. En d&#39;autres termes, ils **do** le consentement à l’utilisation de leurs données, comme indiqué par le consentement ou la préférence en question. |
| `n` | Non (opt-out) | Le client s’est désabonné du consentement ou de la préférence. En d&#39;autres termes, ils **ne pas** le consentement à l’utilisation de leurs données, comme indiqué par le consentement ou la préférence en question. |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de consentement ou de préférence finale. Il est le plus souvent utilisé dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des emails, ce consentement est défini sur `p` jusqu’à ce qu’ils sélectionnent un lien dans un courrier électronique pour vérifier qu’ils ont fourni l’adresse électronique correcte, à ce moment-là le consentement est mis à jour pour `y`.<br><br>Si ce consentement ou cette préférence n’utilise pas un processus de vérification à deux ensembles, la variable `p` choix peut être utilisé pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web, avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui ne requièrent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client n’a pas explicitement exercé son droit d’opposition (en d’autres termes, le consentement est supposé). |
| `u` | Inconnu | Les informations de consentement ou de préférence du client sont inconnues. |
| `dy` | Par défaut : Oui (inclusion) | Le client n’a pas fourni de valeur de consentement lui-même et est traité comme un accord préalable (&quot;Oui&quot;) par défaut. En d’autres termes, le consentement est supposé jusqu’à ce que le client indique le contraire.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `dn` | Non par défaut (opt-out) | Le client n’a pas fourni de valeur de consentement lui-même et est traité comme un droit d’opposition (&quot;Non&quot;) par défaut. En d’autres termes, le client est supposé avoir refusé le consentement jusqu’à ce qu’il en indique autrement.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `LI` | L&#39;intérêt légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiées l’emporte sur le préjudice potentiel qu’elles peuvent causer à l’individu. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec l’individu. |
| `CP` | Respect d’une obligation juridique | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations légales de l’entreprise. |
| `VI` | Intérêt vital de l’individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l’individu. |
| `PI` | Intérêt public | La collecte de données aux fins spécifiées est nécessaire pour effectuer une tâche dans l’intérêt public ou dans l’exercice de l’autorité officielle. |

{style="table-layout:auto"}

### Valeurs acceptées pour `preferred` {#preferred-values}

Le tableau suivant décrit les valeurs acceptées pour `preferred`. La variable `preferred` les valeurs indiquent le canal préféré du client pour la réception de communications qui l’informerait sur la collecte de données, les politiques de confidentialité et les options de personnalisation.

| Valeur | Description |
| --- | --- |
| `email` | Cette préférence indique le consentement du client pour recevoir des messages par courrier électronique. |
| `push` | Cette préférence indique le consentement du client pour recevoir des notifications push. Il s’agit de messages ou d’alertes envoyés directement à leur appareil, souvent à partir d’une application mobile. |
| `inApp` | Cette préférence indique le consentement du client pour la réception de messages in-app. Ces messages sont diffusés dans une application mobile ou web et fournissent des informations pendant que l’utilisateur est activement impliqué dans l’application. |
| `sms` | Cette préférence indique le consentement du client pour recevoir des messages par SMS (Short Message Service). Il s’agit de SMS envoyés à leur téléphone mobile. |
| `phone` | Cette préférence indique le consentement du client pour recevoir des communications par le biais d’interactions d’appel téléphonique. |
| `phyMail` | Cette préférence indique le consentement du client pour recevoir du matériel par courrier physique. |
| `inVehicle` | Cette préférence indique le consentement du client pour recevoir des notifications lorsqu’il se trouve dans son véhicule. Ces messages peuvent être diffusés par le biais de systèmes d’information sur les véhicules ou d’autres canaux de communication internes au véhicule. |
| `inHome` | Cette préférence indique le consentement du client pour recevoir les messages pendant son séjour à l’domicile. Ces messages peuvent être diffusés par le biais de périphériques d’accueil intelligents ou d’autres canaux de communication basés sur l’accueil. |
| `iot` | Cette préférence indique le consentement du client pour recevoir des messages liés à l’Internet des objets (IoT). Ces messages peuvent être diffusés par le biais de périphériques et de systèmes connectés au sein de leur environnement. |
| `social` | Cette préférence indique le consentement du client pour recevoir des communications par le biais des plateformes de médias sociaux. |
| `other` | Cette préférence englobe les canaux qui ne correspondent pas aux catégories standard. Il représente des canaux de communication spécialisés ou alternatifs qui peuvent être spécifiques à une entreprise ou à un secteur d’activité particulier. |
| `none` | Cette préférence indique que le client n’a pas de canal de communication préféré. |
| `unknown` | Cette préférence signifie que le canal de communication préféré du client n’est pas connu ou n’a pas été spécifié. Cela peut se produire si le client n’a pas fourni d’informations de consentement ou de préférence explicites. |

{style="table-layout:auto"}

### Complet [!UICONTROL Consentements et préférences] schema {#full-schema}

Pour afficher le schéma complet de la variable [!UICONTROL Consentements et préférences] type de données, voir [référentiel XDM officiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
