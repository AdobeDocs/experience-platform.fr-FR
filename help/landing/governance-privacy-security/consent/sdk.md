---
title: Traiter les données de consentement des clients à l’aide de Adobe Experience Platform Web SDK
description: Découvrez comment intégrer Adobe Experience Platform Web SDK pour traiter les données de consentement des clients dans Adobe Experience Platform.
role: Developer
feature: Consent, Web SDK
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 2%

---

# Intégrer Experience Platform Web SDK pour traiter les données de consentement des clients

Adobe Experience Platform Web SDK vous permet de récupérer les signaux de consentement des clients générés par les plateformes de gestion du consentement (CMP) et de les envoyer à Adobe Experience Platform chaque fois qu’un événement de changement de consentement se produit.

**Le SDK n’est pas compatible avec les CMP prêts à l’emploi**. C’est à vous de déterminer comment intégrer SDK à votre site web, d’être attentif aux modifications apportées au consentement dans la CMP et d’appeler la commande appropriée. Ce document fournit des instructions générales sur l’intégration de votre CMP à Experience Platform Web SDK.

## Conditions préalables {#prerequisites}

Ce tutoriel suppose que vous avez déjà déterminé comment générer des données de consentement dans votre CMP et que vous avez créé un jeu de données contenant des champs de consentement conformes à la norme Adobe ou à la norme IAB Transparency and Consent Framework (TCF) 2.0. Si vous n’avez pas encore créé ce jeu de données, reportez-vous aux tutoriels suivants avant de revenir à ce guide :

* [Création d’un jeu de données à l’aide de la norme Adobe](./adobe/dataset.md)
* [Créer un jeu de données à l’aide de la norme TCF 2.0](./iab/dataset.md)

Ce guide suit le processus de configuration de SDK à l’aide de l’extension de balise dans l’interface utilisateur. Si vous ne souhaitez pas utiliser l’extension et que vous préférez incorporer directement la version autonome du SDK sur votre site, reportez-vous à la documentation suivante au lieu de ce guide :

* [Configurer un trains de données](/help/datastreams/overview.md)
* [Installation du SDK](/help/collection/js/install/overview.md)
* [Configuration du SDK pour les commandes de consentement](/help/collection/js/commands/configure/defaultconsent.md)

Les étapes d’installation de ce guide nécessitent une compréhension pratique des extensions de balises et de leur installation dans des applications web. Pour plus d’informations, reportez-vous à la documentation suivante :

* [Présentation des balises](/help/tags/home.md)
* [Guide de démarrage rapide](/help/tags/quick-start/quick-start.md)
* [Présentation de la publication](/help/tags/ui/publishing/overview.md)

## Configurer un flux de données

Pour que le SDK envoie des données à Experience Platform, vous devez d’abord configurer un flux de données. Dans l’interface utilisateur de collecte de données ou d’Experience Platform, sélectionnez **[!UICONTROL Datastreams]** dans le volet de navigation de gauche.

Après avoir créé un flux de données ou sélectionné un flux de données existant à modifier, cliquez sur le bouton de basculement en regard de **[!UICONTROL Adobe Experience Platform]**. Ensuite, utilisez les valeurs répertoriées ci-dessous pour remplir le formulaire.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Champ du flux de données | Valeur |
| --- | --- |
| [!UICONTROL Sandbox] | Nom de l’Experience Platform [sandbox](/help/sandboxes/home.md) qui contient la connexion en continu requise et les jeux de données pour configurer le flux de données. |
| [!UICONTROL Event Dataset] | Jeu de données [!DNL XDM ExperienceEvent] que vous prévoyez d’envoyer à à l’aide de SDK. Bien que vous deviez fournir un jeu de données d’événement pour créer un flux de données Experience Platform, les données de consentement envoyées par le biais d’événements ne sont pas respectées dans les workflows d’application en aval. |
| [!UICONTROL Profile Dataset] | Le jeu de données [!DNL Profile] avec les champs de consentement client que vous avez créé [précédemment](#prerequisites). |

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]** en bas de l’écran et continuez à suivre les invites supplémentaires pour terminer la configuration.

## Installation et configuration d’Experience Platform Web SDK

Une fois que vous avez créé un flux de données comme décrit dans la section précédente, vous devez configurer l’extension Experience Platform Web SDK que vous déploierez finalement sur votre site. Si l’extension SDK n’est pas installée sur votre propriété de balise, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, suivi de l’onglet **[!UICONTROL Catalog]** . Sélectionnez ensuite **[!UICONTROL Install]** sous l’extension Experience Platform SDK dans la liste des extensions disponibles.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Lors de la configuration du SDK, sous **[!UICONTROL Edge Configurations]**, sélectionnez le flux de données que vous avez créé à l’étape précédente.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Sélectionnez **[!UICONTROL Save]** pour installer l’extension.

### Créer un élément de données pour définir le consentement par défaut

Une fois l’extension SDK installée, vous avez la possibilité de créer un élément de données pour représenter la valeur de consentement de collecte de données par défaut (`collect.val`) pour vos utilisateurs. Cela peut s’avérer utile si vous souhaitez définir différentes valeurs par défaut en fonction de l’utilisateur, par exemple `pending` pour les utilisateurs de l’Union européenne et `in` pour les utilisateurs d’Amérique du Nord.

Dans ce cas d’utilisation, vous pouvez implémenter les éléments suivants pour définir le consentement par défaut en fonction de la région de l’utilisateur :

1. Déterminez la région de l’utilisateur sur le serveur web.
1. Avant la balise `script` (code incorporé) sur la page web, effectuez le rendu d’une balise `script` distincte qui définit une variable `adobeDefaultConsent` en fonction de la région de l’utilisateur.
1. Configurez un élément de données qui utilise la variable JavaScript `adobeDefaultConsent` et utilisez cet élément de données comme valeur de consentement par défaut pour l’utilisateur.

Si la région de l’utilisateur est déterminée par une CMP, vous pouvez suivre les étapes suivantes à la place :

1. Gérez l’événement « CMP loaded » sur la page.
1. Dans le gestionnaire d’événements , définissez une variable `adobeDefaultConsent` en fonction de la région de l’utilisateur, puis chargez le script de la bibliothèque de balises à l’aide de JavaScript.
1. Configurez un élément de données qui utilise la variable JavaScript `adobeDefaultConsent` et utilisez cet élément de données comme valeur de consentement par défaut pour l’utilisateur.

Pour créer un élément de données dans l’interface utilisateur, sélectionnez **[!UICONTROL Data Elements]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Add Data Element]** pour accéder à la boîte de dialogue de création d’élément de données.

À partir de là, vous devez créer un élément de données [!UICONTROL JavaScript Variable] basé sur `adobeDefaultConsent`. Sélectionnez **[!UICONTROL Save]** (Enregistrer) une fois terminé.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Une fois l’élément de données créé, revenez à la page de configuration de l’extension Web SDK. Sous la section [!UICONTROL Privacy] , sélectionnez **[!UICONTROL Provided by data element]** et utilisez la boîte de dialogue fournie pour sélectionner l’élément de données de consentement par défaut que vous avez créé précédemment.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Déployez l’extension sur votre site web

Une fois la configuration de l’extension terminée, elle peut être intégrée à votre site web. Pour obtenir des informations détaillées sur le déploiement de la version de bibliothèque mise à jour[&#x200B; consultez le &#x200B;](/help/tags/ui/publishing/overview.md) guide de publication dans la documentation sur les balises.

## Exécution de commandes de modification du consentement {#commands}

Une fois que vous avez intégré l’extension SDK à votre site web, vous pouvez commencer à utiliser la commande de `setConsent` Experience Platform Web SDK pour envoyer des données de consentement à Experience Platform.

La commande `setConsent` effectue deux actions :

1. Met à jour les attributs de profil de l’utilisateur directement dans la banque de profils. Cela n’envoie aucune donnée au lac de données.
1. Crée un [événement d’expérience](/help/xdm/classes/experienceevent.md) qui enregistre un compte horodaté de l’événement de changement de consentement. Ces données sont envoyées directement au lac de données et peuvent être utilisées pour suivre les modifications des préférences de consentement au fil du temps.

### Quand appeler `setConsent`

Il existe deux scénarios dans lesquels `setConsent` doit être appelé sur votre site :

1. Lorsque le consentement est chargé sur la page (en d’autres termes, à chaque chargement de page)
1. Dans le cadre d’un hook CMP ou d’un écouteur d’événement qui détecte les modifications des paramètres de consentement

### syntaxe `setConsent`

La commande [`setConsent`](/help/collection/js/commands/setconsent.md) exige un objet de payload contenant une seule propriété de type tableau : `consent`. Le tableau `consent` doit contenir au moins un objet qui fournit les champs de consentement requis pour la norme Adobe.

Les champs de consentement requis pour la norme Adobe sont affichés dans l’exemple d’appel de `setConsent` suivant :

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Propriété de payload | Description |
| --- | --- |
| `standard` | Norme de consentement utilisée. Pour la norme Adobe, cette valeur doit être définie sur `Adobe`. |
| `version` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement standard Adobe. |
| `value` | Les informations de consentement mises à jour du client, fournies sous la forme d’un objet XDM conforme à la structure des champs de consentement du jeu de données activé pour Profile. |

>[!NOTE]
>
>Si vous utilisez d’autres normes de consentement conjointement avec `Adobe` (telles que `IAB TCF`), vous pouvez ajouter des objets supplémentaires au tableau `consent` pour chaque norme. Chaque objet doit contenir les valeurs appropriées pour `standard`, `version` et `value` pour la norme de consentement qu’ils représentent.

Le JavaScript suivant fournit un exemple de fonction qui gère les modifications des préférences de consentement sur un site web, qui peut être utilisée comme rappel dans un écouteur d’événement ou un hook CMP :

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Experience Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Gestion des réponses SDK

Toutes les commandes [!DNL Experience Platform SDK] renvoient des promesses indiquant si l’appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage de messages de confirmation au client. Voir [Réponses des commandes](/help/collection/js/commands/command-responses.md) pour plus d’informations.

Une fois que vous avez effectué `setConsent` appels avec le SDK, vous pouvez utiliser la visionneuse de profils dans l’interface utilisateur d’Experience Platform pour vérifier si les données arrivent dans la banque de profils. Pour plus d’informations, consultez la section sur la [navigation dans les profils par identité](/help/profile/ui/user-guide.md#browse-identity).

## Étapes suivantes

En suivant ce guide, vous avez configuré l’extension Experience Platform Web SDK pour envoyer des données de consentement à Experience Platform. Pour obtenir des conseils sur le test de votre implémentation, reportez-vous à la documentation de la norme de consentement que vous implémentez :

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0 standard](./iab/overview.md#test)
