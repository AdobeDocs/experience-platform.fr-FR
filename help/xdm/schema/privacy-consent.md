---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: Présentation du mixage de confidentialité
description: Le mixin Préférences de confidentialité/marketing (Consentement) est un mélange de modèle de données d’expérience (XDM) destiné à prendre en charge la collecte des autorisations et préférences utilisateur générées par les CMP et d’autres sources provenant de clients. Ce document couvre la structure et l'utilisation prévue des différents champs fournis par le mixin.
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 1%

---


# [!DNL Privacy Consent] présentation du mixin

Le [!DNL Privacy/Marketing Preferences (Consent)] mixin (ci-après dénommé &quot;[!DNL Privacy Consent] mixin&quot;) est un mixin [!DNL Experience Data Model] (XDM) destiné à soutenir la collecte des autorisations et préférences des utilisateurs générées par les CMP et d&#39;autres sources auprès des clients. Ce document couvre la structure et l&#39;utilisation prévue des différents champs fournis par le mixin.

## Conditions préalables  {#prerequisites}

Ce document exige une compréhension pratique de [!DNL Experience Data Model] (XDM) et l&#39;utilisation des schémas dans [!DNL Experience Platform]. Veuillez consulter la documentation suivante avant de continuer :

* [Présentation du système XDM](http://www.adobe.com/go/xdm-home-en)
* [Principes de base de la composition des schémas](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Exemple de schéma {#schema}

>[!NOTE]
>
>L&#39;exemple ci-dessous est destiné à illustrer la structure des données envoyées à [!DNL Platform] travers le [!DNL Privacy Consent] mixin, afin de donner un contexte à la section suivante du présent document qui explique les principaux champs fournis par le mixin. Un exemple complet de la structure du schéma se trouve dans l&#39; [appendice](#full-schema) à des fins de référence.

Le fichier JSON suivant présente un exemple du type de données que le [!DNL Privacy Consent] mixin peut traiter. Les informations sur l&#39;utilisation spécifique de chacun de ces champs sont fournies dans la section suivante.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Champs {#fields}

Les sections ci-dessous traitent de l&#39;utilisation de chacun des principaux champs fournis par le [!DNL Privacy Consent] mixin et de la manière dont leurs sous-champs doivent être structurés.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` est une baie qui représente les paramètres généraux d&#39;exclusion sélectionnés par le client. Plusieurs objets peuvent être inclus dans ce tableau, chacun représentant un type d&#39;exclusion spécifique et les préférences que le client a sélectionnées pour ce type.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Propriété | Description |
| --- | --- |
| `xdm:optOutType` | Type d’exclusion. Consultez l&#39; [annexe](#optOutType-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:optOutValue` | La préférence sélectionnée par le client pour ce type d’exclusion particulier. Consultez l&#39; [annexe](#choice-optOutValue-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:timestamp` | Horodatage ISO 8601 indiquant le moment où la préférence d’exclusion a changé, le cas échéant. |
| `xdm:basisOfProcessing` | Indique la base liée à la confidentialité selon laquelle les données doivent être collectées et traitées. Par défaut, ce champ est défini sur `consent`, ce qui indique que les données ne doivent être traitées que si l’utilisateur a donné son consentement (comme indiqué dans `xdm:optOutValue`).<br><br>Dans certains cas, il n’est pas nécessaire d’inviter les clients à consentir au traitement des données. `xdm:basisOfProcessing` doit être incluse dans l’objet opt-out dans ces cas, en indiquant la raison pour laquelle une invite de consentement n’a pas été fournie. Consultez l&#39; [annexe](#basisOfProcessing-values) pour connaître les valeurs et les définitions acceptées. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` capture les préférences des clients quant aux manières dont leurs données peuvent être utilisées pour la personnalisation. Les utilisateurs peuvent opt-out de cas d’utilisation spécifiques de la personnalisation ou opt-out de la personnalisation entièrement.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` ne couvre pas les cas d’utilisation marketing. Par exemple, si un client choisit de ne pas personnaliser ses messages électroniques, il n’arrêtera pas de les recevoir. Au contraire, les courriels qu&#39;ils reçoivent seront génériques et ne seront pas basés sur leur profil.
>
>Dans le même exemple, si un client choisit de ne pas participer au marketing par courriel (par `xdm:marketingPreferences`, comme expliqué dans la section [](#marketingPreferences)suivante), il ne recevra aucun courriel, même si la personnalisation du courriel est autorisée.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Propriété | Description |
| --- | --- |
| `xdm:default` | Les données fournies dans cet objet représentent les préférences du client pour la personnalisation dans son ensemble. |
| `xdm:details` | Tableau d’objets, un pour chaque type de personnalisation spécifique pour lequel le client a fourni des préférences. |
| `xdm:choice` | La préférence de consentement fournie par le client pour la personnalisation en général, ou un type de personnalisation spécifique, selon qu’elle est fournie sous `xdm:default` ou `xdm:details`, respectivement. Consultez l&#39; [annexe](#choice-optOutValue-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:type` | Les objets de la `xdm:details` baie doivent fournir ce champ pour indiquer le cas d&#39;utilisation de la personnalisation spécifique pour lequel le client fournit des données de consentement. Consultez l&#39; [annexe](#type-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:timestamp` | Horodatage ISO 8601 indiquant le moment où la préférence d’exclusion a changé, le cas échéant. |
| `xdm:basisOfProcessing` | Indique la base liée à la confidentialité selon laquelle les données doivent être collectées et traitées. Par défaut, ce champ est défini sur `consent`, ce qui indique que les données ne doivent être traitées que si l’utilisateur a donné son consentement (comme indiqué dans `xdm:choice`).<br><br>Dans certains cas, les clients n’ont pas à donner leur consentement à la personnalisation. `xdm:basisOfProcessing` doit être incluse dans l’objet opt-out dans ces cas, en indiquant la raison pour laquelle une invite de consentement n’a pas été fournie. Consultez l&#39; [annexe](#basisOfProcessing-values) pour connaître les valeurs et les définitions acceptées. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` capture les préférences des clients concernant les objectifs marketing auxquels leurs données peuvent être utilisées. Les utilisateurs peuvent opt-out de cas d’utilisation marketing spécifiques ou opt-out de marketing direct entièrement.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Propriété | Description |
| --- | --- |
| `xdm:default` | Les données fournies dans cet objet représentent les préférences du client pour le marketing direct dans son ensemble. |
| `xdm:details` | Tableau d’objets, un pour chaque cas d’utilisation marketing spécifique pour lequel le client a fourni des préférences. |
| `xdm:choice` | La préférence de consentement fournie par le client pour le marketing en général, ou un cas d’utilisation spécifique du marketing, selon qu’elle est fournie sous `xdm:default` ou `xdm:details`, respectivement. Consultez l&#39; [annexe](#choice-optOutValue-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:subscriptions` | Objet dont les clés représentent des abonnements spécifiques à une société, tels que des listes de publipostage ou des bulletins d’information. Chaque objet d&#39;abonnement doit à son tour contenir une `xdm:choice` valeur pour l&#39;abonnement en question. |
| `xdm:type` | Les objets de la `xdm:details` baie doivent fournir ce champ pour indiquer le cas d&#39;utilisation marketing spécifique pour lequel le client fournit des données de consentement. Consultez l&#39; [annexe](#type-values) pour connaître les valeurs et les définitions acceptées. |
| `xdm:timestamp` | Horodatage ISO 8601 indiquant le moment où la préférence d’exclusion a changé, le cas échéant. |
| `xdm:basisOfProcessing` | Indique la base liée à la confidentialité selon laquelle les données doivent être collectées et traitées. Par défaut, ce champ est défini sur `consent`, ce qui indique que les données ne doivent être traitées que si l’utilisateur a donné son consentement (comme indiqué dans `xdm:choice`).<br><br>Dans certains cas, les clients n’ont pas à donner leur accord pour le marketing direct. `xdm:basisOfProcessing` doit être incluse dans l’objet opt-out dans ces cas, en indiquant la raison pour laquelle une invite de consentement n’a pas été fournie. Consultez l&#39; [annexe](#basisOfProcessing-values) pour connaître les valeurs et les définitions acceptées. |

## Incorporation de données de consentement à l’aide du mixin {#ingest}

Pour utiliser le [!DNL Privacy Consent] mixin pour ingérer les données de consentement de vos clients, vous devez ajouter le mixin à un schéma nouveau ou existant et créer un jeu de données basé sur ce schéma.

Consultez le didacticiel sur la [création d’un schéma dans l’interface utilisateur](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) pour savoir comment ajouter des mixins à un schéma. Le[!DNL  Privacy Consent] mixin est compatible avec les schémas basés sur les classes [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Une fois que vous avez créé un schéma contenant le [!DNL Privacy Consent] mixin, reportez-vous à la section relative à la [création d’un jeu de données](../../catalog/datasets/user-guide.md#create) dans le guide d’utilisation du jeu de données, en suivant les étapes de création d’un jeu de données avec un schéma existant.

>[!IMPORTANT]
>
>Si vous souhaitez envoyer des données de consentement à [!DNL Real-time Customer Profile], vous devez créer un schéma [!DNL Profile]activé basé sur la [!DNL XDM Individual Profile] classe contenant le [!DNL Privacy Consent] mixin. Le jeu de données que vous créez en fonction de ce schéma doit également être activé pour [!DNL Profile]. Reportez-vous aux didacticiels ci-dessus pour connaître les étapes spécifiques liées aux [!DNL Real-time Customer Profile] exigences.

## Annexe {#appendix}

Les sections ci-dessous fournissent des informations de référence supplémentaires sur le [!DNL Privacy Consent] mixin.

### Valeurs acceptées pour xdm:optOutType {#optOutType-values}

Le tableau suivant présente les valeurs acceptées pour `xdm:optOutType`:

| Valeur | Description |
| --- | --- |
| `general_opt_out` | Les données ne peuvent pas être utilisées à quelque fin que ce soit. Cela bloque généralement la collecte de données, sauf lorsque le traitement ne repose pas sur le &quot;consentement&quot;.<br><br>Lors de l’utilisation de ce type d’exclusion, les valeurs acceptées `in` et `out` obtiennent la signification contextuelle suivante :<ul><li>`in`: L’utilisateur **a donné son consentement** pour que ses données soient utilisées pour un traitement général.</li><li>`out`: L’utilisateur **n’accepte** pas que ses données soient utilisées pour le traitement général.</li></ul>Pour plus d’informations, voir le tableau des valeurs [acceptées pour xdm:optOutValue](#choice-optOutValue-values) . |
| `anonymous_analysis` | Les données ne peuvent pas être utilisées pour des mesures Web génériques qui ne nécessitent aucun type d’ID utilisateur, comme le nombre de fois où une page particulière a été consultée. |
| `device_linking` | Les données d&#39;un périphérique utilisé par un visiteur ne peuvent pas être combinées avec celles d&#39;un autre périphérique utilisé par ce même visiteur. Les périphériques sont liés à l’aide de techniques telles qu’un nom d’utilisateur ou une adresse électronique courants, souvent par l’intermédiaire de la coopérative de périphériques d’Adobe ou d’un graphique de périphériques privés. |
| `pseudonymous_analysis` | Les données ne peuvent pas être utilisées pour les mesures Web fournies par Adobe Analytics, qui requiert des identifiants pseudonymes pour identifier les chemins empruntés par les utilisateurs sur un site Web (tel qu’un rapport d’abandons), pour établir des sessions et à des fins d’attribution. |
| `sales_sharing_opt_out` | Les données ne peuvent pas être utilisées à des fins de vente ou de partage avec des tiers.<br><br>Lors de l’utilisation de ce type d’exclusion, les valeurs acceptées `in` et `out` obtiennent la signification contextuelle suivante :<ul><li>`in`: L’utilisateur **a donné son consentement** pour que ses données soient utilisées à des fins de vente et de partage.</li><li>`out`: L&#39;utilisateur **n&#39;accepte** pas que ses données soient utilisées à des fins de vente et de partage.</li></ul>Pour plus d’informations, voir le tableau des valeurs [acceptées pour xdm:optOutValue](#choice-optOutValue-values) . |

### Valeurs acceptées pour xdm:baseOfProcessing {#basisOfProcessing-values}

Le tableau suivant présente les valeurs acceptées pour `xdm:basisOfProcessing`:

| Valeur | Description |
| --- | --- |
| `consent` **(Par défaut)** | La collecte de données à l&#39;usage spécifié est autorisée, étant donné que l&#39;individu a fourni une autorisation explicite. Il s’agit de la valeur par défaut de `xdm:basisOfProcessing` si aucune autre valeur n’est fournie. <br><br>**IMPORTANT**: Les valeurs pour `xdm:choice` et `xdm:optOutValue` ne sont respectées que lorsque `xdm:basisOfProcessing` est défini sur `consent`. Si l&#39;une des autres valeurs indiquées dans ce tableau est utilisée à `xdm:basisOfProcessing` la place, les choix de consentement de la personne sont ignorés. |
| `compliance` | La collecte de données à des fins déterminées est nécessaire pour satisfaire aux obligations légales de l&#39;entreprise. |
| `contract` | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec la personne. |
| `legitimate_interest` | L&#39;intérêt commercial légitime de recueillir et de traiter ces données à des fins déterminées l&#39;emporte sur le préjudice qu&#39;elles peuvent causer à la personne. |
| `public_interest` | La collecte de données à des fins déterminées est nécessaire pour réaliser une tâche dans l&#39;intérêt public ou dans l&#39;exercice de l&#39;autorité officielle. |
| `vital_interest` | La collecte de données à des fins déterminées est nécessaire pour protéger les intérêts vitaux de l&#39;individu. |

### Valeurs acceptées pour xdm:choice et xdm:optOutValue {#choice-optOutValue-values}

Le tableau suivant présente les valeurs acceptées pour `xdm:choice` et `xdm:optOutValue`:

| Valeur | Description |
| --- | --- |
| `pending` | Le système n&#39;a pas encore reçu d&#39;informations concernant les préférences de consentement de la part du client. Peut être utilisé pour la première page d&#39;un site Web pendant que le consentement est obtenu. Il peut également être utilisé pour indiquer que le consentement est &quot;présumé&quot; plutôt que explicitement fourni. |
| `in` | L’utilisateur a choisi la préférence de consentement. En d&#39;autres termes, ils **consentent** à l&#39;utilisation de leurs données, comme l&#39;indique la préférence de consentement en question. |
| `out` | L’utilisateur a choisi de ne pas donner son consentement. En d&#39;autres termes, ils **ne consentent pas** à l&#39;utilisation de leurs données, comme l&#39;indique la préférence de consentement en question. |
| `not_applicable` | La préférence de consentement en question ne s&#39;applique pas au client. |
| `not_provided` | Le client n&#39;a fourni aucune information de préférence de consentement. |
| `unknown` | Les informations de préférence de consentement du client sont inconnues. |

### Valeurs acceptées pour xdm:type {#type-values}

Le tableau suivant présente les valeurs acceptées pour `xdm:type`:

| Valeur | Description |
| --- | --- |
| `ads` | Publicités qui peuvent être affichées à partir de sites Web non liés. |
| `content` | Contenu affiché sur votre site Web. |
| `customer_support` | Données relatives au service clientèle. |
| `email` | Canal Email. |
| `iot` | Données relatives à l&#39;&quot;Internet des choses&quot; (IoT). |
| `in_app_messages` | Les messages in-app. |
| `in_home` | Messages internes. |
| `in_store` | Messages en magasin. |
| `in_vehicle` | Messages embarqués. |
| `offers` | Offres spéciales. |
| `phone_calls` | Données relatives aux interactions d’appel téléphonique. |
| `push_notifications` | Notifications push. |
| `sms` | SMS. |
| `social_media` | Contenu des médias sociaux. |
| `snail_mail` | Messages envoyés par diffusion postale conventionnelle. |
| `third_party_content` | Contenu ou articles affichés sur votre site Web qui sont fournis par une entité non liée. |
| `third_party_offers` | offres ou publicités affichées sur votre site Web à partir de services publicitaires provenant d’une entité non liée. |

### Schéma complet [!DNL Privacy Consent] {#full-schema}

Le fichier JSON suivant représente le [!DNL Privacy Consent] schéma complet tel qu’il apparaît dans le registre des Schémas :

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
