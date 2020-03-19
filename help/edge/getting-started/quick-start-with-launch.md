---
title: ' rapide avec lancement'
seo-title: rapide du kit SDK Web d’Adobe Experience Platform avec lancement
description: Guide de  rapide pour l’utilisation de l’extension SDK Web Experience Platform pour la collecte de données
seo-description: Guide de  rapide pour l’utilisation de l’extension SDK Web Experience Platform pour la collecte de données
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Conditions préalables

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Actuellement, le SDK Web d’Adobe Experience Platform ne prend en charge que l’envoi de données vers Adobe Experience Platform à l’aide de XDM. Vous devez satisfaire aux conditions préalables suivantes.

- Activez un domaine [propriétaire (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) . Si vous disposez déjà d’un CNAME pour Analytics, vous devez l’utiliser.
- Être autorisé à utiliser Adobe Experience Platform
- Utiliser la dernière version du service d’ID de

## Préparation de la plate-forme

Pour pouvoir envoyer des données à Adobe Experience Platform, vous devez créer un XDM et un jeu de données qui utilise cet .

- [Créez un](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) avec les mixins suivants :
   - Détails de l’implémentation d’ExperienceEvent
   - Détails de l&#39; ExperienceEvent 
   - Détails Web d’ExperienceEvent
- Ajouter le mixin SDK Web d’Adobe Experience Platform au  que vous avez créé
- [Créez un jeu](https://platform.adobe.com/dataset/overview) de données avec votre à l’emplacement où vous souhaitez que les données s’affichent.

## Demande d’un ID de configuration

Vous devez disposer d’un ID de configuration pour utiliser le SDK. L’ID de configuration garantit que vos données sont acheminées au bon endroit. Vous pouvez obtenir un ID de configuration soit auprès de votre consultant, soit auprès du service à la clientèle. Ils auront besoin des informations suivantes :

- **ID d&#39;entreprise :** Vous pouvez le trouver en suivant les instructions [ici](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **ID du jeu de données :** Cette option est disponible dans l’interface utilisateur du jeu de données lorsque vous cliquez sur un jeu de données.
- **ID  :** Cette information est disponible dans l’URL de l’écran de création  du
- **Nom convivial :** Nom convivial qui sera utilisé dans les futures interfaces utilisateur pour cette configuration

## Installation du SDK au lancement

Connectez-vous à Launch et installez l’ `AEP Web SDK` extension. Dans le cadre de l’installation du SDK, vous serez invité à configurer l’extension. Entrez l&#39;ID de configuration que vous avez demandé ci-dessus. L’extension renseigne automatiquement votre ID d’organisation.

Pour plus d’informations sur les différentes options de configuration, voir [Configuration du SDK](../fundamentals/configuring-the-sdk.md).

## Envoyer un 

Une fois l’extension installée, le envoie   en ajoutant une action &quot;Send Beacon&quot; à partir de l’extension AEP Web SDK. Il est recommandé d’envoyer au moins un  chaque fois qu’une page est chargée, l’option &quot;se produit au  d’un &quot; étant cochée.

Pour plus d&#39;informations sur le suivi des  de, reportez-vous à la page  de [suivi des](../fundamentals/tracking-events.md).

## Envoyer des données

Vous pouvez envoyer des données qui correspondent au que vous avez créé plus tôt avec votre  de. Par exemple, si vous possédez un site de commerce et que vous ajoutez le mixin de commerce à votre  de, vous envoyez la structure suivante lorsqu’un utilisateur  un produit.

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
