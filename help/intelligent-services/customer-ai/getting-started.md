---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Prise en main de l’API client
topic: Getting started
translation-type: tm+mt
source-git-commit: f7c59ef097c00073fbf9f6522b6e70ed24cc8bf1

---


# Prise en main de l’API client

Les guides pour l’IA du client nécessitent une compréhension pratique des différents services de la plateforme impliqués dans l’utilisation de l’IA du client. Avant de vous , veuillez consulter le  suivant :

- [Présentation](../../xdm/home.md)du système du modèle de données d’expérience (XDM) : XDM est la structure de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon , exactement au bon moment. La méthodologie sur laquelle la plateforme d’expérience est créée, XDM System, rend opérationnel le de modèles de données d’expérience pour l’utiliser par les services de la plateforme.
- [Principes de base de la composition](../../xdm/schema/composition.md)de  : Ce présente le du modèle de données d’expérience (XDM) ainsi que les blocs de création, les principes et les bonnes pratiques pour la composition dela plate-forme de données d’expérience à utiliser dans Adobe Experience Platform.
- [](../../xdm/tutorials/create-schema-ui.md)de création : Ce didacticiel décrit les étapes de création d’un  à l’aide de l’éditeur de  de dans la plateforme d’expérience.
- [Présentation](../../rtcdp/overview.md)du client en temps réel : Basée sur Adobe Experience Platform, la plateforme de données clientes en temps réel d’Adobe (CDP en temps réel) aide les à rassembler des données connues et inconnues pour activer les clients par une prise de décision intelligente tout au long du parcours des clients. La plateforme CDP en temps réel associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences client personnalisées et individuelles sur tous les canaux et périphériques.
- [Présentation](../../segmentation/home.md)du service de segmentation : La segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble de  de votre magasin de  de afin de distinguer un groupe de personnes commercialisables de votre base de clients. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différents segments, vous pouvez vous concentrer sur les différentes audiences afin de fournir une expérience marketing plus personnalisée.
- [Guide](../../segmentation/tutorials/create-a-segment.md)de l’utilisateur du créateur de segments : Plateforme vous permet de créer et d’accéder facilement aux segments et d’utiliser différents blocs de création pour caractériser davantage vos segments.

## Téléchargement des scores AI client

>[!NOTE] Si vous n’avez pas besoin de télécharger des scores bruts, ignorez cette étape et passez au guide [de](./user-guide/configure.md)configuration.

Le téléchargement des scores API du client s’effectue par le biais d’une combinaison d’appels d’API. Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md) d’API dans le guide de dépannage de la plateforme d’expérience.

## Étapes suivantes

Une fois que vous avez suivi les étapes décrites dans le  ci-dessus, consultez la documentation [Entrée et Sortie](./input-output.md) . Ce  donne un bref aperçu des types de données utilisés et produits dans l’API du client.