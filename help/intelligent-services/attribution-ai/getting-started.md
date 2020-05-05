---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Prise en main dans l’API d’attribution
topic: Getting started
translation-type: tm+mt
source-git-commit: 6161f5a9ca0df341272a96a8a19ce6c34f6d5d3e

---


# Prise en main dans l’API d’attribution

Les guides ci-dessous vous permettent de comprendre les différents services Adobe Experience Platform impliqués dans l’utilisation de l’API d’attribution. Avant de commencer les didacticiels, veuillez consulter les documents suivants :

- [Présentation](../../xdm/home.md)du système du modèle de données d’expérience (XDM) : XDM est le cadre fondamental qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, au bon canal, exactement au bon moment. La méthodologie sur laquelle la plate-forme d’expérience est créée, XDM System, rend opérationnels les schémas de modèles de données d’expérience à utiliser par les services de la plate-forme.
- [Principes de base de la composition](../../xdm/schema/composition.md)des schémas : Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les éléments de base, les principes et les meilleures pratiques de composition de schémas à utiliser dans Adobe Experience Platform.
- [schémas](../../xdm/tutorials/create-schema-ui.md)de construction : Ce didacticiel décrit les étapes de création d’un schéma à l’aide de l’éditeur de Schéma dans la plate-forme d’expérience.

Attribution AI nécessite que les jeux de données soient conformes au schéma CEE (Consumer Experience Événements), qui est un mélange dans le modèle [de données d’](../../xdm/home.md) expérience (XDM). Contactez l’assistance d’Adobe à l’adresse attributionai-support@adobe.com pour mettre en oeuvre ces données ou apporter des modifications à celles-ci. Si des données de dépenses des médias sont présentes, vous pouvez effectuer d’autres analyses, telles que les recettes incrémentielles et le RSI. Si les données du profil client sont disponibles, vous pouvez en outre attribuer des crédits au niveau du profil client.

## Terminologie

- **événement de conversion :** Tout événement numérique ou interaction numérique que les clients effectuent pour indiquer un jalon vers un objectif, tel que l’inscription à une conférence. Les autres exemples incluent les conversions payantes, les abonnements au compte gratuit ou les qualifications pour une caractéristique.

- **Point de contact :** Tout événement numérique ou interaction numérique que les clients effectuent sur le chemin d’un objectif. Les exemples incluent les actions marketing liées aux achats précédents, les impressions publicitaires affichées et les clics de recherche payante.

## Téléchargement de scores d’API d’attribution

>[!NOTE] Si vous n’avez pas besoin de télécharger des scores bruts, vous pouvez ignorer cette étape et passer aux étapes [](#next-steps)suivantes.

Le téléchargement des scores d’API d’attribution se fait par le biais d’une combinaison d’appels d’API. Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md) d’API dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Une fois que vous êtes prêt et que vos informations d’identification et vos schémas sont en place, début en suivant le guide [de l’interface utilisateur](./user-guide.md)Attribution AI. Ce guide vous guide tout au long des étapes nécessaires pour créer une instance et l’envoyer pour formation et score.