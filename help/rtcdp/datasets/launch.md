---
title: Didacticiel Mise en oeuvre des balises de site Web avec Adobe Launch
seo-title: Mise en oeuvre de balises de site Web avec Adobe Launch
description: Utilisation d’Adobe Launch pour implémenter des balises de site Web dans Adobe Experience Platform
seo-description: Utilisation d’Adobe Launch pour implémenter des balises de site Web dans Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 3083f6fb25a331eb6dd1d9a63b65aa206481dcb3

---


# Didacticiel :Mise en oeuvre de balises de site Web avec Adobe Launch

Ce didacticiel explique comment implémenter les balises de votre site Web pour envoyer des données à Adobe Experience Platform à l’aide d’Adobe Launch.

## Conditions préalables

* Le schéma et le jeu de données nécessaires sont créés dans Platform.
* La configuration nécessaire a été déployée dans Experience Edge et possède l’ID de configuration et le domaine Edge correspondants.
* Le CMS de l’entreprise a déjà été configuré pour fournir un objet JavaScript sur chaque page avec les données à envoyer à la plateforme.

## Étapes

Ce didacticiel décrit les étapes suivantes :

1. Installez l’extension Adobe Experience Platform Web SDK.
1. Créez une règle pour indiquer au lancement quelles données envoyer.
1. Regroupez l’extension et la règle dans une bibliothèque.

## Installation de l’extension SDK Web d’Adobe Experience Platform

Installez d’abord l’extension SDK Web d’Adobe Experience Platform.

1. In Launch, open the **[!UICONTROL Extensions]** tab.

   ![image](assets/launch-overview.png)

1. Sélectionnez l’extension SDK Web d’Adobe Experience Platform dans le catalogue de lancement de l’extension. L’écran de configuration s’ouvre.

   ![image](assets/launch-extension-install.png)

   Pour plus d’informations, voir [Extensions](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) dans la documentation sur le lancement.

1. Configuration de l’extension.

   Les seuls paramètres dont vous avez besoin pour l’instant sont les suivants :

   * **** ID de configuration : Indiquez l’ID de configuration que vous avez obtenu de votre représentant Adobe.
   * **** Domaine Edge : Indiquez le domaine Edge que vous avez obtenu de votre représentant Adobe.

1. Cliquez sur **[!UICONTROL Enregistrer]** et passez à l’étape suivante.

## Créez une règle pour indiquer au lancement quelles données envoyer

Créez ensuite une règle pour indiquer au lanceur quelles données vous souhaitez envoyer à Adobe Experience Platform et quand vous souhaitez l’envoyer.

1. Sous l’onglet **[!UICONTROL Règles]** , configurez un événement qui se déclenchera sur chaque nouvelle page du site Web au chargement de la bibliothèque de lancement.

   ![image](assets/launch-make-a-rule.png)

1. Ajouter une action.

   Pour configurer l’action, indiquez au lancement où trouver la couche de données. La couche de données est un objet JavaScript qui existe sur la page et qui est diffusé à partir du même CMS que celui qui effectue le rendu de la page Web. Indiquez le chemin JavaScript vers l’objet de données.

   ![image](assets/launch-add-aep-action.png)

   L’objet de données que vous envoyez doit être XDM valide et transmettre la validation par rapport au schéma utilisé par le jeu de données connecté à votre ID de configuration.

1. Click **[!UICONTROL Keep Changes]**.

Pour plus d’informations, voir [Règles](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) dans la documentation sur le lancement.

## Regrouper l’extension et la règle dans une bibliothèque

Ensuite, [assemblez l’extension](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) et votre nouvelle règle dans une bibliothèque et testez ces modifications dans un environnement de développement.

![image](assets/launch-add-changes-to-library.png)

Une fois les tests terminés, faites la promotion de la bibliothèque dans le flux de travail afin qu’elle puisse être déployée sur le site Production. Les données circulent désormais de chaque utilisateur vers Adobe Experience Platform.

![image](assets/launch-promote-library.png)

Pour plus d’informations, voir [Bibliothèques](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) dans la documentation de lancement.