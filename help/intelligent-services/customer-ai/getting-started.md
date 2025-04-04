---
keywords: Experience Platform;prise en main;ia dédiée aux clients;rubriques populaires
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Prise en main de l’IA dédiée aux clients
description: Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des payloads de requête correctement formatées.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 43%

---

# Prise en main de Customer AI

Les guides sur l’IA dédiée aux clients nécessitent une compréhension pratique des différents services Experience Platform impliqués dans l’utilisation de l’IA dédiée aux clients. Avant de commencer, consultez les documents suivants :

- [Présentation du système de modèle de données d’expérience (XDM)](../../xdm/home.md) : XDM est le cadre de base qui permet aux [!DNL Adobe Experience Cloud], optimisés par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. La méthodologie sur laquelle repose Experience Platform, à savoir le système XDM, rend les schémas de modèles de données d’expérience opérationnels pour qu’ils soient utilisés par les services Experience Platform.
- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : ce document présente les schémas XDM ainsi que les blocs de création, principes et bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Adobe Experience Platform].
- [Création de schémas](../../xdm/tutorials/create-schema-ui.md) : ce tutoriel décrit les étapes de la création d’un schéma à l’aide de l’éditeur de schémas dans Experience Platform.
- [Présentation du profil client en temps réel](../../rtcdp/overview.md) : basé sur [!DNL Adobe Experience Platform], Adobe Real-Time Customer Data Platform (Real-Time CDP) aide les entreprises à rassembler des données connues et inconnues pour activer les profils des clients avec une prise de décision intelligente sur l’ensemble du parcours client. Real-Time CDP associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences personnalisées et individuelles aux clients et clientes sur tous les canaux et appareils.
- [Présentation de Segmentation Service](../../segmentation/home.md) : la segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels de votre base de clients. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différents segments, vous pouvez vous concentrer sur les différentes audiences afin de fournir une expérience marketing plus personnalisée.
- [Guide d’utilisation du créateur de segments](../../segmentation/tutorials/create-a-segment.md) : Experience Platform vous permet de créer des segments et d’y accéder facilement, ainsi que d’utiliser différents blocs de création pour caractériser vos segments avec plus de précision.

## Téléchargement des scores de Customer AI

>[!NOTE]
>
>Si vous n’avez pas besoin de télécharger les scores bruts, vous pouvez ignorer cette étape et passer au guide de configuration [](./user-guide/configure.md).

Une combinaison d’appels API est nécessaire pour télécharger les scores de Customer AI. Pour lancer des appels aux API Experience Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

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

## Étapes suivantes

Une fois les étapes décrites dans le document ci-dessus terminées, consultez la documentation [Entrée et Sortie](./data-requirements.md). Ce document donne un bref aperçu des types de données utilisés et générés dans l’IA dédiée aux clients.
