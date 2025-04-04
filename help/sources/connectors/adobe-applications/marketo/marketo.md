---
keywords: Experience Platform;accueil;rubriques populaires;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Connecteur Marketo Engage
description: Ce document présente le connecteur source Marketo Engage, y compris des informations sur son authentification, son mappage et la latence des données.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 7%

---

# Connecteur [!DNL Marketo Engage]

>[!IMPORTANT]
>
>Vous pouvez désormais utiliser la source [!DNL Marketo Engage] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../landing/multi-cloud.md).

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) est une solution complète pour la gestion des leads et les spécialistes du marketing B2B qui cherchent à transformer les expériences client en s’engageant à chaque étape de parcours d’achat complexes.

Avec le connecteur source [!DNL Marketo Engage], vous pouvez importer les données B2B de [!DNL Marketo Engage] vers Experience Platform et les tenir à jour à l’aide d’applications connectées à Experience Platform.

>[!IMPORTANT]
>
>Vous devez avoir accès à [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) pour utiliser tous les jeux de données Marketo pour la segmentation avec le [profil client en temps réel](../../../../profile/home.md). Sans Real-Time CDP B2B edition, vous pouvez toujours utiliser la source Marketo pour importer les données des jeux de données de personnes et d’activités dans le profil client en temps réel pour la segmentation.

Ce document présente le connecteur source [!DNL Marketo Engage], y compris des informations sur la manière d’authentifier le connecteur, de mapper des champs de [!DNL Marketo Engage] au modèle de données d’expérience (XDM) et sur la latence des données du connecteur.

## Configurer le mappage d’organisation Adobe

Avant de pouvoir établir des jeux de mappages pour [!DNL Marketo Engage], vous devez d’abord configurer le mappage d’organisation d’Adobe. Pour obtenir des instructions détaillées sur la manière d’effectuer cette opération, consultez le guide sur la [configuration du mappage d’organisation d’Adobe pour [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Authentification de votre connecteur [!DNL Marketo Engage]

Pour connecter [!DNL Marketo Engage] à Experience Platform, vous devez d’abord récupérer des valeurs pour vos `munchkinId`, `clientId` et `clientSecret`.

Consultez les étapes décrites dans le document [ Authentifier le connecteur source Marketo ](./marketo-auth.md) pour récupérer vos informations d’identification.

## Configurer l’utilitaire de génération automatique de schémas et d’espaces de noms B2B

Ensuite, utilisez l’utilitaire de génération automatique de schémas et d’espaces de noms B2B pour configurer votre Developer Console Experience Platform et votre environnement Postman. Cela vous permet de renseigner automatiquement vos espaces de noms et schémas B2B. Pour obtenir des instructions détaillées, consultez le guide sur la [configuration de votre utilitaire de génération automatique de schémas et d’espaces de noms B2B](./marketo-namespaces.md)

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes qui vous permettent d’ingérer des données provenant de sources tierces pour les utiliser dans des services Experience Platform en aval.

Le respect des normes XDM permet d’incorporer uniformément les données dans l’écosystème Experience Platform, ce qui facilite la diffusion des données et la collecte d’informations.

Pour en savoir plus sur XDM et son rôle dans Experience Platform, consultez la [présentation du système XDM](../../../../xdm/home.md).

## Mappage des champs de [!DNL Marketo Engage] à XDM

Pour établir une connexion source entre [!DNL Marketo Engage] et Experience Platform, les champs de données sources Marketo doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Experience Platform.

Pour plus d’informations sur les règles de mappage des champs entre les jeux de données [!DNL Marketo Engage] et Experience Platform, consultez les sections suivantes :

* [Activités](../mapping/marketo.md#activities)
* [Programmes](../mapping/marketo.md#programs)
* [Abonnements au programme](../mapping/marketo.md#program-memberships)
* [Sociétés](../mapping/marketo.md#companies)
* [Listes statiques](../mapping/marketo.md#static-lists)
* [Abonnements à des listes statiques](../mapping/marketo.md#static-list-memberships)
* [Comptes désignés](../mapping/marketo.md#named-accounts)
* [Opportunités](../mapping/marketo.md#opportunities)
* [Rôles de contact d’opportunité](../mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../mapping/marketo.md#persons)

## Latence attendue des données [!DNL Marketo Engage] sur Experience Platform

Le tableau suivant décrit la latence attendue pour importer des données [!DNL Marketo Engage] dans Experience Platform, en fonction de la nature de l’ingestion et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minutes |
| Lac de données | &lt; 60 minutes |

>[!NOTE]
>
>Les chiffres de latence ci-dessus représentent les attentes à un niveau de confiance de 95 %. Les latences réelles varieront et peuvent aller au-delà de ces chiffres de 50 % dans de rares cas.

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d’une connexion source [!DNL Marketo Engage] :

* Pour plus d’informations sur la connexion de vos données [!DNL Marketo Engage] à Experience Platform, consultez le tutoriel sur la [création d’une connexion source dans l [!DNL Marketo Engage] interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Pour plus d’informations sur la configuration de vos schémas et l’ingestion de données d’activité personnalisées, consultez le tutoriel sur [la création d’une connexion source et d’un flux de données pour les données  [!DNL Marketo Engage] ’activité personnalisées](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Pour plus d’informations sur la migration de votre mappage ECID du jeu de données [!DNL Person] vers le jeu de données [!DNL Activity], consultez le [guide de migration du mappage ECID](./migration.md).
* Pour plus d’informations sur la configuration sous-jacente des espaces de noms et des schémas B2B utilisés avec [!DNL Marketo Engage], consultez la documentation relative aux espaces de noms et aux schémas [B2B](./marketo-namespaces.md).
* Pour plus d’informations sur la recherche de votre identifiant munchkin [!DNL Marketo Engage] et la génération de vos informations d’identification, consultez le guide d’authentification [[!DNL Marketo Engage] ](./marketo-auth.md).
* Pour plus d’informations sur les règles de mappage spécifiques qui s’appliquent aux jeux de données [!DNL Marketo Engage], consultez la documentation sur les [[!DNL Marketo Engage] mappages de champs](../mapping/marketo.md).
* Pour obtenir des informations générales sur [!DNL Real-Time Customer Data Platform B2B Edition] et ses fonctionnalités, consultez la documentation sur [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
