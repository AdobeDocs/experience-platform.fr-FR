---
solution: Experience Platform
title: Type de données du champ de préférences de personnalisation générique
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Champ de préférences de personnalisation générique.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: 0f39e9237185b49417f2af8dfc288ab1420cccae
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 2%

---

# [!UICONTROL Champ de préférences de personnalisation générique] type de données

[!UICONTROL Champ de préférences de personnalisation générique] est un type de données XDM standard qui décrit la sélection d’un client pour une préférence de personnalisation spécifique.

>[!NOTE]
>
>Ce type de données est destiné à être utilisé pour personnaliser la structure des schémas de consentement de votre entreprise à l’aide de la variable [[!UICONTROL Consentements et préférences] groupe de champs](../field-groups/profile/consents.md) comme ligne de base.

![](../images/data-types/personalization-field.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `val` | Chaîne | Choix des préférences fournies par le client pour ce cas d’utilisation de la personnalisation. Consultez le tableau ci-dessous pour connaître les valeurs et définitions acceptées. |

{style=&quot;table-layout:auto&quot;}

Le tableau suivant décrit les valeurs acceptées pour `val`:

| Valeur | Titre | Description |
| --- | --- | --- |
| `y` | Oui (inclusion) | Le client a choisi la préférence. En d&#39;autres termes, ils **do** le consentement à l’utilisation de leurs données, comme indiqué par la préférence en question. |
| `n` | Non (opt-out) | Le client s’est désinscrit de la préférence. En d&#39;autres termes, ils **ne pas** le consentement à l’utilisation de leurs données, comme indiqué par la préférence en question. |
| `p` | En attente de vérification | Le système n’a pas encore reçu de valeur de préférence finale. Il est le plus souvent utilisé dans le cadre d’un consentement qui nécessite une vérification en deux étapes. Par exemple, si un client choisit de recevoir des emails, ce consentement est défini sur `p` jusqu’à ce qu’ils sélectionnent un lien dans un courrier électronique pour vérifier qu’ils ont fourni l’adresse électronique correcte, à ce moment-là le consentement est mis à jour pour `y`.<br><br>Si cette préférence n’utilise pas un processus de vérification à deux ensembles, la variable `p` choix peut être utilisé pour indiquer que le client n’a pas encore répondu à l’invite de consentement. Par exemple, vous pouvez définir automatiquement la valeur sur `p` sur la première page d’un site web, avant que le client n’ait répondu à l’invite de consentement. Dans les juridictions qui ne requièrent pas de consentement explicite, vous pouvez également l’utiliser pour indiquer que le client n’a pas explicitement exercé son droit d’opposition (en d’autres termes, le consentement est supposé). |
| `u` | Unknown (Inconnu) | Les informations de préférence du client sont inconnues. |
| `dy` | Par défaut : Oui (inclusion) | Le client n’a pas fourni de valeur de consentement lui-même et est traité comme un accord préalable (&quot;Oui&quot;) par défaut. En d’autres termes, le consentement est supposé jusqu’à ce que le client indique le contraire.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `dn` | Valeur par défaut de Non (opt-out) | Le client n’a pas fourni de valeur de consentement lui-même et est traité comme un droit d’opposition (&quot;Non&quot;) par défaut. En d’autres termes, le client est supposé avoir refusé le consentement jusqu’à ce qu’il en indique autrement.<br><br>Notez que si des lois ou des modifications apportées à la politique de confidentialité de votre entreprise entraînent des modifications des valeurs par défaut de certains utilisateurs ou de tous les utilisateurs, vous devez mettre à jour manuellement tous les profils contenant des valeurs par défaut. |
| `LI` | L&#39;intérêt légitime | L’intérêt commercial légitime de collecter et de traiter ces données à des fins spécifiées l’emporte sur le préjudice potentiel qu’elles peuvent causer à l’individu. |
| `CT` | Contrat | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations contractuelles avec l’individu. |
| `CP` | Respect d’une obligation juridique | La collecte de données aux fins spécifiées est nécessaire pour respecter les obligations légales de l’entreprise. |
| `VI` | Intérêt vital de l’individu | La collecte de données aux fins spécifiées est nécessaire pour protéger les intérêts vitaux de l’individu. |
| `PI` | Intérêt public | La collecte de données aux fins spécifiées est nécessaire pour effectuer une tâche dans l’intérêt public ou dans l’exercice de l’autorité officielle. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
