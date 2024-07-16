---
title: Traiter les données de consentement du client à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment intégrer le SDK Web de Adobe Experience Platform pour traiter les données de consentement des clients dans Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 2%

---

# Intégrer le SDK Web Platform pour traiter les données de consentement du client

Le SDK Web de Adobe Experience Platform vous permet de récupérer les signaux de consentement des clients générés par les plateformes de gestion du consentement (CMP) et de les envoyer à Adobe Experience Platform chaque fois qu’un événement de modification du consentement se produit.

**Le SDK n’interface pas de CMP prêtes à l’emploi**. C’est à vous de déterminer comment intégrer le SDK à votre site web, écouter les modifications apportées au consentement dans la CMP et appeler la commande appropriée. Ce document fournit des instructions générales sur la manière d’intégrer votre CMP au SDK Web de Platform.

## Conditions préalables {#prerequisites}

Ce tutoriel suppose que vous avez déjà déterminé comment générer des données de consentement dans votre CMP et que vous avez créé un jeu de données contenant des champs de consentement conformes à la norme Adobe ou à la norme IAB Transparency and Consent Framework (TCF) 2.0. Si vous n’avez pas encore créé ce jeu de données, reportez-vous aux tutoriels suivants avant de revenir à ce guide :

* [Création d’un jeu de données à l’aide de la norme Adobe](./adobe/dataset.md)
* [Création d’un jeu de données à l’aide de la norme TCF 2.0](./iab/dataset.md)

Ce guide suit le processus de configuration du SDK à l’aide de l’extension de balise dans l’interface utilisateur. Si vous ne souhaitez pas utiliser l’extension et que vous préférez incorporer directement la version autonome du SDK sur votre site, reportez-vous aux documents suivants au lieu de ce guide :

* [Configurer un trains de données](/help/datastreams/overview.md)
* [Installation du SDK](/help/web-sdk/install/overview.md)
* [Configuration du SDK pour les commandes de consentement](/help/web-sdk/commands/configure/defaultconsent.md)

Les étapes d’installation de ce guide nécessitent une compréhension pratique des extensions de balise et de leur installation dans les applications web. Pour plus d’informations, reportez-vous à la documentation suivante :

* [Présentation des balises](/help/tags/home.md)
* [Guide de démarrage rapide](/help/tags/quick-start/quick-start.md)
* [Présentation de la publication](/help/tags/ui/publishing/overview.md)

## Configuration d’un flux de données

Pour que le SDK envoie des données à l’Experience Platform, vous devez d’abord configurer un flux de données. Dans l’interface utilisateur de la collecte de données ou l’interface utilisateur Experience Platform, sélectionnez **[!UICONTROL Datastreams]** dans le volet de navigation de gauche.

Après avoir créé un nouveau flux de données ou sélectionné un flux existant à modifier, cliquez sur le bouton de basculement en regard de **[!UICONTROL Adobe Experience Platform]**. Ensuite, utilisez les valeurs répertoriées ci-dessous pour remplir le formulaire.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Champ de flux de données | Valeur |
| --- | --- |
| [!UICONTROL Sandbox] | Le nom de la plateforme [sandbox](../../../sandboxes/home.md) qui contient la connexion en continu requise et les jeux de données pour configurer le flux de données. |
| [!UICONTROL Jeu de données d’événement] | Jeu de données [!DNL XDM ExperienceEvent] que vous prévoyez d’envoyer aux données d’événement à à l’aide du SDK. Bien que vous soyez tenu de fournir un jeu de données d’événement pour créer un flux de données Platform, notez que les données de consentement envoyées par le biais d’événements ne sont pas honorées dans les workflows d’application en aval. |
| [!UICONTROL Jeu de données de profil] | Jeu de données [!DNL Profile] avec champs de consentement du client que vous avez créé [précédemment](#prerequisites). |

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** en bas de l’écran et continuez à suivre les autres invites pour terminer la configuration.

## Installation et configuration du SDK Web de Platform

Une fois que vous avez créé un flux de données comme décrit dans la section précédente, vous devez configurer l’extension SDK Web Platform que vous allez déployer sur votre site. Si l’extension SDK n’est pas installée sur votre propriété de balise, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, suivi de l’onglet **[!UICONTROL Catalogue]** . Sélectionnez ensuite **[!UICONTROL Installer]** sous l’extension du SDK Platform dans la liste des extensions disponibles.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Lors de la configuration du SDK, sous **[!UICONTROL Configurations d’Edge]**, sélectionnez la banque de données que vous avez créée à l’étape précédente.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Sélectionnez **[!UICONTROL Save]** pour installer l’extension.

### Créer un élément de données pour définir le consentement par défaut

Une fois l’extension SDK installée, vous avez la possibilité de créer un élément de données représentant la valeur de consentement de collecte de données par défaut (`collect.val`) pour vos utilisateurs. Cela peut s’avérer utile si vous souhaitez avoir différentes valeurs par défaut en fonction de l’utilisateur, telles que `pending` pour les utilisateurs de l’Union européenne et `in` pour les utilisateurs d’Amérique du Nord.

Dans ce cas d’utilisation, vous pouvez mettre en oeuvre les éléments suivants pour définir le consentement par défaut en fonction de la région de l’utilisateur :

1. Déterminez la région de l’utilisateur sur le serveur web.
1. Avant la balise `script` (code incorporé) sur la page web, effectuez le rendu d’une balise `script` distincte définissant une variable `adobeDefaultConsent` en fonction de la région de l’utilisateur.
1. Configurez un élément de données qui utilise la variable JavaScript `adobeDefaultConsent` et utilisez cet élément de données comme valeur de consentement par défaut pour l’utilisateur.

Si la région de l’utilisateur est déterminée par une CMP, vous pouvez plutôt utiliser les étapes suivantes :

1. Gérez l’événement &quot;CMP loaded&quot; (Chargé par la CMP) sur la page.
1. Dans le gestionnaire d’événements, définissez une variable `adobeDefaultConsent` en fonction de la région de l’utilisateur, puis chargez le script de bibliothèque de balises à l’aide de JavaScript.
1. Configurez un élément de données qui utilise la variable JavaScript `adobeDefaultConsent` et utilisez cet élément de données comme valeur de consentement par défaut pour l’utilisateur.

Pour créer un élément de données dans l’interface utilisateur, sélectionnez **[!UICONTROL Data Elements]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Add Data Element]** pour accéder à la boîte de dialogue de création de l’élément de données.

À partir de là, vous devez créer un élément de données [!UICONTROL Variable JavaScript] basé sur `adobeDefaultConsent`. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Une fois l’élément de données créé, revenez à la page de configuration de l’extension SDK Web. Sous la section [!UICONTROL Confidentialité], sélectionnez **[!UICONTROL Fourni par l’élément de données]** et utilisez la boîte de dialogue fournie pour sélectionner l’élément de données de consentement par défaut que vous avez créé précédemment.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Déployer l’extension sur votre site web

Une fois que vous avez terminé de configurer l’extension, elle peut être intégrée à votre site web. Pour plus d’informations sur le déploiement de votre version de bibliothèque mise à jour, reportez-vous au [guide de publication](../../../tags/ui/publishing/overview.md) dans la documentation sur les balises.

## Exécution de commandes de changement de consentement {#commands}

Une fois que vous avez intégré l’extension SDK à votre site web, vous pouvez commencer à utiliser la commande SDK Web Platform `setConsent` pour envoyer les données de consentement à Platform.

La commande `setConsent` effectue deux actions :

1. Met à jour les attributs de profil de l’utilisateur directement dans la banque de profils. Cela n’envoie aucune donnée au lac de données.
1. Crée un [événement d’expérience](../../../xdm/classes/experienceevent.md) qui enregistre un compte horodaté de l’événement de modification du consentement. Ces données sont envoyées directement au lac de données et peuvent être utilisées pour suivre les changements de préférences de consentement au fil du temps.

### Quand appeler `setConsent`

Il existe deux scénarios où `setConsent` doit être appelé sur votre site :

1. Lorsque le consentement est chargé sur la page (en d’autres termes, à chaque chargement de page)
1. Dans le cadre d’un crochet de CMP ou d’un écouteur d’événement qui détecte les modifications apportées aux paramètres de consentement

### Syntaxe `setConsent`

La commande [`setConsent`](/help/web-sdk/commands/setconsent.md) exige un objet de charge utile contenant une seule propriété de type tableau : `consent`. Le tableau `consent` doit contenir au moins un objet qui fournit les champs de consentement requis pour la norme Adobe.

Les champs de consentement requis pour la norme d’Adobe sont affichés dans l’exemple d’appel `setConsent` suivant :

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

| Propriété Payload | Description |
| --- | --- |
| `standard` | La norme de consentement utilisée. Pour la norme Adobe, cette valeur doit être définie sur `Adobe`. |
| `version` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement standard par Adobe. |
| `value` | Informations de consentement mises à jour du client, fournies sous la forme d’un objet XDM conforme à la structure des champs de consentement du jeu de données activé par Profile. |

>[!NOTE]
>
>Si vous utilisez d’autres normes de consentement conjointement avec `Adobe` (telles que `IAB TCF`), vous pouvez ajouter des objets supplémentaires au tableau `consent` pour chaque norme. Chaque objet doit contenir les valeurs appropriées pour `standard`, `version` et `value` pour la norme de consentement qu’il représente.

Le JavaScript suivant fournit un exemple de fonction qui gère les modifications des préférences de consentement sur un site web, qui peuvent être utilisées comme rappel dans un écouteur d’événement ou un crochet de CMP :

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

Toutes les commandes [!DNL Platform SDK] renvoient des promesses indiquant si l’appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage des messages de confirmation au client. Voir [Réponses de commande](/help/web-sdk/commands/command-responses.md) pour plus d’informations.

Une fois que vous avez effectué avec succès des appels `setConsent` avec le SDK, vous pouvez utiliser la visionneuse de profils dans l’interface utilisateur de Platform pour vérifier si les données arrivent dans la banque de profils. Pour plus d’informations, consultez la section sur la [navigation des profils par identité](../../../profile/ui/user-guide.md#browse-identity) .

## Étapes suivantes

En suivant ce guide, vous avez configuré l’extension SDK Web Platform pour envoyer des données de consentement à Experience Platform. Pour plus d’informations sur le test de votre mise en oeuvre, reportez-vous à la documentation de la norme de consentement que vous mettez en oeuvre :

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0 standard](./iab/overview.md#test)
