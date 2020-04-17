---
title: Démarrage rapide avec Launch
seo-title: 'SDK Web d’Adobe Experience Platform : démarrage rapide avec Launch'
description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
seo-description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

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

## Demande d’un ID de configuration

Vous devez disposer d’un ID de configuration pour utiliser le SDK. L’ID de configuration garantit que vos données sont acheminées au bon endroit. Vous pouvez obtenir un ID de configuration soit auprès de votre consultant, soit auprès de l’Assistance clientèle. Vous devrez fournir les informations suivantes :

- **ID d’organisation :** vous pouvez le trouver en suivant les instructions [ici](https://docs.adobe.com/content/help/fr-FR/core-services/interface/manage-users-and-products/organizations.html).
- **ID de jeu de données :** il est disponible dans l’interface utilisateur des jeux de données lorsque vous cliquez sur un jeu de données.
- **ID de schéma :** il est disponible dans l’URL de l’écran de création de schéma.
- **Nom convivial :** il s’agit du nom convivial qui sera utilisé dans les futures interfaces utilisateur pour cette configuration.

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
