---
title: Traiter les données de consentement du client à l’aide du SDK Web de Adobe Experience Platform
topic-legacy: getting started
description: Découvrez comment intégrer le SDK Web de Adobe Experience Platform pour traiter les données de consentement des clients dans Adobe Experience Platform à l’aide de la norme Adobe 2.0.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 3%

---

# Intégrer le SDK Web Platform pour traiter les données de consentement des clients à l’aide de la norme Adobe 2.0

Le SDK Web de Adobe Experience Platform vous permet de récupérer les signaux de consentement des clients générés par les plateformes de gestion du consentement (CMP) et de les envoyer à Adobe Experience Platform chaque fois qu’un événement de modification du consentement se produit.

**Le SDK n’interface pas avec les CMP prêtes à l’emploi**. C’est à vous de déterminer comment intégrer le SDK à votre site web, écouter les modifications apportées au consentement dans la CMP et appeler la commande appropriée. Ce document fournit des instructions générales sur la manière d’intégrer votre CMP au SDK Web de Platform.

## Conditions préalables

Ce tutoriel suppose que vous avez déjà déterminé comment générer des données de consentement dans votre CMP et que vous avez créé un jeu de données contenant des champs de consentement activés pour Real-time Customer Profile. Pour en savoir plus sur ces étapes, consultez la présentation du [traitement du consentement dans Experience Platform](./overview.md) avant de revenir à ce guide.

En outre, ce guide nécessite une compréhension pratique des extensions Adobe Experience Platform Launch et de leur installation dans les applications web. Pour plus d’informations, consultez la documentation suivante :

* [Présentation des platform launchs](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=fr)
* [Guide de démarrage rapide](https://experienceleague.adobe.com/docs/launch/using/get-started/quick-start.html?lang=fr)
* [Présentation de la publication](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html?lang=fr)

## Configuration d’un flux de données

Pour que le SDK envoie des données à l’Experience Platform, un flux de données existant pour Platform doit être configuré dans Adobe Experience Platform Launch. En outre, le [!UICONTROL jeu de données de profil] que vous sélectionnez pour la configuration doit contenir des champs de consentement normalisés.

Après avoir créé une configuration ou sélectionné une configuration existante à modifier, cliquez sur le bouton de basculement en regard de **[!UICONTROL Adobe Experience Platform]**. Ensuite, utilisez les valeurs répertoriées ci-dessous pour remplir le formulaire.

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Champ de flux de données | Valeur |
| --- | --- |
| [!UICONTROL Environnement de test] | Nom de la plateforme [sandbox](../../../../sandboxes/home.md) qui contient la connexion en continu requise et les jeux de données pour configurer le flux de données. |
| [!UICONTROL Inlet de diffusion en continu] | Une connexion en continu valide pour l’Experience Platform. Consultez le tutoriel sur la [création d’une connexion en continu](../../../../ingestion/tutorials/create-streaming-connection-ui.md) si vous ne disposez pas d’inlet de diffusion existant. |
| [!UICONTROL Jeu de données d’événement] | Jeu de données [!DNL XDM ExperienceEvent] que vous prévoyez d’envoyer aux données d’événement à l’aide du SDK. Bien que vous soyez tenu de fournir un jeu de données d’événement pour créer un flux de données Platform, notez que l’envoi direct de données de consentement via des événements n’est actuellement pas pris en charge. |
| [!UICONTROL Jeu de données de profil] | Jeu de données compatible [!DNL Profile] avec les champs de consentement du client que vous avez créés précédemment. |

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** en bas de l’écran et continuez à suivre les autres invites pour terminer la configuration.


## Installation et configuration de l’extension SDK Web Platform

Une fois que vous avez créé un flux de données comme décrit dans la section précédente, vous devez configurer l’extension SDK Web Platform que vous allez déployer sur votre site. Si l’extension SDK n’est pas installée sur la propriété de Platform launch, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, suivi de l’onglet **[!UICONTROL Catalogue]** . Sélectionnez ensuite **[!UICONTROL Installer]** sous l’extension SDK Platform dans la liste des extensions disponibles.

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Lors de la configuration du SDK, sous **[!UICONTROL Configurations Edge]**, sélectionnez le flux de données que vous avez créé à l’étape précédente.

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour installer l’extension.

### Création d’un élément de données pour définir le consentement par défaut

Une fois l’extension SDK installée, vous avez la possibilité de créer un élément de données représentant la valeur de consentement de collecte de données par défaut (`collect.val`) pour vos utilisateurs. Cela peut s’avérer utile si vous souhaitez avoir différentes valeurs par défaut en fonction de l’utilisateur, telles que `pending` pour les utilisateurs de l’Union européenne et `in` pour les utilisateurs d’Amérique du Nord.

Dans ce cas d’utilisation, vous pouvez mettre en oeuvre les éléments suivants pour définir le consentement par défaut en fonction de la région de l’utilisateur :

1. Déterminez la région de l’utilisateur sur le serveur web.
1. Avant la balise de script de Platform launch (code incorporé) sur la page web, effectuez le rendu d’une balise de script distincte qui définit une variable `adobeDefaultConsent` en fonction de la région de l’utilisateur.
1. Configurez un élément de données qui utilise la variable JavaScript `adobeDefaultConsent` et utilisez cet élément de données comme valeur de consentement par défaut pour l’utilisateur.

Si la région de l’utilisateur est déterminée par une CMP, vous pouvez plutôt utiliser les étapes suivantes :

1. Gérez l’événement &quot;CMP loaded&quot; (Chargé par la CMP) sur la page.
1. Dans le gestionnaire d’événements, définissez une variable `adobeDefaultConsent` en fonction de la région de l’utilisateur, puis chargez le script de bibliothèque de Platform launchs à l’aide de JavaScript.
1. Configurez un élément de données qui utilise la variable JavaScript `adobeDefaultConsent` et utilisez cet élément de données comme valeur de consentement par défaut pour l’utilisateur.

Pour créer un élément de données dans l’interface utilisateur de Platform launch, sélectionnez **[!UICONTROL Éléments de données]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Ajouter un élément de données]** pour accéder à la boîte de dialogue de création de l’élément de données.

À partir de là, vous devez créer un élément de données [!UICONTROL Variable JavaScript] basé sur `adobeDefaultConsent`. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Une fois l’élément de données créé, revenez à la page de configuration de l’extension SDK Web. Dans la section [!UICONTROL Confidentialité], sélectionnez **[!UICONTROL Fourni par l’élément de données]** et utilisez la boîte de dialogue fournie pour sélectionner l’élément de données de consentement par défaut que vous avez créé précédemment.

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Déployer l’extension sur votre site web

Une fois que vous avez terminé de configurer l’extension, elle peut être intégrée à votre site web. Pour plus d’informations sur le déploiement de votre version de bibliothèque mise à jour, reportez-vous au [guide de publication](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html) dans la documentation du Platform launch.

## Exécution de commandes de changement de consentement

Une fois que vous avez intégré l’extension SDK à votre site web, vous pouvez commencer à utiliser la commande SDK Web Platform `setConsent` pour envoyer les données de consentement à Platform.

Il existe deux scénarios où `setConsent` doit être appelé sur votre site :

1. Lorsque le consentement est chargé sur la page (en d’autres termes, à chaque chargement de page)
1. Dans le cadre d’un crochet de CMP ou d’un écouteur d’événement qui détecte les modifications apportées aux paramètres de consentement

>[!NOTE]
>
>Pour une présentation de la syntaxe courante des commandes du SDK Platform, consultez le document sur [l’exécution des commandes](../../../../edge/fundamentals/executing-commands.md).

La commande `setConsent` requiert deux arguments :

1. Chaîne indiquant le type de commande (ici, `"setConsent"`)
1. Objet de payload contenant une seule propriété de type tableau : `consent`. Le tableau `consent` doit contenir au moins un objet qui fournit les champs de consentement requis pour la norme Adobe.

Les champs de consentement requis pour la norme Adobe sont présentés dans l’exemple d’appel `setConsent` suivant :

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
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Propriété Payload | Description |
| --- | --- |
| `standard` | La norme de consentement utilisée. Pour la norme Adobe, cette valeur doit être définie sur `Adobe`. |
| `version` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement standard par Adobe. |
| `value` | Informations de consentement mises à jour du client, fournies sous la forme d’un objet XDM conforme à la structure des champs de consentement du jeu de données activé par Profile. |

>[!NOTE]
>
>Si vous utilisez d’autres normes de consentement conjointement avec `Adobe` (comme `IAB TCF`), vous pouvez ajouter des objets supplémentaires au tableau `consent` pour chaque norme. Chaque objet doit contenir les valeurs appropriées pour `standard`, `version` et `value` pour la norme de consentement qu’il représente.

Le code JavaScript suivant illustre une fonction qui gère les modifications des préférences de consentement sur un site web, qui peuvent être utilisées comme rappel dans un écouteur d’événement ou un crochet de CMP :

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

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Gestion des réponses du SDK

Toutes les commandes [!DNL Platform SDK] renvoient des promesses indiquant si l’appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage des messages de confirmation au client. Pour obtenir des exemples spécifiques, reportez-vous à la section [Gestion de la réussite ou de l’échec](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) du guide sur l’exécution des commandes du SDK.

## Étapes suivantes

En suivant ce guide, vous avez configuré l’extension SDK Web Platform pour envoyer des données de consentement à Experience Platform. Vous pouvez maintenant revenir à la présentation du traitement du consentement pour savoir comment [tester votre mise en oeuvre](./overview.md#test-implementation).
