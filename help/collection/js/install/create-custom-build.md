---
title: Créer une version SDK Web personnalisée à l’aide du package NPM
description: Créez une version de Web SDK personnalisée qui ne contient que les modules dont vous avez besoin.
exl-id: 0ba5ae55-9ec0-41b6-9675-e76ade8ca4cd
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 7%

---

# Création d’une version de Web SDK personnalisée

La bibliothèque Experience Platform Web SDK comprend plusieurs modules pour différentes fonctionnalités telles que la personnalisation, l’identité, le suivi des liens, etc. Selon vos cas d’utilisation, il se peut que vous n’ayez besoin que de fonctionnalités spécifiques au lieu de l’ensemble de la bibliothèque. La création d’une version Web SDK personnalisée vous permet de sélectionner uniquement les modules dont vous avez besoin, ce qui réduit la taille de la bibliothèque et améliore les performances.

## Cas d’utilisation {#use-case}

La création d’une version Web SDK personnalisée permet de réduire la taille de la bibliothèque et d’améliorer les performances. Voici quelques exemples :

### Suppression de Media Analytics {#media-analytics-removal}

Si votre site web ne comporte pas de contenu multimédia, vous pouvez exclure les modules [!DNL Media Analytics] et [!DNL Streaming Media] de la version. Cela peut réduire la taille de la version de Web SDK de jusqu’à 50 % et améliorer la vitesse de chargement.

### Suppression de Personalization {#personalization}

Si vous devez uniquement collecter des mesures d’utilisateur et ne prévoyez pas d’utiliser Adobe Target ou Journey Optimizer pour la personnalisation, vous pouvez exclure le module [!DNL Personalization]. Cela réduit la taille de la bibliothèque tout en vous permettant de collecter les mesures nécessaires.

## Conditions préalables {#prerequisites}

Pour créer une version personnalisée de Web SDK, vous avez besoin du package NPM de Web SDK. Vérifiez que [Node.js](https://nodejs.org/en/download/package-manager/all) est installé sur votre ordinateur. Pour plus d’informations, consultez la documentation sur la [installation du SDK Web à l’aide du package NPM](npm.md).

## Composants et dépendances {#components-dependencies}

Avant de créer une version Web SDK personnalisée, définissez les composants et commandes Web SDK que vous prévoyez d’utiliser. Certaines commandes dépendent de modules spécifiques inclus dans la version.

Le tableau ci-dessous montre la relation entre les modules Web SDK et les commandes qu’ils incluent :

| Dépendance du module | Paramètres de configuration | Commands | Catégorie de taille |
|---------|----------|---------|---------|
| Collecteur d’activités | [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) | S/O | Méthode |
| Audiences | S.O. | S.O. | Petit |
| Contexte | [`context`](../commands/configure/context.md) | S/O | Petit |
| Moteur de règles | `personalizationStorageEnabled` | <ul><li>`evaluateRulesets`</li><li>[`subscribeRulesetItems`](../commands/subscriberulesetitems.md)</li></ul> | Méthode |
| Fusion des événements | S/O | `createEventMergeId` | Petit |
| Bridge Media Analytics | S/O | [`getMediaAnalyticsTracker`](../commands/getmediaanalyticstracker.md) | Grand |
| Personnalisation | <ul><li>[`prehidingStyle`](../commands/configure/prehidingstyle.md)</li><li>[`targetMigrationEnabled`](../commands/configure/targetmigrationenabled.md)</li><li>[`autoCollectPropositionInteractions`](../commands/configure/autocollectpropositioninteractions.md)</li></ul> | S/O | Grand |
| Consentement | [`defaultConsent`](../commands/configure/defaultconsent.md) | [`setConsent`](../commands/setconsent.md) | Petit |
| Streaming Media | [`streamingMedia`](../commands/configure/streamingmedia.md) | <ul><li>[`createMediaSession`](../commands/createmediasession.md)</li><li>[`sendMediaEvent`](../commands/sendmediaevent.md)</li></ul> | Grand |

## Créer une version SDK Web personnalisée à l’aide du package NPM {#create-custom-build}

1. Ouvrez votre terminal et exécutez `npx @adobe/alloy`. Vous êtes invité à sélectionner les composants Web SDK que vous souhaitez que votre version personnalisée inclue.

   ![Image d’un terminal affichant la sélection du module de création personnalisé.](../assets/custom-build/npx.png)

   Utilisez les touches fléchées pour vous déplacer vers le haut et vers le bas dans la liste des modules.

   * Appuyez sur **Espace** pour activer ou désactiver le module sélectionné.
   * Appuyez sur `A` pour activer ou désactiver tous les modules.
   * Appuyez sur `I` pour inverser votre sélection.
   * Appuyez sur `Enter` pour confirmer votre sélection et passez à l’étape suivante.

1. Après avoir sélectionné les modules à inclure dans votre version personnalisée, vous pouvez choisir d’enregistrer une version miniaturisée ou non miniaturisée de votre version personnalisée de bibliothèque Web SDK. Sélectionnez l’option souhaitée et appuyez sur `Enter`.

   ![Image d’un terminal affichant la sélection de minification de version personnalisée.](../assets/custom-build/minify.png)

1. Ensuite, vous êtes invité à indiquer l’emplacement où vous souhaitez enregistrer la version sur votre ordinateur local. Appuyez sur `Enter` pour confirmer l’emplacement présélectionné ou saisissez un nouvel emplacement.

   ![Image d’un terminal affichant l’option d’enregistrement de la version personnalisée.](../assets/custom-build/save.png)

1. Une fois l’emplacement confirmé, votre version personnalisée est générée et enregistrée.

   ![Image d’un terminal affichant l’emplacement enregistré de la version personnalisée.](../assets/custom-build/saved.png)
