---
solution: Experience Platform
title: Champ Générique De Préférences Marketing Avec Type De Données D’Abonnements
description: Découvrez le type de données XDM Champ de préférences marketing générique avec abonnements .
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# Type de données [!UICONTROL Generic Marketing Preference Field with Subscriptions]

[!UICONTROL Generic Marketing Preference Field with Subscriptions] est un type de données XDM standard qui décrit la sélection d’un client pour une préférence marketing spécifique.

>[!NOTE]
>
>Ce type de données est conçu pour être utilisé pour personnaliser la structure des schémas de consentement de votre organisation à l’aide du groupe de champs [[!UICONTROL Contenus et Préférences]](../field-groups/profile/consents.md) comme ligne de base.
>
>Si vous n’avez pas besoin d’une carte `subscriptions` pour un champ de préférence marketing particulier, vous pouvez utiliser le [type de données de champ marketing de base](./marketing-field.md) à la place.

![](../images/data-types/marketing-field-subscriptions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `reason` | Chaîne | Lorsqu’un client s’exclut d’un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle le client s’est désinscrit. |
| `subscriptions` | Carte | Carte des préférences marketing client pour des abonnements spécifiques. Pour plus d’informations, consultez la section sur les [abonnements](#subscriptions) . |
| `time` | DateTime | Horodatage ISO 8601 du moment où la préférence marketing a changé, le cas échéant. |
| `val` | Chaîne | Choix des préférences fournies par le client pour ce cas d’utilisation marketing. Consultez la [section suivante](#val) pour connaître les valeurs et les définitions acceptées. |

{style="table-layout:auto"}

## `val` {#val}

Le tableau suivant décrit les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui (inclusion) | Le client a choisi la préférence. En d’autres termes, ils **font** consentent à l’utilisation de leurs données comme indiqué par la préférence en question. |
| `n` | Non (opt-out) | Le client s’est désinscrit de la préférence. En d’autres termes, ils **ne consentent pas** à l’utilisation de leurs données comme indiqué par la préférence en question. |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de préférence finale. Il est le plus souvent utilisé dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des emails, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un email pour vérifier qu’il a fourni l’adresse email correcte, auquel moment le consentement sera mis à jour sur `y`.<br><br>Si cette préférence n’utilise pas de processus de vérification à deux ensembles, le choix `p` peut être utilisé à la place pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui ne requièrent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client n’a pas explicitement exercé son droit d’opposition (en d’autres termes, le consentement est supposé). |
| `u` | Inconnu | Les informations de préférence du client sont inconnues. |
| `dy` | Par défaut : Oui (inclusion) | Le client n’a pas fourni de valeur de consentement lui-même et est traité comme un accord préalable (&quot;Oui&quot;) par défaut. En d’autres termes, le consentement est supposé jusqu’à ce que le client indique le contraire.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `dn` | Non par défaut (opt-out) | Le client n’a pas fourni de valeur de consentement lui-même et est traité comme un droit d’opposition (&quot;Non&quot;) par défaut. En d’autres termes, le client est supposé avoir refusé le consentement jusqu’à ce qu’il en indique autrement.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `LI` | L&#39;intérêt légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiées l’emporte sur le préjudice potentiel qu’elles peuvent causer à l’individu. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec l’individu. |
| `CP` | Respect d’une obligation juridique | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations légales de l’entreprise. |
| `VI` | Intérêt vital de l’individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l’individu. |
| `PI` | Intérêt public | La collecte de données aux fins spécifiées est nécessaire pour effectuer une tâche dans l’intérêt public ou dans l’exercice de l’autorité officielle. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Certaines entreprises permettent aux clients de souscrire à différents abonnements associés à un canal marketing particulier. Par exemple, une société bancaire peut permettre aux clients de s’abonner à des alertes par téléphone pour des comptes surchargés ou de recevoir des appels de vente pour des offres de programme de fidélité.

Le fichier JSON suivant représente un exemple de champ marketing pour un canal marketing d’appel téléphonique qui contient une carte `subscriptions`. Chaque clé de l’objet `subscriptions` représente un abonnement individuel pour le canal marketing. De même, chaque abonnement contient une valeur d’inclusion (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `val` | [valeur de consentement](#val) pour l’abonnement. |
| `type` | Type d’abonnement. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne 15 caractères ou moins. |
| `topics` | Tableau de chaînes représentant les centres d’intérêt auxquels un client s’est abonné, qui peut être utilisé pour lui envoyer du contenu pertinent. |
| `subscribers` | Champ facultatif de type map qui représente un ensemble d’identifiants (tels que les adresses électroniques ou les numéros de téléphone) abonnés à un abonnement particulier. Chaque clé de cet objet représente l’identifiant en question et contient deux sous-propriétés : <ul><li>`time` : horodatage ISO 8601 du moment où l’identité s’est abonnée, le cas échéant.</li><li>`source` : source d’où provient l’abonné. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne 15 caractères ou moins.</li></ul> |

{style="table-layout:auto"}

## Ressources supplémentaires

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
