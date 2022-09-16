---
title: Configuration de l’extension du SDK Web Adobe Experience Platform
description: Comment configurer l’extension de balise du SDK Web Adobe Experience Platform dans l’interface utilisateur de la collecte de données.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 6%

---

# Configuration de l’extension du SDK Web Adobe Experience Platform

L’extension de balise SDK Web Adobe Experience Platform envoie des données à Adobe Experience Cloud à partir de propriétés web via Adobe Experience Platform Edge Network. L’extension vous permet de diffuser des données dans Platform, de synchroniser les identités, de traiter les signaux de consentement du client et de collecter automatiquement des données contextuelles.

Ce document explique comment configurer l’extension dans l’interface utilisateur de la collecte de données.

## Prise en main

Si l’extension SDK Web Platform a déjà été installée pour une propriété, ouvrez la propriété dans l’interface utilisateur de la collecte de données et sélectionnez l’option **[!UICONTROL Extensions]** . Sous Platform Web SDK, sélectionnez **[!UICONTROL Configurer]**.

![](../images/extension/overview/configure.png)

Si vous n’avez pas encore installé l’extension, sélectionnez l’extension **[!UICONTROL Catalogue]** . Dans la liste des extensions disponibles, recherchez l’extension SDK Web Platform et sélectionnez **[!UICONTROL Installer]**.

![](../images/extension/overview/install.png)

Dans les deux cas, vous accédez à la page de configuration du SDK Web Platform. Les sections ci-dessous expliquent les options de configuration de l’extension.

![](../images/extension/overview/config-screen.png)

## Options de configuration générales

Les options de configuration en haut de la page indiquent à Adobe Experience Platform où acheminer les données et quelles configurations utiliser sur le serveur.

### [!UICONTROL Nom]

L’extension SDK Web Adobe Experience Platform prend en charge plusieurs instances sur la page. Le nom est utilisé pour envoyer des données à plusieurs organisations avec une configuration de balise.

Par défaut, le nom de l’extension est &quot;[!DNL alloy]&quot;. Vous pouvez toutefois remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide.

### **[!UICONTROL Identifiant IMS de l’organisation]**

Le [!UICONTROL Identifiant de l’organisation IMS] est l’organisation à laquelle vous souhaitez envoyer les données dans Adobe. La plupart du temps, utilisez la valeur par défaut qui est renseignée automatiquement. Si la page contient plusieurs instances, renseignez ce champ avec la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.

### **[!UICONTROL Domaine Edge]**

Le [!UICONTROL Domaine Edge] est le domaine à partir duquel l’extension Adobe Experience Platform envoie et reçoit des données. Adobe recommande d’utiliser un domaine propriétaire (CNAME) pour cette extension. Le domaine tiers par défaut fonctionne pour les environnements de développement, mais ne convient pas aux environnements de production. Les instructions de configuration d’un CNAME propriétaire sont répertoriées [ici](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=fr).

## [!UICONTROL Flux de données]

Lorsqu’une demande est envoyée au réseau Adobe Experience Platform Edge, un identifiant de flux de données est utilisé pour référencer la configuration côté serveur. Vous pouvez mettre à jour la configuration sans avoir à apporter de modifications au code sur votre site web.

Consultez le guide sur la [datastreams](../datastreams/overview.md) pour plus d’informations.


## [!UICONTROL Confidentialité]

![](../images/extension/overview/privacy.png)

Le [!UICONTROL Confidentialité] vous permet de configurer la manière dont le SDK traite les signaux de consentement de l’utilisateur de votre site web. Plus précisément, il vous permet de sélectionner le niveau de consentement par défaut supposé d’un utilisateur si aucune autre préférence de consentement explicite n’a été fournie. Le niveau de consentement par défaut n’est pas enregistré dans le profil de l’utilisateur. Le tableau suivant décompose les fonctions de chaque option :

| [!UICONTROL Niveau de consentement par défaut] | Description |
| --- | --- |
| [!UICONTROL Dans] | Collectez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL Out] | Ignorer les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL En attente] | Événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. Lorsque les préférences de consentement sont fournies, les événements sont collectés ou ignorés en fonction des préférences fournies. |
| [!UICONTROL Fourni par l’élément de données] | Le niveau de consentement par défaut est déterminé par un élément de données distinct que vous définissez. Lorsque vous utilisez cette option, vous devez spécifier l’élément de données à l’aide du menu déroulant fourni. |

Utilisez Out ou Pending (En attente) si vous avez besoin du consentement explicite de l’utilisateur pour vos activités commerciales.

## [!UICONTROL Identité]

![](../images/extension/overview/identity.png)

### [!UICONTROL Migration de l’ECID depuis VisitorAPI]

Cette option est affichée par défaut. Lorsque cette fonction est activée, le SDK peut lire les cookies AMCV et s_ecid et définir le cookie AMCV utilisé par Visitor.js. Cette fonctionnalité est importante lors de la migration vers le SDK Web de Adobe Experience Platform, car certaines pages peuvent toujours utiliser Visitor.js. Il permet au SDK de continuer à utiliser le même ECID afin que les utilisateurs ne soient pas identifiés comme deux utilisateurs distincts.

### [!UICONTROL Utilisation de cookies tiers]

Cette option permet au SDK de tenter de stocker un identifiant d’utilisateur dans un cookie tiers. En cas de réussite, l’utilisateur est identifié comme un utilisateur unique lorsqu’il navigue sur plusieurs domaines, plutôt que comme un utilisateur distinct sur chaque domaine. Si cette option est activée, le SDK peut toujours ne pas pouvoir stocker l’identifiant de l’utilisateur dans un cookie tiers si le navigateur ne prend pas en charge les cookies tiers ou s’il a été configuré par l’utilisateur pour ne pas autoriser les cookies tiers. Dans ce cas, le SDK stocke uniquement l’identifiant dans le domaine propriétaire.

## [!UICONTROL Personnalisation]

![](../images/extension/overview/personalization.png)

Si vous souhaitez masquer certaines parties si le contenu personnalisé de votre site est chargé, vous pouvez spécifier les éléments à masquer dans l’éditeur de style de prémasquage. Vous pouvez ensuite copier le fragment de code de masquage préalable par défaut qui vous a été fourni et le coller dans le `<head>`de votre site de HTML.

## [!UICONTROL Collecte de données]

![](../images/extension/overview/data-collection.png)

### [!UICONTROL Fonction de rappel]

La fonction de rappel fournie dans l’extension est également appelée [`onBeforeEventSend` function](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) dans la bibliothèque. Cette fonction vous permet de modifier les événements de manière globale avant qu’ils ne soient envoyés à Adobe Edge Network. Vous trouverez des informations plus détaillées sur l’utilisation de cette fonction [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Clic sur la collecte de données]

Le SDK peut automatiquement collecter des informations sur les clics sur les liens. Cette fonctionnalité est activée par défaut, mais elle peut être désactivée à l’aide de cette option. Les liens sont également étiquetés comme liens de téléchargement s’ils contiennent l’une des expressions de téléchargement répertoriées dans la variable [!UICONTROL Télécharger le qualificateur de lien] textbox. Adobe vous fournit quelques qualificateurs de lien de téléchargement par défaut, mais ils peuvent être modifiés à tout moment.

### [!UICONTROL Données contextuelles collectées automatiquement]

Par défaut, le SDK collecte certaines données contextuelles concernant l’appareil, le web, l’environnement et le contexte de lieu. Si vous souhaitez voir une liste des informations collectées par l&#39;Adobe, vous pouvez la trouver. [here](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Si vous ne souhaitez pas que ces données soient collectées ou que vous souhaitez uniquement que certaines catégories de données soient collectées, vous pouvez modifier ces options.

## [!UICONTROL Paramètres avancés]

![](../images/extension/overview/advanced-settings.png)

### [!UICONTROL Chemin de base Edge]

Utilisez ce champ si vous devez modifier le chemin de base utilisé pour interagir avec Adobe Edge Network. Cela ne doit pas nécessiter de mise à jour, mais dans le cas où vous participez à une version bêta ou alpha, l’Adobe peut vous demander de modifier ce champ.
