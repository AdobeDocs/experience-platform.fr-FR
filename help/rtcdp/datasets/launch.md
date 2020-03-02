---
title: Tutoriel Mise en œuvre des balises de site web avec Adobe Launch
seo-title: Mise en œuvre des balises de site web avec Adobe Launch
description: Utilisation d’Adobe Launch pour mettre en œuvre des balises de site web dans Adobe Experience Platform
seo-description: Utilisation d’Adobe Launch pour mettre en œuvre des balises de site web dans Adobe Experience Platform
translation-type: ht
source-git-commit: 3083f6fb25a331eb6dd1d9a63b65aa206481dcb3

---


# Tutoriel : mise en œuvre des balises de site web avec Adobe Launch

Ce tutoriel explique comment mettre en œuvre les balises de votre site web pour envoyer des données à Adobe Experience Platform à l’aide d’Adobe Launch.

## Conditions préalables

* Le schéma et le jeu de données nécessaires sont créés dans Platform.
* La configuration requise a été déployée dans Experience Edge et possède l’ID de configuration et le domaine Edge correspondants.
* Le CMS de l’entreprise a déjà été configuré pour fournir un objet JavaScript sur chaque page avec les données à envoyer à Platform.

## Étapes

Ce tutoriel décrit les étapes suivantes :

1. Installer l’extension Adobe Experience Platform Web SDK
1. Créer une règle pour indiquer à Launch les données à envoyer
1. Regrouper l’extension et la règle dans une bibliothèque

## Installer l’extension Adobe Experience Platform Web SDK

Tout d’abord, installez l’extension Adobe Experience Platform Web SDK.

1. Dans Launch, ouvrez l’onglet **[!UICONTROL Extensions]**.

   ![image](assets/launch-overview.png)

1. Sélectionnez l’extension Adobe Experience Platform Web SDK dans le catalogue d’extensions de Launch.
L’écran de configuration s’ouvre.

   ![image](assets/launch-extension-install.png)

   Pour plus d’informations, consultez [Extensions](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/overview.html) dans la documentation de Launch.

1. Configurez l’extension.

   Pour l’instant, vous avez seulement besoin des paramètres suivants :

   * **ID de configuration :** indiquez l’ID de configuration que votre représentant Adobe vous a remis.
   * **Domaine Edge :** indiquez le domaine Edge que votre représentant Adobe vous a remis.

1. Cliquez sur **[!UICONTROL Enregistrer]** et passez à l’étape suivante.

## Créer une règle pour indiquer à Launch les données à envoyer

Ensuite, créez une règle pour indiquer à Launch les données à envoyer à Adobe Experience Platform et le moment auquel vous souhaitez les envoyer.

1. Sous l’onglet **[!UICONTROL Règles]**, configurez un événement qui se déclenche sur chaque nouvelle page du site web au chargement de la bibliothèque de Launch.

   ![image](assets/launch-make-a-rule.png)

1. Ajoutez une action.

   Pour configurer l’action, indiquez à Launch où trouver la couche de données. La couche de données est un objet JavaScript qui existe sur la page et qui est diffusé à partir du même CMS que celui qui effectue le rendu de la page web. Indiquez le chemin d’accès JavaScript vers l’objet de données.

   ![image](assets/launch-add-aep-action.png)

   L’objet de données que vous envoyez doit être un XDM validé par le schéma utilisé par le jeu de données connecté à votre ID de configuration.

1. Cliquez sur **[!UICONTROL Conserver les modifications]**.

Pour plus d’informations, consultez [Règles](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/rules.translate.html) dans la documentation de Launch.

## Regrouper l’extension et la règle dans une bibliothèque

Ensuite, [regroupez l’extension](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/publish/overview.html) et votre nouvelle règle dans une bibliothèque et testez ces modifications dans un environnement de développement.

![image](assets/launch-add-changes-to-library.png)

Une fois les tests terminés, faites la promotion de la bibliothèque dans le workflow afin qu’elle puisse être déployée sur le site de production. Les données circulent désormais de chaque utilisateur vers Adobe Experience Platform.

![image](assets/launch-promote-library.png)

Pour plus d’informations, consultez [Bibliothèques](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/publish/libraries.html) dans la documentation de Launch.