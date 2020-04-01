---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Prise en main dans Attribution AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Prise en main dans Attribution AI

Les guides ci-dessous vous permettent de comprendre les différents services Adobe Experience Platform impliqués dans l’utilisation de l’API d’attribution. Avant de commencer les didacticiels, veuillez consulter le  de suivant :

- [Présentation](../../xdm/home.md)du système du modèle de données d’expérience (XDM) : XDM est la structure de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon , exactement au bon moment. La méthodologie sur laquelle la plateforme d’expérience est créée, XDM System, rend opérationnel le de modèles de données d’expérience pour l’utiliser par les services de la plateforme.
- [Principes de base de la composition](../../xdm/schema/composition.md)de  : Ce présente le du modèle de données d’expérience (XDM) ainsi que les blocs de création, les principes et les bonnes pratiques pour la composition dela plate-forme de données d’expérience à utiliser dans Adobe Experience Platform.
- [](../../xdm/tutorials/create-schema-ui.md)de création : Ce didacticiel décrit les étapes de création d’un  à l’aide de l’éditeur de  de dans la plateforme d’expérience.

L’attribut AI exige que les jeux de données soient conformes au CEE (Consumer Experience ), qui est un mixin dans le modèle [de données d’](../../xdm/home.md) expérience (XDM). Veuillez contacter l’assistance technique d’Adobe à l’adresse attributionai-support@adobe.com pour mettre en oeuvre ces données ou apporter des modifications à celles-ci. Si des données de dépense multimédia sont présentes, vous pouvez effectuer d’autres  , telles que les recettes incrémentielles et le RSI. Si les données de  du client sont disponibles, vous pouvez attribuer davantage de crédits au niveau de l’du client.

## Terminologie

- **de conversion :** Tout numérique ou interaction numérique que les clients font pour indiquer un jalon vers un objectif, tel que les inscriptions aux conférences. Les autres exemples incluent les conversions payantes, les abonnements au compte gratuit ou les qualifications pour une caractéristique.

- **Point de contact :** Tout numérique ou interaction numérique que les clients font sur la voie d’un objectif. Par exemple, les actions marketing liées aux achats précédents, les impressions publicitaires affichées et les clics sur les recherches payantes.

## Accès et interrogation de scores

>[!NOTE] Si vous n’avez pas besoin de  ou d’accéder à des scores bruts, vous pouvez ignorer cette étape et passer au guide [de l’interface](./user-guide.md)utilisateur.

L’accès et l’interrogation des scores pour Attribution AI se font par Snowflake. Pour l’instant, vous devez envoyer un courrier électronique à l’assistance d’Adobe à l’adresse attributionai-support@adobe.com afin de configurer et de recevoir les informations d’identification de votre compte Reader pour Snowflake ou d’exporter en masse des données brutes.

Une fois votre demande traitée par le service d’assistance d’Adobe, vous recevez l’URL du compte Reader pour Snowflake et les informations d’identification correspondantes ci-dessous :

- URL de Snowflake
- Nom d’utilisateur
- Mot de passe

## Étapes suivantes

Une fois que vous êtes prêt et que vos informations d’identification et vos  sont en place,  en suivant le guide [de l’interface utilisateur](./user-guide.md)d’Attribution AI. Ce guide vous guide tout au long de la création d’une instance et de son envoi pour formation et score.