---
solution: Experience Platform
title: Type de données de champ de consentement générique
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Champ de consentement générique .
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 3%

---

# [!UICONTROL Type ] Champ de données de consentement générique

[!UICONTROL Champ de consentement générique ] d’un type de données XDM standard qui décrit la sélection d’un client pour une préférence de consentement spécifique.

>[!NOTE]
>
>Ce type de données est conçu pour être utilisé afin de personnaliser la structure des schémas de consentement de votre organisation à l’aide du [[!UICONTROL groupe de champs Confidentialité/Personnalisation/Préférences marketing (consentement)]](../field-groups/profile/consents.md) comme base.

![](../images/data-types/consent-field.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `val` | Chaîne | Choix du consentement fourni par le client pour ce cas d’utilisation. Consultez le tableau ci-dessous pour connaître les valeurs et définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

Le tableau suivant décrit les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a donné son consentement. En d’autres termes, ils ont le **consentement** pour l’utilisation de leurs données, comme indiqué par le consentement en question. |
| `n` | Non | Le client s’est désabonné du consentement. En d’autres termes, ils **ne donnent pas leur consentement à l’utilisation de leurs données comme indiqué par le consentement en question.** |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de consentement finale. Il est le plus souvent utilisé dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des emails, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un email pour vérifier qu’il a fourni l’adresse email correcte, auquel moment le consentement est mis à jour sur `y`.<br><br>Si ce consentement n’utilise pas un processus de vérification à deux ensembles, le  `p` choix peut être utilisé pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui ne requièrent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client n’a pas explicitement exercé son droit d’opposition (en d’autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations de consentement du client sont inconnues. |
| `LI` | L&#39;intérêt légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiées l’emporte sur le préjudice potentiel qu’elles peuvent causer à l’individu. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec l’individu. |
| `CP` | Respect d’une obligation juridique | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations légales de l’entreprise. |
| `VI` | Intérêt vital de l’individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l’individu. |
| `PI` | Intérêt public | La collecte de données aux fins spécifiées est nécessaire pour effectuer une tâche dans l’intérêt public ou dans l’exercice de l’autorité officielle. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
