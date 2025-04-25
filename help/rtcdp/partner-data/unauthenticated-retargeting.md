---
title: Reciblage côté serveur non authentifié
description: Découvrez comment recibler des utilisateurs non authentifiés à l’aide d’ECID
feature: Use Cases, Customer Acquisition
exl-id: 008f4534-29e7-49b9-b0be-9e0c3962ee21
source-git-commit: ba2154e84f24ddf4ec270121bdcbb6dd5d3dff42
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Reciblage côté serveur non authentifié {#unauthenticated-retargeting}

À mesure que les cookies tiers perdent de leur efficacité, les entreprises passent à des solutions sans cookies pour un engagement personnalisé et un reciblage. Le reciblage hors site permet aux entreprises d’atteindre des utilisateurs et utilisatrices à forte intention en fonction de leurs interactions précédentes, sans dépendre de JavaScript côté client.

## Pourquoi recibler les visiteurs non authentifiés ? {#why-use-case}

En intégrant Adobe Experience Platform Web SDK et le transfert d’événement côté serveur, vous pouvez rationaliser la diffusion d’événement et le transfert de données. Cela permet un reciblage transparent des utilisateurs non authentifiés à l’aide d’ECID (Experience Cloud ID), assurant ainsi un engagement cohérent sur toutes les plateformes. Avec cette solution, vous pouvez augmenter les opportunités de conversion en reciblant efficacement les utilisateurs non authentifiés en fonction de leurs interactions passées.

## Prérequis et planification {#prerequisites-and-planning}

Avant de poursuivre le déploiement de Web SDK et de la configuration de transfert d’événement, vérifiez les points suivants :

1. **Adobe avec configuration de Web SDK** : Adobe Web SDK doit être mis en œuvre pour faciliter la collecte d’événements et le transfert de données.

2. **Configuration d’Adobe Experience Platform Edge Network** : assurez-vous qu’Edge Network est configuré pour prendre en charge le transfert d’événement en temps réel pour le reciblage hors site.

3. **Synchronisation des ECID** : assurez-vous que les ECID sont synchronisés sur toutes les plateformes pour permettre une correspondance d’audience transparente.

## Réalisation du reciblage hors site {#achieve-offsite-retargeting}

1. **Déployer Web SDK** : mettez en œuvre le SDK Web Adobe sur votre site Web pour capturer les données d’événement en temps réel, y compris les interactions utilisateur telles que les pages vues, les clics et d’autres comportements.

2. **Activer le transfert d’événement** : configurez le transfert d’événement dans Platform pour envoyer les données utilisateur collectées, en garantissant un transfert de données efficace pour l’activation de l’audience.

3. **Configurer l’activation côté serveur** : utilisez les fonctionnalités côté serveur d’Adobe pour activer les audiences de reciblage en fonction des ECID, afin de garantir un ciblage précis des audiences sur l’ensemble des plateformes.

4. **Créer des audiences reciblées** : utilisez les outils de segmentation d’audience de Platform pour définir des audiences ciblées en fonction du comportement de l’utilisateur, tel que les vues, les interactions ou les paniers abandonnés.

5. **Activer les audiences** : une fois vos audiences reciblées créées, activez-les pour diffuser du contenu personnalisé, en vous assurant que les utilisateurs sont à nouveau engagés en fonction de leurs interactions précédentes avec votre site.

## Créer une audience à l’aide de l’attribut calculé {#create-audience}

Pour recibler efficacement les utilisateurs à forte intention, créez des audiences en fonction de leurs interactions antérieures avec votre site web. Utilisez Platform pour segmenter les utilisateurs à l’aide d’attributs calculés.

1. **Identifier les comportements clés** : sélectionnez les actions des utilisateurs à suivre, telles que les pages vues ou les clics.

2. **Créer des audiences** : utilisez les outils de segmentation d’audience pour regrouper les utilisateurs en fonction de leurs comportements.

3. **Synchroniser l’ECID** : assurez-vous que les ECID sont synchronisés sur les plateformes pour une correspondance d’audience précise.

## Activer votre audience {#activate-audience}

Une fois que vous avez créé votre audience, activez-la sur plusieurs plateformes pour interagir avec les utilisateurs.

1. **Vérifier les audiences** : assurez-vous que les segments d’audience reflètent les comportements appropriés.

2. **Créer des règles d’activation** : définissez des conditions pour savoir quand et comment les utilisateurs sont engagés en fonction des actions.

3. **Push to Platform** : activez l’audience.

4. **Surveillance des performances** : suivez les performances des audiences et apportez les modifications nécessaires.

## Configuration de l’extension de reciblage hors site {#configure-extension}

### Déploiement de Web SDK

Assurez-vous que le SDK Web Adobe est correctement intégré à votre site web. Ce SDK permet la collecte de données d’événement en temps réel, ce qui est essentiel pour un reciblage efficace.

### Activation du transfert dʼévénements

Configurez un transfert d’événement dans Platform pour envoyer les données de comportement utilisateur collectées aux plateformes de reciblage. Le transfert d’événement garantit que les données sont transmises efficacement, ce qui permet aux entreprises de cibler les utilisateurs et utilisatrices à forte intention sans recourir aux cookies.

### Joindre à la règle de reciblage

Assurez-vous que l’extension de reciblage hors site est associée à une règle d’événement valide dans la collecte de données Adobe Experience Platform. En règle générale, une règle globale doit être créée pour se déclencher sur des actions clés, telles que des `page load` ou des interactions utilisateur spécifiques.

Pour en savoir plus sur la configuration de l’extension, consultez la documentation [Transfert d’événement](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started).

## Autres cas d’utilisation {#other-use-cases}

Ce document présente les principaux cas d’utilisation et les considérations techniques pour réussir le développement et l’utilisation de la configuration du SDK web et du transfert d’événement. En suivant les procédures décrites et en vous assurant que les conditions préalables nécessaires sont remplies, vous pouvez améliorer considérablement leurs fonctionnalités de suivi et d’analyse des données.

Vous pouvez explorer d’autres cas d’utilisation activés par le biais de la prise en charge des données des partenaires dans Real-Time CDP :

- [Interagissez et acquérez de nouveaux clients](./prospecting.md) en utilisant les données des partenaires.
- [Personnaliser les expériences sur site](./offsite-retargeting.md) avec reconnaissance des visiteurs assistée par des partenaires.
- [Complétez les profils propriétaires](./supplement-first-party-profiles.md) avec les attributs fournis par le partenaire.
