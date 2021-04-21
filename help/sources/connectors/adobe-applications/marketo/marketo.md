---
keywords: Experience Platform ; accueil ; rubriques populaires ; Marketo Engage ; marketing à engager ; marketing
solution: Experience Platform
title: Connecteur Marketo Engage
topic-legacy: overview
description: Ce document présente un aperçu du connecteur source du Marketo Engage, y compris des informations sur son authentification, son mappage et sa latence des données.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 13%

---


# (Bêta) [!DNL Marketo Engage] connecteur

>[!IMPORTANT]
>
>La source [!DNL Marketo Engage] est actuellement en version bêta. Ses fonctionnalités et la documentation peuvent être modifiées.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (ci-après dénommés &quot;[!DNL Marketo]&quot;) est une solution complète pour la gestion des pistes et les spécialistes du marketing B2B qui cherchent à transformer l&#39;expérience client en intervenant à toutes les étapes de parcours d&#39;achat complexes.

Avec le connecteur source [!DNL Marketo], vous pouvez importer les données B2B de [!DNL Marketo] vers la plate-forme et les mettre à jour à l&#39;aide d&#39;applications connectées à la plate-forme.

Ce document fournit un aperçu du connecteur source [!DNL Marketo], y compris des informations sur la manière d&#39;authentifier le connecteur, de mapper les champs [!DNL Marketo] au modèle de données d&#39;expérience (XDM) et la latence des données du connecteur.

## Authentifier votre connecteur [!DNL Marketo]

Pour connecter [!DNL Marketo] à la plate-forme, vous devez d&#39;abord récupérer les valeurs de `munchkinId`, `clientId` et `clientSecret`.

Reportez-vous aux étapes décrites dans le document [Authentifier votre connecteur source Marketo](./marketo-auth.md) pour récupérer vos informations d’identification.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions communes qui vous permettent d’assimiler des données de sources tierces pour les utiliser dans les services Plateforme en aval.

Le respect des normes XDM permet d&#39;intégrer uniformément les données dans l&#39;écosystème de la Plateforme, ce qui facilite la transmission des données et la collecte des informations.

Pour en savoir plus sur XDM et son rôle dans Plateforme, consultez l&#39;[Présentation du système XDM](../../../../xdm/home.md).

## Mappage des champs de [!DNL Marketo] à XDM

Pour établir une connexion source entre [!DNL Marketo] et la plate-forme, les champs de données source Marketo doivent être mappés à leurs champs XDM de cible appropriés avant d&#39;être assimilés à Platform.

Pour plus d&#39;informations sur les règles de mappage des champs entre les jeux de données [!DNL Marketo] et la plate-forme, reportez-vous aux sections suivantes :

* [Activités](../mapping/marketo.md#activities)
* [Programmes](../mapping/marketo.md#programs)
* [adhésions au programme](../mapping/marketo.md#program-memberships)
* [Sociétés](../mapping/marketo.md#companies)
* [Listes statiques](../mapping/marketo.md#static-lists)
* [Abonnements à la liste statique](../mapping/marketo.md#static-list-memberships)
* [Comptes nommés](../mapping/marketo.md#named-accounts)
* [Opportunités](../mapping/marketo.md#opportunities)
* [Rôles de contact d&#39;opportunité](../mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../mapping/marketo.md#persons)

## Latence attendue des données [!DNL Marketo] sur la plateforme

Le tableau suivant décrit la latence attendue pour l&#39;introduction de [!DNL Marketo] données dans la plate-forme, en fonction de la nature de l&#39;assimilation et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d&#39;une connexion source [!DNL Marketo] :

* Pour plus d&#39;informations sur la connexion de vos données [!DNL Marketo] à la plate-forme, consultez le didacticiel sur la création d&#39;un connecteur source Marketo dans l&#39;interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).[
* Pour plus d&#39;informations sur la configuration sous-jacente des espaces de nommage et schémas B2B utilisés avec [!DNL Marketo], consultez la documentation relative aux [espaces de nommage et schémas B2B](./marketo-namespaces.md).
* Pour plus d&#39;informations sur la recherche de votre [!DNL Marketo] ID de munchkin et la génération de vos informations d&#39;identification, consultez le [[!DNL Marketo] guide d&#39;authentification](./marketo-auth.md).
* Pour plus d&#39;informations sur les règles de mappage spécifiques qui s&#39;appliquent aux jeux de données [!DNL Marketo], consultez la documentation sur les [[!DNL Marketo] mappages de champs](../mapping/marketo.md).