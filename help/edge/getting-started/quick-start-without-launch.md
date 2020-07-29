---
title: début rapide à l’aide de JavaScript standard
seo-title: 'début rapide du SDK Web Adobe Experience Platform '
description: Guide de début rapide pour l’utilisation du SDK Web Experience Platform pour la collecte de données
seo-description: Guide de début rapide pour l’utilisation du SDK Web Experience Platform pour la collecte de données
translation-type: tm+mt
source-git-commit: d958e323df2535c168edd3a35b878fcc4bb73370
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 14%

---


# Bienvenue

Ce guide vous guide tout au long des différentes manières de configurer le SDK Adobe Experience Platform Web. Pour utiliser cette fonctionnalité, vous devez être autorisé. Si vous souhaitez monter sur la liste d&#39;attente, veuillez contacter votre CSM.

- Vous devez disposer d’un [domaine propriétaire (CNAME)](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html) activé. Si vous disposez déjà d’un CNAME pour Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionnent sans CNAME, mais vous en avez besoin avant de commencer la production.
- Avoir droit à l&#39;Adobe Experience Platform.  Si vous n’avez pas acheté Platform, l’Adobe vous fournira la Fondation Data Services Experience Platform pour une utilisation limitée avec le SDK sans frais supplémentaires.
- Vous devez utiliser la dernière version du service d’identifiant visiteur.

## Préparation d’un Schéma

Le [!DNL Experience Platform Edge Network] prend les données comme XDM. XDM est un format de données qui vous permet de définir des schémas. Le schéma définit la manière dont les données [!DNL Edge Network] doivent être formatées. Pour envoyer des données, vous devez définir votre schéma.

- [Création d’un schéma](../../xdm/tutorials/create-schema-ui.md)
- Add the Adobe Experience Platform [!DNL Web SDK] mixin to the schema you created

La vidéo suivante est destinée à vous aider à créer un schéma, un jeu de données et un connecteur source de flux continu pour vos [!DNL Web SDK] données.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Création d’un ID de configuration

Vous pouvez créer un ID de configuration à l’aide de l’outil [de configuration](../fundamentals/edge-configuration.md) Edge dans Adobe Launch, même si vous n’utilisez pas les fonctionnalités de gestion des balises. Cela vous permet de permettre à la [!DNL Edge Network] d&#39;envoyer des données aux différentes solutions. Vous trouverez des informations détaillées sur la manière de trouver chaque option dans la page Outil [de configuration](../fundamentals/edge-configuration.md) Edge.

>[!NOTE]
>
>Votre organisation doit être sur la liste autorisée de la fonction. Veuillez contacter votre CSM pour être mis sur la liste autorisée.

## Installation du SDK

Pour installer le SDK, copiez et collez le &quot;code de base&quot; suivant le plus haut possible dans la balise `<head>` de votre code HTML :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Pour plus d’informations sur les différentes options pour ce faire, voir [Installation du SDK](../fundamentals/installing-the-sdk.md).

## Configuration du SDK

Ensuite, fournissez votre configuration au SDK. Pour ce faire, utilisez la `configure` commande. Il doit s’agir de la première commande appelée sur chaque page.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Vous fournissez ici l’ID de configuration que vous avez créé ci-dessus ainsi que l’ID d’organisation. Il s’agit des deux seuls champs obligatoires. Cependant, il existe de nombreuses autres options [de](../fundamentals/configuring-the-sdk.md)configuration.

## Envoi d’un événement

Une fois que vous avez appelé la commande configure, vous êtes libre de début des événements de suivi.

```javascript
alloy("sendEvent", {});
```

En général, vous envoyez des événements contenant des données. Vous pouvez envoyer des données XDM comme celle-ci. Les données envoyées doivent se trouver dans le schéma que vous avez créé dans XDM.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Pour plus d’informations sur le suivi des événements, voir [Suivi des événements](../fundamentals/tracking-events.md).

## Étapes suivantes

Une fois les données circulées, vous pouvez effectuer les opérations suivantes :

- [Construisez votre schéma](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/schema/composition.html)
- [En savoir plus sur le débogage](../fundamentals/debugging.md)
- Découvrez comment [personnaliser l’expérience](../fundamentals/rendering-personalization-content.md)
- Découvrez comment envoyer des données à plusieurs solutions
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
