---
keywords: Experience Platform;prise en main;ia dédiée à l’attribution;rubriques populaires
feature: Attribution AI
title: Prise en main dans l’IA dédiée à l’attribution
description: Les guides ci-dessous nécessitent une compréhension des différents services impliqués dans l’utilisation d’Attribution AI. Avant de commencer les tutoriels, veuillez consulter les documents suivants.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 57%

---

# Prise en main d’Attribution AI

Les guides suivants nécessitent une compréhension des différents services de [!DNL Adobe Experience Platform] impliqués dans l’utilisation d’Attribution AI. Avant de commencer les tutoriels, veuillez consulter les documents suivants :

- [Présentation du système de modèle de données d’expérience (XDM)](../../xdm/home.md) : XDM est le cadre de base qui permet aux [!DNL Adobe Experience Cloud], optimisés par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. La méthodologie sur laquelle repose Experience Platform, à savoir le système XDM, rend les schémas de modèles de données d’expérience opérationnels pour qu’ils soient utilisés par les services Experience Platform.
- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : ce document présente les schémas XDM ainsi que les blocs de création, principes et bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Adobe Experience Platform].
- [Création de schémas](../../xdm/tutorials/create-schema-ui.md) : ce tutoriel décrit les étapes de la création d’un schéma à l’aide de l’éditeur de schémas dans Experience Platform.

L’IA dédiée à l’attribution nécessite que les jeux de données soient conformes au schéma CEE (Consumer Experience Events), qui est un groupe de champs de schéma [ Modèle de données d’expérience (XDM)](../../xdm/home.md). Veuillez contacter l’assistance d’Adobe à l’adresse attributionai-support@adobe.com pour mettre en œuvre ou apporter des modifications à ces données. Si des données de dépenses médias sont présentes, vous pouvez effectuer une analyse supplémentaire par exemple du chiffre d’affaires incrémentiel et du retour sur investissement. Si des données de profil client sont disponibles, vous pouvez attribuer davantage de crédits au niveau de profil du client.

## Terminologie

- **Événement de conversion :** tout événement ou toute interaction digitale que les clients effectuent pour indiquer un jalon vers un objectif, par exemple dans le cadre d’inscriptions à une réunion. D’autres exemples incluent les conversions payantes, les créations gratuites de comptes ou l’éligibilité à une caractéristique.

- **Point de contact :** tout événement ou toute interaction numérique effectuée pour atteindre un objectif. Cela inclut par exemple les efforts marketing précédant un achat, les impressions de publicité display vues et les clics de référencement payant.

## Téléchargement des scores de l’IA dédiée à l’attribution

>[!NOTE]
>
>Si vous n’avez pas besoin de télécharger les scores bruts, vous pouvez ignorer cette étape et passer aux [étapes suivantes](#next-steps).

Le téléchargement des scores de l’IA dédiée à l’attribution est effectué par le biais d’une combinaison d’appels API. Pour lancer des appels aux API Experience Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Dans Experience Platform, toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API Experience Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Contrôle d’accès {#access-control}

Lors de l’utilisation du contrôle d’accès basé sur les rôles, les privilèges **Afficher l’IA dédiée à l’attribution** et **Gérer l’IA dédiée à l’attribution** accordent l’accès à différentes fonctionnalités de l’IA dédiée à l’attribution. L’**Gérer l’IA dédiée à l’attribution** vous permet de **créer**, **cloner**, **modifier**, **supprimer**, **activer** ou **désactiver** une instance tandis que **Afficher l’IA dédiée à l’attribution** vous permet de **lire** ou **afficher**. Les actions **créer**, **modifier** et **supprimer** sont enregistrées par les journaux d’audit.

Consultez la documentation pour apprendre à [attribuer des autorisations pour le contrôle d’accès](../../../help/access-control/home.md) ou comment [utiliser les journaux d’audit pour surveiller l’accès et l’activité](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Étapes suivantes {#next-steps}

Lorsque vous êtes prêt et que l’ensemble de vos informations d’identification et schémas sont en place, commencez par suivre le [guide de l’interface utilisateur d’Attribution AI](./user-guide.md). Ce guide vous accompagne dans la création d’une instance et son envoi pour formation et notation.
