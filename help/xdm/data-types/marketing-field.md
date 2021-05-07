---
solution: Experience Platform
title: Type de données de champ de préférence marketing générique
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM du champ de préférence marketing générique.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 2%

---

# [!UICONTROL Type de données ] champ de préférence marketing générique

[!UICONTROL Les ] champs de préférence marketing générique désignent un type de données XDM standard qui décrit la sélection d’un client pour une préférence marketing particulière.

>[!NOTE]
>
>Ce type de données est destiné à être utilisé pour personnaliser la structure des schémas de consentement de votre organisation à l’aide du [[!UICONTROL groupe de champs Confidentialité/Personnalisation/Préférences marketing (Contenus)]](../field-groups/profile/consents.md) comme base de référence.
>
>Si vous avez besoin d’un `subscriptions` mappage pour un champ de préférence marketing particulier, vous devez utiliser le champ [marketing avec le type de données abonnements](./marketing-field-subscriptions.md) à la place.

![](../images/data-types/marketing-field.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `reason` | Chaîne | Lorsqu’un client choisit de ne pas participer à un cas d’utilisation marketing, ce champ de chaîne représente la raison pour laquelle il s’est désabonné. |
| `time` | DateTime | Horodatage ISO 8601 indiquant le moment où la préférence marketing a changé, le cas échéant. |
| `val` | Chaîne | Choix de préférence fourni par le client pour ce cas d’utilisation marketing. Consultez le tableau ci-dessous pour connaître les valeurs et les définitions acceptées. |

Le tableau suivant présente les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a opté pour la préférence. En d&#39;autres termes, ils [a0/>font **consentent à l&#39;utilisation de leurs données, comme l&#39;indique la préférence en question.** |
| `n` | Non | Le client a choisi de ne pas bénéficier de cette préférence. En d&#39;autres termes, ils **n&#39;acceptent pas** l&#39;utilisation de leurs données comme l&#39;indique la préférence en question. |
| `p` | Vérification en attente | Le système n&#39;a pas encore reçu de valeur de préférence finale. Il s&#39;agit le plus souvent d&#39;un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des courriers électroniques, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un courrier électronique pour vérifier qu’il a fourni l’adresse électronique correcte, auquel moment le consentement est mis à jour sur `y`.<br><br>Si cette préférence n&#39;utilise pas un processus de vérification à deux ensembles, le  `p` choix peut être utilisé pour indiquer que le client n&#39;a pas encore répondu à l&#39;invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur `p` sur la première page d’un site Web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui n&#39;exigent pas de consentement explicite, vous pouvez également l&#39;utiliser pour indiquer que le client n&#39;a pas explicitement choisi de se retirer (en d&#39;autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations de préférence du client sont inconnues. |
| `LI` | Intérêt légitime | L&#39;intérêt commercial légitime de recueillir et de traiter ces données à des fins déterminées l&#39;emporte sur le préjudice qu&#39;elles peuvent causer à la personne. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec la personne. |
| `CP` | Respect d&#39;une obligation légale | La collecte de données à des fins déterminées est nécessaire pour satisfaire aux obligations légales de l&#39;entreprise. |
| `VI` | Intérêts vitaux du particulier | La collecte de données à des fins déterminées est nécessaire pour protéger les intérêts vitaux de l&#39;individu. |
| `PI` | Intérêt public | La collecte de données à des fins déterminées est nécessaire pour réaliser une tâche dans l&#39;intérêt public ou dans l&#39;exercice de l&#39;autorité officielle. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
