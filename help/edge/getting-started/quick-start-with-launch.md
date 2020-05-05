---
title: Démarrage rapide avec Launch
seo-title: 'SDK Web d’Adobe Experience Platform : démarrage rapide avec Launch'
description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
seo-description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
translation-type: tm+mt
source-git-commit: e23b0ce9c20d5d2d770d1c1261fe08de5743325a

---


# (Version bêta) Conditions préalables

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Actuellement, le SDK Web d’Adobe Experience Platform ne prend en charge que l’envoi de données à Adobe Experience Platform à l’aide de XDM. Vous devez remplir les conditions préalables ci-après.

- Vous devez disposer d’un [domaine propriétaire (CNAME)](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html) activé. Si vous disposez déjà d’un CNAME pour Analytics, vous devez l’utiliser.
- Vous devez avoir le droit d’accéder à Adobe Experience Platform.
- Vous devez utiliser la dernière version du service d’identifiant visiteur

## Préparation de la plateforme

Pour pouvoir envoyer des données à Adobe Experience Platform, vous devez créer un XDM et un jeu de données qui utilise ce schéma.

- [Créez un schéma](../../xdm/tutorials/create-schema-ui.md) avec les mixins suivants :
   - Détails de l’implémentation d’ExperienceEvent
   - Détails de l’environnement d’ExperienceEvent
   - Détails Web d’ExperienceEvent
- Ajoutez le mixin du SDK Web d’Adobe Experience Platform au schéma créé.
- [Créez un jeu de données](https://platform.adobe.com/dataset/overview) avec votre schéma à l’emplacement où vous souhaitez que les données se trouvent.

## Création d’un ID de configuration

Vous pouvez créer un ID de configuration à l’aide de l’outil [de configuration](../fundamentals/edge-configuration.md) edge au lancement.

>Remarque : Votre organisation doit être mise en liste blanche pour la fonction. Veuillez contacter votre CSM pour qu&#39;il soit mis sur la liste pour une éventuelle liste blanche.

## Installation du SDK dans Launch

Connectez-vous à Launch et installez l’extension `AEP Web SDK`. Dans le cadre de l’installation du SDK, vous serez invité à configurer l’extension. Entrez l’ID de configuration que vous avez demandé ci-dessus. L’extension renseigne automatiquement l’ID d’organisation.

Pour plus d’informations sur les différentes options de configuration, voir [Configuration du SDK](../fundamentals/configuring-the-sdk.md).

## Envoi d’un événement

Une fois l’extension installée, commencez à envoyer des événements en ajoutant une action d’envoi de balise à partir de l’extension SDK Web d’AEP. Il est recommandé d’envoyer au moins un événement chaque fois qu’une page est chargée avec l’option « occurs at the start of a view » cochée.

Pour plus d’informations sur le suivi des événements, voir [Suivi des événements](../fundamentals/tracking-events.md).

## Envoi des données

Vous pouvez envoyer des données qui correspondent au schéma que vous avez créé auparavant avec vos événements. Par exemple, si vous possédez un site de commerce et que vous ajoutez le mixin de commerce à votre schéma, vous envoyez la structure ci-dessous lorsqu’un utilisateur consulte un produit.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
