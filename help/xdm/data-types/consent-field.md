---
solution: Experience Platform
title: Type de données de champ de consentement générique
topic: aperçu
description: Ce document présente un aperçu du type de données XDM du champ de consentement générique.
translation-type: tm+mt
source-git-commit: ebcd8900687b6e91d3f06690a9db0e118bbc3b58
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---


# [!UICONTROL Type de données de ] champ de consentement générique

[!UICONTROL Les ] champs de consentement générique désignent un type de données XDM standard qui décrit la sélection d’un client pour une préférence de consentement particulière.

>[!NOTE]
>
>Ce type de données est destiné à être utilisé pour personnaliser la structure des schémas de consentement de votre organisation à l’aide de [[!UICONTROL Préférences de confidentialité/personnalisation/marketing (Consentements)] mixin](../mixins/profile/consents.md) comme base de référence.

![](../images/data-types/consent-field.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `val` | Chaîne | Le choix de consentement fourni par le client pour ce cas d’utilisation. Consultez le tableau ci-dessous pour connaître les valeurs et les définitions acceptées. |

Le tableau suivant présente les valeurs acceptées pour `val` :

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui | Le client a opté pour le consentement. En d&#39;autres termes, ils [a0/>acceptent **l&#39;utilisation de leurs données comme indiqué par le consentement en question.** |
| `n` | Non | Le client a choisi de ne pas consentir. En d&#39;autres termes, ils **ne donnent pas leur consentement à l&#39;utilisation de leurs données comme l&#39;indique le consentement en question.** |
| `p` | Vérification en attente | Le système n&#39;a pas encore reçu de valeur de consentement final. Il s&#39;agit le plus souvent d&#39;un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des courriers électroniques, ce consentement est défini sur `p` jusqu’à ce qu’il sélectionne un lien dans un courrier électronique pour vérifier qu’il a fourni l’adresse électronique correcte, auquel moment le consentement est mis à jour sur `y`.<br><br>Si ce consentement n&#39;utilise pas un processus de vérification à deux étapes, le  `p` choix peut être utilisé pour indiquer que le client n&#39;a pas encore répondu à l&#39;invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur `p` sur la première page d’un site Web avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui n&#39;exigent pas de consentement explicite, vous pouvez également l&#39;utiliser pour indiquer que le client n&#39;a pas explicitement choisi de se retirer (en d&#39;autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations relatives au consentement du client sont inconnues. |
| `LI` | Intérêt légitime | L&#39;intérêt commercial légitime de recueillir et de traiter ces données à des fins déterminées l&#39;emporte sur le préjudice qu&#39;elles peuvent causer à la personne. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec la personne. |
| `CP` | Respect d&#39;une obligation légale | La collecte de données à des fins déterminées est nécessaire pour satisfaire aux obligations légales de l&#39;entreprise. |
| `VI` | Intérêts vitaux du particulier | La collecte de données à des fins déterminées est nécessaire pour protéger les intérêts vitaux de l&#39;individu. |
| `PI` | Intérêt public | La collecte de données à des fins déterminées est nécessaire pour réaliser une tâche dans l&#39;intérêt public ou dans l&#39;exercice de l&#39;autorité officielle. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)