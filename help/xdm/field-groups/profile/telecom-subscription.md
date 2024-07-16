---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schémas;télécommunications;abonnement;télécommunications;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma d’abonnement aux télécommunications
description: Découvrez le groupe de champs Schéma d'abonnement aux télécommunications .
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 8%

---

# Groupe de champs de schéma [!UICONTROL Inscription aux télécommunications]

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Inscription aux télécommunications] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) qui décrit le plan d’abonnement d’un client à des services de télécommunication, y compris les tarifs, les packages et les abonnements à des produits individuels.

Le groupe de champs fournit un champ de type objet unique, `telecomSubscription`, dont les propriétés sont décrites ci-dessous.

![Structure d&#39;abonnement aux télécoms](../../images/field-groups/telecom-subscription/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `internetSubscription` | Tableau d’objets | Décrit les détails du plan d’abonnement Internet, tels que la limite de données, le type de connexion et les détails de vitesse. Pour plus d’informations, consultez la [section ci-dessous](#internetSubscription) . |
| `landlineSubscription` | Tableau d’objets | Décrit les détails du plan d’abonnement fixe, y compris les fonctionnalités, les minutes et les plans de numérotation sélectionnés. Pour plus d’informations, consultez la [section ci-dessous](#landlineSubscription) . |
| `mediaSubscription` | Tableau d’objets | Décrit les détails du plan d’abonnement au média, y compris le nombre de canaux et les services de diffusion en continu inclus. Pour plus d’informations, consultez la [section ci-dessous](#mediaSubscription) . |
| `mobileSubscription` | Tableau d’objets | Décrit les détails du plan d’abonnement mobile, notamment le nombre de lignes, les taux de données, le coût, etc. Pour plus d’informations, consultez la [section ci-dessous](#mobileSubscription) . |
| `primarySubscriber` | [[!UICONTROL Personne]](../../data-types/person.md) | Décrit le propriétaire de l’abonnement. |
| `bundleName` | Chaîne | Capture le nom de tout type de bundle d’abonnement dans lequel le client est inscrit, par exemple `Internet + Media`. |
| `primaryPartyID` | Chaîne | Identifiant de la personne principale responsable de l’abonnement, qui peut généralement être son numéro de téléphone d’appareil. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Abonnement aux télécommunications]](../../data-types/telecom-subscription.md) | Décrit les détails généraux de l’abonnement, notamment la durée de l’abonnement, les frais, l’état, etc. Décrit les détails généraux de l’abonnement, notamment la durée de l’abonnement, les frais, l’état, etc. |
| `connectionType` | Chaîne | Type de connexion de l’abonnement. |
| `dataCap` | Nombre entier | Limite de la limite de données pour le compte, en mégaoctets (Mo). |
| `downloadSpeed` | Nombre entier | Vitesse de téléchargement maximale disponible pour l’abonnement, en mégaoctets (Mo). |
| `selfSetup` | Booléen | Indique si un client est éligible à la configuration Internet sans visite d’un technicien. |
| `uploadSpeed` | Nombre entier | Vitesse de chargement maximale disponible pour l’abonnement, en mégaoctets (Mo). |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Numéro de téléphone]](../../data-types/telecom-subscription.md) | Numéro de téléphone attribué à cet abonnement. |
| `subscriptionDetails` | [[!UICONTROL Abonnement aux télécommunications]](../../data-types/telecom-subscription.md) | Décrit les détails généraux de l’abonnement, notamment la durée de l’abonnement, les frais, l’état, etc. |
| `callBlocking` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent le blocage des appels. |
| `callForwarding` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent le transfert d’appel. |
| `callWaiting` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent l’attente d’appel. |
| `callerID` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent un ID d’appelant. |
| `internationalCalling` | Booléen | Indique si les fonctions d&#39;abonnement aux lignes fixes incluent des appels internationaux. |
| `minutes` | Nombre entier | Nombre de minutes mensuelles disponibles dans l’abonnement. |
| `threeWayCalling` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent des appels tridirectionnels. |
| `unlimitedDomesticLongDistance` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent un nombre illimité d’appels interurbains nationaux. |
| `unlimitedLocalCalling` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent un nombre illimité d’appels locaux. |
| `voicemail` | Booléen | Indique si les fonctionnalités d’abonnement fixe incluent la messagerie vocale. |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `streamingServices` | Tableau d’objets | Liste de tous les services de diffusion en continu inclus dans l’abonnement. Chaque élément de tableau comprend les propriétés suivantes : <ul><li>`promotionLength` : durée de la promotion, en mois, si le service de diffusion en continu a été ajouté dans le cadre d’une promotion.</li><li>`promotionalAddition` : indique si le service de diffusion en continu a été ajouté dans le cadre d’une promotion.</li><li>`serviceName` : nom du service de diffusion en continu.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Abonnement aux télécommunications]](../../data-types/telecom-subscription.md) | Décrit les détails généraux de l’abonnement, notamment la durée de l’abonnement, les frais, l’état, etc. |
| `channels` | Nombre entier | Nombre de canaux inclus dans l’abonnement au média. |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Numéro de téléphone]](../../data-types/telecom-subscription.md) | Numéro de téléphone attribué à cet abonnement. |
| `subscriptionDetails` | [[!UICONTROL Abonnement aux télécommunications]](../../data-types/telecom-subscription.md) | Décrit les détails généraux de l’abonnement, notamment la durée de l’abonnement, les frais, l’état, etc. |
| `earlyUpgradeEnrollment` | Booléen | Indique si le client s’inscrit aux mises à niveau anticipées. |
| `planLevel` | Chaîne | Nom du plan mobile affecté à cet abonnement. |
| `portedNumber` | Booléen | Indique si le client porte son numéro depuis un autre opérateur. |

{style="table-layout:auto"}
