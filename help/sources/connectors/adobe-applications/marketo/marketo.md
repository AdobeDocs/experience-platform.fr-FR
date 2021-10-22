---
keywords: Experience Platform ; accueil ; sujets populaires ; Marketo Engage ; marketing à engager ; marketing
solution: Experience Platform
title: Connecteur Marketo Engage
topic-legacy: overview
description: Ce document fournit une vue d’ensemble du connecteur source Marketo Engage, y compris des informations sur son authentification, son mappage et sa latence de données.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: a36a4775c14e97df51f218cea3a083d29c7b69dc
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 13%

---

# (Bêta) [!DNL Marketo Engage] connecteur

>[!IMPORTANT]
>
>Le [!DNL Marketo Engage] source dans Adobe Experience Platform est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (ci-après dénommés &quot;[!DNL Marketo]&quot;) est une solution complète pour la gestion des prospects et les spécialistes du marketing B2B qui cherchent à transformer l&#39;expérience client en s&#39;engageant à travers toutes les étapes de parcours d&#39;achat complexes.

Avec la [!DNL Marketo] connecteur source, vous pouvez importer des données B2B à partir de [!DNL Marketo] sur Plate-forme et tenir ces données à jour à l’aide d’applications connectées à la plate-forme.

Ce document fournit un aperçu de la [!DNL Marketo] connecteur source, y compris des informations sur l&#39;authentification du connecteur, comment mapper [!DNL Marketo] vers Experience Data Model (XDM) et la latence des données du connecteur.

## Authentifiez votre [!DNL Marketo] connecteur

Pour connecter [!DNL Marketo] sur Plate-forme, vous devez d’abord récupérer des valeurs pour votre `munchkinId`, `clientId`et `clientSecret`.

Reportez-vous aux étapes décrites dans la section [Authentifiez votre connecteur source Marketo.](./marketo-auth.md) pour récupérer vos informations d’identification.

## Configuration du partage d&#39;audience Adobe Experience Cloud

Avant d’établir des jeux de mappages pour [!DNL Marketo], vous devez d’abord configurer le partage d’audience Adobe Experience Cloud. Pour connaître les étapes détaillées à suivre, consultez le guide [configuration du partage d&#39;audience Adobe Experience Cloud pour [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-experience-cloud-audience-sharing.html?lang=en).

## Modèle de données d’expérience (XDM)

XDM est une spécification publiquement documentée qui fournit des structures et des définitions communes qui vous permettent d’assimiler des données de sources tierces pour les utiliser dans les services de plate-forme en aval.

Le respect des normes XDM permet d&#39;intégrer uniformément les données dans l&#39;écosystème de la plate-forme, ce qui facilite la transmission des données et la collecte des informations.

Pour en savoir plus sur XDM et son rôle dans la plate-forme, consultez la section [Présentation du système XDM](../../../../xdm/home.md).

## Mappage de champs depuis [!DNL Marketo] vers XDM

Pour établir une connexion source entre [!DNL Marketo] et Platform, les champs de données source Marketo doivent être mappés à leurs champs XDM cibles appropriés avant d’être assimilés à Platform.

Pour plus d’informations sur les règles de mappage de champs entre [!DNL Marketo] ensembles de données et plate-forme :

* [Activités](../mapping/marketo.md#activities)
* [Programmes](../mapping/marketo.md#programs)
* [Abonnements au programme](../mapping/marketo.md#program-memberships)
* [Sociétés](../mapping/marketo.md#companies)
* [Listes statiques](../mapping/marketo.md#static-lists)
* [Abonnements à une liste statique](../mapping/marketo.md#static-list-memberships)
* [Comptes nommés](../mapping/marketo.md#named-accounts)
* [Opportunités](../mapping/marketo.md#opportunities)
* [Rôles de contact d’opportunité](../mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../mapping/marketo.md#persons)

## Latence attendue de [!DNL Marketo] données sur la plate-forme

Le tableau suivant décrit la latence prévue pour l’importation [!DNL Marketo] données dans la plate-forme, en fonction de la nature de l&#39;ingestion et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d’un fichier [!DNL Marketo] connexion source :

* Pour plus d’informations sur la connexion de votre [!DNL Marketo] données vers la plate-forme, consultez le tutoriel sur [création d&#39;un connecteur source Marketo dans l&#39;interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Pour plus d&#39;informations sur la configuration sous-jacente des espaces de noms et schémas B2B utilisés avec [!DNL Marketo], consultez la documentation pour [Espaces de noms et schémas B2B](./marketo-namespaces.md).
* Pour plus d’informations sur la recherche de [!DNL Marketo] munchkin ID et génération de vos informations d’identification, consultez la section [[!DNL Marketo] guide d’authentification](./marketo-auth.md).
* Pour plus d’informations sur les règles de mappage spécifiques qui s’appliquent à [!DNL Marketo] ensembles de données, voir la documentation sur [[!DNL Marketo] mappages de champs](../mapping/marketo.md).
* Pour des informations générales sur [!DNL Real-time Customer Data Platform B2B Edition] et ses fonctionnalités, voir la documentation sur [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
