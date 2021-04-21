---
keywords: Experience Platform ; prise en main ; assistance client ; rubriques populaires
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Prise en main dans l’API client
topic-legacy: Getting started
description: Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 75%

---

# Prise en main de Customer AI

Les guides sur Customer AI nécessitent une compréhension pratique des différents services Platform impliqués dans l’utilisation de Customer AI. Avant de commencer, consultez les documents suivants :

- [Présentation](../../xdm/home.md) du système du modèle de données d’expérience (XDM) : XDM est le cadre fondateur qui permet  [!DNL Adobe Experience Cloud], propulsé par un Experience Platform, de transmettre le bon message à la bonne personne, au bon canal, exactement au bon moment. La méthodologie sur laquelle Experience Platform repose, à savoir le système XDM, rend les schémas de modèles de données d’expérience opérationnels pour qu’ils soient utilisés par les services de Platform.
- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : ce document présente les schémas XDM ainsi que les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Adobe Experience Platform].
- [Création de schémas](../../xdm/tutorials/create-schema-ui.md) : ce tutoriel décrit les étapes de la création d’un schéma à l’aide de l’éditeur de schémas dans Experience Platform.
- [Présentation](../../rtcdp/overview.md) du Profil client en temps réel : La plate-forme de données clientes en temps réel (CDP en temps réel)  [!DNL Adobe Experience Platform]intégrée permet aux sociétés de rassembler des données connues et inconnues pour activer les profils clients grâce à une prise de décision intelligente sur l’ensemble du parcours client. La plateforme de données clients en temps réel associe plusieurs sources de données d’entreprise pour créer des profils unifiés en temps réel qui peuvent être utilisés pour offrir des expériences client personnalisées et individuelles sur tous les canaux et périphériques.
- [Présentation de Segmentation Service](../../segmentation/home.md) : la segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différents segments, vous pouvez vous concentrer sur les différentes audiences afin de fournir une expérience marketing plus personnalisée.
- [Guide d’utilisation du créateur de segments](../../segmentation/tutorials/create-a-segment.md) : Platform vous permet de créer des segments et d’y accéder en toute facilité, ainsi que d’utiliser différents blocs de création pour caractériser vos segments avec plus de précision.

## Téléchargement des scores de Customer AI

>[!NOTE]
>
>Si vous n&#39;avez pas besoin de télécharger des scores bruts, vous pouvez ignorer cette étape et passer au [guide de configuration](./user-guide/configure.md).

Une combinaison d’appels API est nécessaire pour télécharger les scores de Customer AI. Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Dans Experience Platform, toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans Platform, consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes

Une fois que vous avez suivi les étapes décrites dans le document ci-dessus, consultez la documentation [Entrée et sortie](./input-output.md). Ce document donne un bref aperçu des types de données utilisés et produits dans l’IA du client.
