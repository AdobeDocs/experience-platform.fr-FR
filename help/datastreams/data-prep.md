---
title: Préparation des données pour la collecte de données
description: Découvrez comment mapper vos données à un schéma d’événement du modèle de données d’expérience (XDM) lors de la configuration d’un flux de données pour les SDK web et mobile d’Adobe Experience Platform.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 60%

---

# Préparation des données pour la collecte de données

La préparation des données est un service Adobe Experience Platform qui vous permet de mapper, transformer et valider des données depuis et vers le [modèle de données d’expérience (XDM)](../xdm/home.md). Lors de la configuration d’un [flux de données](./overview.md) compatible avec Platform, vous pouvez utiliser les fonctionnalités de préparation des données pour mapper vos données source à XDM lors de leur envoi à Platform Edge Network.

Toutes les données envoyées à partir d’une page web doivent atterrir en Experience Platform sous la forme XDM. Il existe 3 manières de traduire les données d’une couche de données sur la page vers le XDM accepté par l’Experience Platform :

1. Reformétez la couche de données dans XDM sur la page web elle-même.
2. Utilisez la fonctionnalité Balises - Éléments de données natifs pour reformater le format de couche de données existant d’une page web en XDM.
3. Reformater le format de couche de données d’une page web dans XDM via l’Edge Network, à l’aide de la préparation de données pour la collecte de données.

Ce guide se concentre sur la 3e option.

## Quand utiliser la préparation de données pour la collecte de données {#when-to-use-data-prep}

Dans deux cas d’utilisation, la préparation des données pour la collecte de données est utile :

1. Le site web dispose d’une couche de données bien formée, bien gérée et bien gérée. Il est préférable de l’envoyer directement à l’Edge Network plutôt que d’utiliser la manipulation JavaScript pour le convertir au format XDM sur la page (soit par le biais d’éléments de données de balises, soit par le biais d’une manipulation manuelle de JavaScript).
2. Un système de balisage autre que Balises est déployé sur le site.

## Envoyer une couche de données existante à l’Edge Network via WebSDK {#send-datalayer-via-websdk}

La couche de données existante doit être envoyée à l’aide de l’objet [`data`](/help/web-sdk/commands/sendevent/data.md) dans la commande `sendEvent`.

Si vous utilisez des balises, vous devez utiliser le champ **[!UICONTROL Data]** du type d’action **[!UICONTROL Send Event]**, comme décrit dans la [documentation de l’extension de balise Web SDK](/help/tags/extensions/client/web-sdk/action-types.md).

Le reste de ce guide se concentrera sur la manière de mapper la couche de données aux normes XDM une fois qu’elle a été envoyée par le SDK WebSDK.

>[!NOTE]
>
>Pour obtenir des instructions complètes sur toutes les fonctionnalités de préparation des données, y compris les fonctions de transformation des champs calculés, consultez la documentation suivante :
>
>* [Présentation de la préparation des données](../data-prep/home.md)
>* [Fonctions de mappage de la préparation des données](../data-prep/functions.md)
>* [Gestion des formats de données avec la préparation des données](../data-prep/data-handling.md)

Ce guide explique comment mapper vos données dans l’interface utilisateur. Pour respecter les étapes, commencez le processus de création d’un flux de données jusqu’à (et y compris) l’[étape de configuration de base](./overview.md#create).

Pour une démonstration rapide du processus de préparation des données pour la collecte de données, reportez-vous à la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Sélectionner les données] {#select-data}

Une fois la configuration de base d’un flux de données terminée, sélectionnez **[!UICONTROL Enregistrer et Ajouter un mappage]** pour passer à l’étape **[!UICONTROL Sélectionner les données]**. Ensuite, vous devez fournir un exemple d’objet JSON qui représente la structure des données que vous prévoyez d’envoyer à Platform.

Pour capturer les propriétés directement à partir de la couche de données, l’objet JSON doit comporter une seule propriété racine `data`. Les sous-propriétés de l’objet `data` doivent ensuite être construites de manière à correspondre aux propriétés de couche de données que vous souhaitez capturer. Sélectionnez la section ci-dessous pour afficher un exemple d’objet JSON correctement formaté avec une racine `data`.

+++Fichier JSON Sample avec une racine `data`

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Les mêmes règles s’appliquent à l’objet JSON pour capturer les propriétés d’un élément de données d’objet XDM, mais la propriété racine doit plutôt être saisie en tant que `xdm`. Sélectionnez la section ci-dessous pour afficher un exemple d’objet JSON correctement formaté avec une racine `xdm`.

+++Fichier JSON Sample avec une racine `xdm`

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

Vous pouvez sélectionner l’option pour charger l’objet sous forme de fichier ou coller l’objet brut dans la zone de texte fournie. Si le fichier JSON est valide, un schéma d’aperçu s’affiche dans le panneau de droite. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Exemple JSON de données entrantes attendues.](assets/data-prep/select-data.png)

>[!NOTE]
>
> Utilisez un exemple d’objet JSON qui représente chaque élément de couche de données pouvant être utilisé sur n’importe quelle page. Par exemple, toutes les pages n’utilisent pas les éléments de couche de données du panier. Toutefois, les éléments de couche de données du panier doivent être inclus dans cet exemple d’objet JSON.

## [!UICONTROL Mappage]

L’étape **[!UICONTROL Mappage]** s’affiche et vous permet de mapper les champs de vos données source à ceux du schéma d’événement cible dans Platform. Ensuite, vous pouvez configurer le mappage de deux manières :

* [Créez des règles de mappage](#create-mapping) pour ce flux de données par le biais d’un processus manuel.
* [Importer des règles de mappage](#import-mapping) d’un flux de données existant.

### Création de règles de mappage {#create-mapping}

Pour créer une règle de mappage, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**.

![Ajout d&#39;un nouveau mapping.](assets/data-prep/add-new-mapping.png)

Sélectionnez l’icône de source (![icône de source](assets/data-prep/source-icon.png)) et, dans la boîte de dialogue qui s’affiche, sélectionnez le champ source que vous souhaitez mapper dans la zone de travail fournie. Une fois que vous avez choisi un champ, utilisez le bouton **[!UICONTROL Sélectionner]** pour continuer.

![Sélectionner le champ à mapper dans le schéma source.](assets/data-prep/source-mapping.png)

Ensuite, sélectionnez l’icône de schéma (![icône de schéma](assets/data-prep/schema-icon.png)) pour ouvrir une boîte de dialogue similaire pour le schéma d’événement cible. Sélectionnez le champ vers lequel vous souhaitez mapper les données avant de confirmer à l’aide du bouton **[!UICONTROL Sélectionner]**.

![Sélectionner le champ à mapper dans le schéma cible.](assets/data-prep/target-mapping.png)

La page de mappage réapparaît et affiche le mappage des champs terminé. La section **[!UICONTROL Progression du mappage]** est mise à jour pour refléter le nombre total de champs qui ont été mappés.

![Champ mappé avec la progression reflétée.](assets/data-prep/field-mapped.png)

>[!TIP]
>
>Si vous souhaitez mapper un tableau d’objets (dans le champ source) à un tableau d’objets différents (dans le champ cible), ajoutez `[*]` après le nom du tableau dans les chemins d’accès aux champs source et de destination, comme illustré ci-dessous.
>
>![Mappage d’objet Array.](assets/data-prep/array-object-mapping.png)

### Importer les règles de mappage existantes {#import-mapping}

Si vous avez déjà créé un flux de données, vous pouvez réutiliser ses règles de mappage configurées pour un nouveau flux de données.

>[!WARNING]
>
>L’importation de règles de mappage à partir d’un autre flux de données remplace les mappages de champs que vous avez peut-être ajoutés avant l’importation.

Pour commencer, sélectionnez **[!UICONTROL Importer le mappage]**.

![Bouton de mappage d’importation en cours de sélection.](assets/data-prep/import-mapping-button.png)

Dans la boîte de dialogue qui s’affiche, sélectionnez le flux de données dont vous souhaitez importer les règles de mappage. Une fois le flux de données choisi, sélectionnez **[!UICONTROL Aperçu]**.

![Sélection d’un flux de données existant.](assets/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Les flux de données peuvent uniquement être importés dans le même [sandbox](../sandboxes/home.md). En d’autres termes, vous ne pouvez pas importer un flux de données d’un sandbox à un autre.

L’écran suivant affiche un aperçu des règles de mappage enregistrées pour le flux de données sélectionné. Assurez-vous que les mappages affichés vous conviennent, puis sélectionnez **[!UICONTROL Importer]** pour confirmer et ajouter les mappages au nouveau flux de données.

![ Règles de mappage à importer.](assets/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Si des champs source dans les règles de mappage importées ne sont pas inclus dans les exemples de données JSON que vous avez [fournis précédemment](#select-data), ces mappages de champs ne seront pas inclus dans l’importation.

### Terminer le mappage

Continuez à suivre les étapes ci-dessus pour mapper le reste des champs au schéma cible. Bien que vous n’ayez pas à mapper tous les champs source disponibles, tous les champs du schéma cible définis selon les besoins doivent être mappés pour terminer cette étape. Le compteur **[!UICONTROL Champs obligatoires]** indique le nombre de champs obligatoires qui ne sont pas encore mappés dans la configuration actuelle.

Une fois que le nombre de champs requis est nul et que vous êtes satisfait de votre mappage, sélectionnez **[!UICONTROL Enregistrer]** pour finaliser vos modifications.

![Mappage terminé](assets/data-prep/mapping-complete.png)

## Étapes suivantes

Ce guide explique comment mapper les données à XDM lors de la configuration d’un flux de données dans l’interface utilisateur. Si vous avez suivi le tutoriel général sur les flux de données, vous pouvez maintenant revenir à l’étape sur l’[affichage des détails des flux de données](./overview.md).
