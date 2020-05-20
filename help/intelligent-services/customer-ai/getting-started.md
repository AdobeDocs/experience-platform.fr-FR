---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Prise en main de Customer AI
topic: Getting started
translation-type: tm+mt
source-git-commit: f7c59ef097c00073fbf9f6522b6e70ed24cc8bf1
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 15%

---


# Prise en main de Customer AI

Les guides de l’API client exigent une compréhension pratique des différents services de plate-forme impliqués dans l’utilisation de l’IA client. Avant de début, veuillez consulter les documents suivants :

- [Présentation](../../xdm/home.md)du système du modèle de données d’expérience (XDM) : XDM est le cadre fondamental qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, au bon canal, exactement au bon moment. La méthodologie sur laquelle la plate-forme d’expérience est créée, XDM System, rend opérationnels les schémas de modèles de données d’expérience à utiliser par les services de la plate-forme.
- [Principes de base de la composition](../../xdm/schema/composition.md)des schémas : Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les éléments de base, les principes et les meilleures pratiques de composition de schémas à utiliser dans Adobe Experience Platform.
- [schémas](../../xdm/tutorials/create-schema-ui.md)de construction : Ce didacticiel décrit les étapes de création d’un schéma à l’aide de l’éditeur de Schéma dans la plate-forme d’expérience.
- [Présentation](../../rtcdp/overview.md)du Profil client en temps réel : Basée sur Adobe Experience Platform, la plateforme de données clientes en temps réel d’Adobe (CDP en temps réel) aide les sociétés à rassembler des données connues et inconnues afin d’activer les profils clients avec une prise de décision intelligente tout au long du parcours des clients. La plateforme CDP en temps réel associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences client personnalisées et individuelles sur tous les canaux et périphériques.
- [Présentation](../../segmentation/home.md)du service de segmentation : La segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de personnes commercialisables de votre base de clients. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différents segments, vous pouvez vous concentrer sur les différentes audiences afin de fournir une expérience marketing plus personnalisée.
- [Guide](../../segmentation/tutorials/create-a-segment.md)de l’utilisateur du créateur de segments : La plate-forme vous permet de créer et d’accéder facilement aux segments, ainsi que d’utiliser différents blocs de construction pour caractériser davantage vos segments.

## Téléchargement des scores d’IA client

>[!NOTE] Si vous n’avez pas besoin de télécharger des scores bruts, vous pouvez ignorer cette étape et passer au guide [de](./user-guide/configure.md)configuration.

Le téléchargement des scores d’API client s’effectue par le biais d’une combinaison d’appels d’API. Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md) d’API dans le guide de dépannage d’Experience Platform.

## Étapes suivantes

Une fois que vous avez suivi les étapes décrites dans le document ci-dessus, consultez la documentation [Entrée et Sortie](./input-output.md) . Ce document donne un bref aperçu des types de données utilisés et produits dans l’IA du client.