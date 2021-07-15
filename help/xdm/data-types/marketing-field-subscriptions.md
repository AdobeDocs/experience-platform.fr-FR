---
solution: Experience Platform
title: Champ Générique De Préférences Marketing Avec Type De Données D’Abonnements
topic-legacy: overview
description: Ce document présente un aperçu du champ de préférences marketing générique avec le type de données XDM Abonnements .
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 3%

---

# [!UICONTROL Champ générique de préférences marketing avec type ] Subscriptionsdata

[!UICONTROL Le champ de préférences marketing générique avec ] abonnement est un type de données XDM standard qui décrit la sélection d’un client pour une préférence marketing spécifique.

>[!NOTE]
>
>Ce type de données est conçu pour être utilisé pour personnaliser la structure des schémas de consentement de votre organisation à l’aide du [[!UICONTROL groupe de champs Contenus et Préférences]](../field-groups/profile/consents.md) comme ligne de base.
>
>Si vous n’avez pas besoin d’une carte `subscriptions` pour un champ de préférence marketing particulier, vous pouvez utiliser le [type de données de champ marketing de base](./marketing-field.md) à la place.

![](../images/data-types/marketing-field-subscriptions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `reason` | Chaîne | Lorsqu’un client s’exclut d’un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle le client s’est désinscrit. |
| `subscriptions` | Carte | Mappage des préférences marketing client pour des abonnements spécifiques. Pour plus d’informations, consultez la section [abonnements](#subscriptions) . |
| `time` | DateTime | Horodatage ISO 8601 du moment où la préférence marketing a changé, le cas échéant. |
| `val` | Chaîne | Choix des préférences fournies par le client pour ce cas d’utilisation marketing. Voir la [section suivante](#val) pour connaître les valeurs et les définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

Le tableau suivant décrit les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a choisi la préférence. En d’autres termes, ils ont le **consentement** pour l’utilisation de leurs données, comme indiqué par la préférence en question. |
| `n` | Non | Le client s’est désinscrit de la préférence. En d’autres termes, ils **ne donnent pas leur consentement à l’utilisation de leurs données comme indiqué par la préférence en question.** |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de préférence finale. Il est le plus souvent utilisé dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des emails, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un email pour vérifier qu’il a fourni l’adresse email correcte, auquel moment le consentement est mis à jour sur `y`.<br><br>Si cette préférence n’utilise pas un processus de vérification à deux ensembles, le  `p` choix peut être utilisé pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui ne requièrent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client n’a pas explicitement exercé son droit d’opposition (en d’autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations de préférence du client sont inconnues. |
| `LI` | L&#39;intérêt légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiées l’emporte sur le préjudice potentiel qu’elles peuvent causer à l’individu. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec l’individu. |
| `CP` | Respect d’une obligation juridique | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations légales de l’entreprise. |
| `VI` | Intérêt vital de l’individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l’individu. |
| `PI` | Intérêt public | La collecte de données aux fins spécifiées est nécessaire pour effectuer une tâche dans l’intérêt public ou dans l’exercice de l’autorité officielle. |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

Certaines entreprises permettent aux clients de souscrire à différents abonnements associés à un canal marketing particulier. Par exemple, une société bancaire peut permettre aux clients de s’abonner à des alertes par téléphone pour des comptes surchargés ou de recevoir des appels de vente pour des offres de programme de fidélité.

Le fichier JSON suivant représente un exemple de champ marketing pour un canal marketing d’appel téléphonique qui contient une carte `subscriptions`. Chaque clé de l’objet `subscriptions` représente un abonnement individuel pour le canal marketing. De même, chaque abonnement contient une valeur d’opt-in (`val`).

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
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
| `type` | Type d’abonnement. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne 15 caractères ou moins. |
| `subscribers` | Champ facultatif de type map qui représente un ensemble d’identifiants (tels que les adresses électroniques ou les numéros de téléphone) abonnés à un abonnement particulier. Chaque clé de cet objet représente l’identifiant en question et contient deux sous-propriétés : <ul><li>`time`: Horodatage ISO 8601 du moment où l’identité s’est abonnée, le cas échéant.</li><li>`source`: Source d’où provient l’abonné. Il peut s’agir de n’importe quelle chaîne descriptive, à condition qu’elle contienne 15 caractères ou moins.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Ressources supplémentaires

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
