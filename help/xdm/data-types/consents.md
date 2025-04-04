---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;consentement;Consentement;préférences;Préférences;privacyOptOuts;préférences marketing;optOutType;baseOfProcessing;consentement;Consentement
title: Type de données Consentements et préférences
description: Le type de données Consentement pour les préférences de confidentialité, de Personalization et de marketing est destiné à prendre en charge la collecte des autorisations et des préférences des clients générées par les plateformes de gestion du consentement (CMP) et d’autres sources à partir de vos opérations de données.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 1%

---

# Type de données [!UICONTROL Consentements et préférences]

Le type de données [!UICONTROL Consentement pour les préférences de confidentialité, de Personalization et de marketing] (ci-après dénommé « type de données [!UICONTROL Consentements et préférences] ») est un type de données [!DNL Experience Data Model] (XDM) destiné à prendre en charge la collecte des autorisations et des préférences des clients générées par les plateformes de gestion du consentement (CMP) et d’autres sources à partir de vos opérations de données.

Ce document couvre la structure et l’utilisation prévue des champs fournis par le type de données [!UICONTROL  Consentements et préférences ].

## Conditions préalables {#prerequisites}

Ce document nécessite une compréhension pratique de XDM et de l’utilisation des schémas dans [!DNL Experience Platform]. Veuillez consulter la documentation suivante avant de continuer :

* [Présentation du système XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr)
* [Principes de base de la composition des schémas](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Structure du type de données {#structure}

>[!IMPORTANT]
>
>Le type de données [!UICONTROL  Consentements et préférences ] est conçu pour couvrir un large éventail de cas d’utilisation de la gestion des préférences et du consentement. Par conséquent, ce document décrit l’utilisation des champs du type de données en termes généraux et ne fait que des suggestions sur la façon d’interpréter l’utilisation de ces champs. Veuillez consulter votre équipe juridique en charge de la confidentialité pour aligner la structure du type de données sur la manière dont votre organisation interprète et présente ces choix de consentement et de préférence à vos clients.

Le type de données [!UICONTROL Consentements et préférences] fournit plusieurs champs utilisés pour capturer des informations de **consentement** et **préférence**.

Le consentement est une option qui permet à un client ou une cliente de spécifier comment ses données peuvent être utilisées. La plupart des consentements ont un aspect juridique, en ce sens que certaines juridictions exigent l&#39;obtention d&#39;une autorisation avant que les données puissent être utilisées d&#39;une manière particulière, ou exigent que le client ait une option pour arrêter cette utilisation (opt-out) si un consentement affirmatif n&#39;est pas requis.

Une préférence est une option qui permet au client ou à la cliente de spécifier comment différents aspects de son expérience avec une marque doivent être traités. Elles se répartissent en deux catégories :

* **Préférences Personalization** : préférences concernant la manière dont la marque doit personnaliser les expériences diffusées à un client.
* **Préférences marketing** : préférences concernant l’autorisation ou non d’une marque à contacter un client par le biais de divers canaux.

La capture d’écran suivante montre comment la structure du type de données est représentée dans l’interface utilisateur d’Experience Platform :

![](../images/data-types/consents.png)

>[!TIP]
>
>Consultez le guide sur l’[exploration des ressources XDM](../ui/explore.md) vers pour savoir comment rechercher n’importe quelle ressource XDM et inspecter sa structure dans l’interface utilisateur d’Experience Platform.

Le fichier JSON suivant illustre un exemple du type de données que le type de données [!UICONTROL Consentements et préférences] peut traiter. Vous trouverez des informations sur l’utilisation spécifique de chacun de ces champs dans les sections suivantes.

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
>Vous pouvez générer des exemples de données JSON pour tout schéma XDM défini dans Experience Platform afin de visualiser plus facilement la manière dont vos données de consentement et de préférence client doivent être mappées. Pour plus d’informations, consultez la documentation suivante :
>
>* [Générer des exemples de données dans l’interface utilisateur](../ui/sample.md)
>* [Générer des exemples de données dans l’API](../api/sample-data.md)

## `consents` {#choices}

`consents` contient plusieurs champs qui décrivent les consentements et les préférences d’un client ou d’une cliente. Ces champs sont décrits en détail dans les sous-sections ci-dessous.

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
| `val` | Choix de consentement fourni par le client pour ce cas d’utilisation. Voir l’[annexe](#choice-values) pour connaître les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `adID`

`adID` représente le consentement du client pour savoir si un ID d’annonceur peut être utilisé pour lier le client dans les applications sur cet appareil.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `idType` | Type d’ID d’annonce, `IDFA` pour l’ID d’Apple pour les annonceurs ou `GAID` pour l’ID d’annonceur Google, également appelé ID d’annonceur Android (AAID). |
| `val` | Choix de consentement fourni par le client pour ce cas d’utilisation. Voir l’[annexe](#choice-values) pour connaître les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `share`

`share` représente le consentement du client quant à savoir si ses données peuvent être partagées avec (ou vendues à) des secondes ou des tiers.

```json
"share": {
  "val": "y"
}
```

| Propriété | Description |
| --- | --- |
| `val` | Choix de consentement fourni par le client pour ce cas d’utilisation. Voir l’[annexe](#choice-values) pour connaître les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` capture les préférences des clients concernant les façons dont leurs données peuvent être utilisées pour la personnalisation. Les clients peuvent se désabonner de cas d’utilisation de personnalisation spécifiques, ou se désabonner entièrement de la personnalisation.

>[!IMPORTANT]
>
>`personalize` ne couvre pas les cas d’utilisation marketing. Par exemple, si un client choisit de ne pas utiliser la personnalisation pour tous les canaux, il ne doit pas cesser de recevoir des communications par ces canaux. Les messages qu’ils reçoivent doivent être génériques et non basés sur leur profil.
>
>Dans le même exemple, si un client se désinscrit du marketing direct pour tous les canaux (par le biais de `marketing`, comme expliqué dans la [section suivante](#marketing)), il ne doit pas recevoir de messages, même si la personnalisation est autorisée.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propriété | Description |
| --- | --- |
| `content` | Représente les préférences du client pour le contenu personnalisé sur votre site web ou application. |
| `val` | Préférence de personnalisation fournie par le client pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas besoin d’être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle la personnalisation doit être effectuée. Voir l’[annexe](#choice-values) pour connaître les valeurs et définitions acceptées. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` capture les préférences des clients concernant les objectifs marketing pour lesquels leurs données peuvent être utilisées. Les clients peuvent se désabonner de cas d’utilisation marketing spécifiques, ou se désabonner entièrement du marketing direct.

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
| `preferred` | Indique le canal préféré du client ou de la cliente pour recevoir des communications. Voir l’[annexe](#preferred-values) pour connaître les valeurs acceptées. |
| `any` | Représente les préférences du client pour le marketing direct dans son ensemble. La préférence de consentement fournie dans ce champ est considérée comme la préférence « par défaut » pour tout canal marketing, sauf si elle est remplacée par des sous-champs supplémentaires fournis sous `marketing`. Si vous prévoyez d’utiliser des options de consentement plus granulaires, il est recommandé d’exclure ce champ.<br><br>Si la valeur est définie sur `n`, tous les paramètres de personnalisation plus spécifiques doivent être ignorés. Si la valeur est définie sur `y`, toutes les options de personnalisation plus précises doivent également être traitées comme des `y`, sauf si elles sont explicitement définies sur `n`. Si la valeur n’est pas définie, les valeurs de chaque option de personnalisation doivent être respectées comme spécifié. |
| `email` | Indique si le client accepte de recevoir des emails. |
| `push` | Indique si le client autorise la réception de notifications push. |
| `sms` | Indique si le client accepte de recevoir des SMS. |
| `val` | Préférence fournie par le client ou la cliente pour le cas d’utilisation spécifié. Dans les cas où le client n’a pas besoin d’être invité à donner son consentement, la valeur de ce champ doit indiquer la base sur laquelle le cas d’utilisation marketing doit avoir lieu. Voir l’[annexe](#choice-values) pour connaître les valeurs et définitions acceptées. |
| `time` | Date et heure ISO 8601 du moment où la préférence marketing a changé, le cas échéant. Notez que si l’horodatage d’une préférence individuelle est identique à celui fourni sous `metadata`, ce champ ne doit pas être défini pour cette préférence. |
| `reason` | Lorsqu’un client se désinscrit d’un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle le client s’est désinscrit. |

{style="table-layout:auto"}

### `metadata`

`metadata` capture les métadonnées générales concernant les consentements et préférences du client ou de la cliente à chaque dernière mise à jour.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriété | Description |
| --- | --- |
| `time` | Date et heure ISO 8601 de la dernière mise à jour des consentements et préférences du client. Vous pouvez utiliser ce champ au lieu d’appliquer des horodatages à des préférences individuelles afin de réduire la charge et la complexité. La fourniture d’une valeur `time` sous une préférence individuelle remplace l’horodatage `metadata` de cette préférence particulière. |

{style="table-layout:auto"}

## Ingestion de données à l’aide du type de données {#ingest}

Pour utiliser le type de données [!UICONTROL Consentements et préférences] afin d’ingérer les données de consentement de vos clients, vous devez créer un jeu de données basé sur un schéma contenant ce type de données.

Consultez le tutoriel sur la [création d’un schéma dans l’interface utilisateur](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment attribuer des types de données aux champs. Une fois que vous avez créé un schéma contenant un champ avec le type de données [!UICONTROL Consentements et préférences], reportez-vous à la section relative à la [création d’un jeu de données](../../catalog/datasets/user-guide.md#create) dans le guide d’utilisation des jeux de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-Time Customer Profile], vous devez créer un schéma activé pour [!DNL Profile] basé sur la classe [!DNL XDM Individual Profile] qui contient le type de données [!UICONTROL Consentements et préférences]. Le jeu de données que vous créez à partir de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux tutoriels liés ci-dessus pour obtenir des instructions spécifiques relatives aux exigences en matière de [!DNL Real-Time Customer Profile] pour les schémas et les jeux de données.
>
>En outre, vous devez également vous assurer que vos politiques de fusion sont configurées pour donner la priorité au(x) jeu(x) de données contenant les dernières données de consentement et de préférence, afin que les profils clients soient correctement mis à jour. Pour plus d’informations, consultez la présentation des [politiques de fusion](../../rtcdp/profile/merge-policies.md).

## Gérer les modifications de consentement et de préférence

Lorsqu’un client modifie ses consentements ou ses préférences sur votre site web, ces modifications doivent être collectées et immédiatement appliquées à l’aide de [Adobe Experience Platform Web SDK](../../web-sdk/commands/setconsent.md). Si un client se désinscrit de la collecte de données, toute collecte de données doit immédiatement cesser. Si un client refuse la personnalisation, aucune personnalisation ne doit figurer sur la page suivante qu’il visite.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires concernant le type de données [!UICONTROL Consentements et préférences].

### Valeurs acceptées pour `val` {#choice-values}

Le tableau suivant décrit les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui (opt-in) | Le client a choisi le consentement ou la préférence. En d’autres termes, ils **consentent** à l’utilisation de leurs données comme indiqué par le consentement ou la préférence en question. |
| `n` | Non (opt-out) | Le client s’est opposé au consentement ou à la préférence. En d&#39;autres termes, ils **ne consentent pas** à l&#39;utilisation de leurs données comme indiqué par le consentement ou la préférence en question. |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de consentement ou de préférence finale. Elle est le plus souvent utilisée dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client accepte de recevoir des e-mails, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un e-mail pour vérifier qu’il a fourni la bonne adresse e-mail. À ce stade, le consentement est mis à jour sur `y`.<br><br>Si ce consentement ou cette préférence n’utilise pas un processus de vérification à deux ensembles, le choix `p` peut alors être utilisé pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web, avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui n’exigent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client ne s’est pas explicitement opposé (en d’autres termes, le consentement est présumé).<br><br> Bien que cette valeur puisse être ingérée dans le [!DNL Profile] à l’aide d’autres mécanismes, tels que l’ingestion par flux, elle n’est **pas prise en charge** pour la collecte de données ou la collecte de consentement sur [!DNL Edge Network]. Bien que la valeur `p` ne puisse pas être envoyée explicitement, la file d’attente des événements est toujours gérée par le [[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md) et l’événement est distribué à [!DNL Edge Network] une fois le consentement de l’utilisateur final explicitement `in`. |
| `u` | Inconnu | Les informations de consentement ou de préférence du client sont inconnues. |
| `dy` | Valeur par défaut de Oui (opt-in) | Le client n&#39;a pas fourni lui-même de valeur de consentement et est traité par défaut comme un accord préalable (« Oui »). En d’autres termes, le consentement est présumé jusqu’à ce que le client indique le contraire.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `dn` | Valeur par défaut de Non (opt-out) | Le client n&#39;a pas fourni lui-même de valeur de consentement et est traité par défaut comme un désabonnement (« Non »). En d’autres termes, le client est présumé avoir refusé son consentement jusqu’à ce qu’il indique le contraire.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `LI` | Intérêt Légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiques l’emporte sur le préjudice potentiel qu’elles peuvent causer à la personne concernée. |
| `CT` | Contrat | La collecte de données à des fins précises est nécessaire pour respecter les obligations contractuelles avec la personne concernée. |
| `CP` | Respect d&#39;une obligation légale | La collecte de données à des fins précises est nécessaire pour respecter les obligations légales de l&#39;entreprise. |
| `VI` | Intérêt vital de l&#39;individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l&#39;individu. |
| `PI` | Intérêt Public | La collecte de données à des fins spécifiques est nécessaire à l&#39;exécution d&#39;une mission d&#39;intérêt public ou dans l&#39;exercice de l&#39;autorité publique. |

{style="table-layout:auto"}

### Valeurs acceptées pour `preferred` {#preferred-values}

Le tableau suivant décrit les valeurs acceptées pour `preferred`. Les valeurs `preferred` indiquent le canal préféré du client ou de la cliente pour recevoir des communications qui l’informeraient sur la collecte de données, les politiques de confidentialité et les options de personnalisation.

| Valeur | Description |
| --- | --- |
| `email` | Cette préférence indique le consentement du client à recevoir des messages par e-mail. |
| `push` | Cette préférence indique le consentement du client à recevoir des notifications push. Il s’agit de messages ou d’alertes envoyés directement à leur appareil, souvent une application mobile. |
| `inApp` | Cette préférence indique le consentement du client à recevoir des messages in-app. Ces messages sont diffusés dans une application mobile ou web et fournissent des informations lorsque l’utilisateur ou l’utilisatrice participe activement à l’application. |
| `sms` | Cette préférence indique le consentement du client à recevoir des messages par SMS (Short Message Service). Il s’agit de messages texte envoyés à leur téléphone mobile. |
| `phone` | Cette préférence indique le consentement du client à recevoir des communications par le biais d’interactions d’appels téléphoniques. |
| `phyMail` | Cette préférence indique le consentement du client à recevoir du matériel par courrier physique. |
| `inVehicle` | Cette préférence indique le consentement du client à recevoir des notifications lorsqu’il est dans son véhicule. Ces messages peuvent être diffusés par l&#39;intermédiaire de systèmes d&#39;infodivertissement du véhicule ou d&#39;autres canaux de communication embarqués. |
| `inHome` | Cette préférence indique le consentement du client à recevoir des messages à la maison. Ces messages peuvent être diffusés par le biais d’appareils domestiques intelligents ou d’autres canaux de communication à domicile. |
| `iot` | Cette préférence indique le consentement du client à recevoir des messages liés à l’Internet des objets (IoT). Ces messages peuvent être diffusés par l’intermédiaire d’appareils et de systèmes connectés au sein de leur environnement. |
| `social` | Cette préférence indique le consentement du client à recevoir des communications par le biais des plateformes de médias sociaux. |
| `other` | Cette préférence englobe les canaux qui ne correspondent pas aux catégories standard. Il s’agit de canaux de communication alternatifs ou spécialisés qui peuvent être spécifiques à une entreprise ou à un secteur d’activité particulier. |
| `none` | Cette préférence indique que le client n’a pas de canal de communication préféré. |
| `unknown` | Cette préférence signifie que le canal de communication préféré du client n’est pas connu ou n’a pas été spécifié. Cela peut se produire si le client n’a pas fourni d’informations explicites de consentement ou de préférence. |

{style="table-layout:auto"}

### Schéma complet [!UICONTROL Consentements et préférences] {#full-schema}

Pour afficher le schéma complet du type de données [!UICONTROL Consentements et préférences], reportez-vous à la section [référentiel XDM officiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
