---
title: Prise En Main Du Transfert D’Événements
description: Suivez ce tutoriel détaillé pour commencer à utiliser le transfert d’événement dans Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 48%

---

# Prise en main du transfert d’événement

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Pour utiliser le transfert d’événement dans Adobe Experience Platform, les données doivent être envoyées à Adobe Experience Platform Edge Network à l’aide d’une ou de plusieurs des trois options suivantes :

* [SDK web Adobe Experience Platform](../../extensions/web/sdk/overview.md)
* [SDK mobile Adobe Experience Platform](https://sdkdocs.com)
* [API serveur à serveur](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>Le SDK Web Platform et le SDK Mobile Platform ne nécessitent pas de déploiement par le biais de balises dans Adobe Experience Platform. Toutefois, il est recommandé d’utiliser des balises pour déployer ces SDK.

Après avoir envoyé les données au réseau Edge, vous pouvez basculer sur des solutions Adobe pour y envoyer des données. Pour envoyer des données à une solution non Adobe, configurez-la dans le transfert d’événement.

## Conditions préalables

* Adobe Experience Platform Collection Enterprise (contactez votre gestionnaire de compte pour connaître les tarifs)
* Transfert d’événement dans Adobe Experience Platform
* SDK Web ou Mobile Adobe Experience Platform, configuré pour envoyer des données au réseau Edge
* Faire correspondre les données au modèle de données d’expérience (XDM) (ce mappage peut être effectué à l’aide de balises).

## Créer un schéma XDM

Créez votre schéma dans Adobe Experience Platform.

1. Créez un schéma en sélectionnant **[!UICONTROL Schémas]** > **[!UICONTROL Créer un schéma]** et en choisissant lʼoption **[!UICONTROL XDM ExperienceEvent]**.

1. Donnez un nom et une brève description au schéma.

1. Vous pouvez ajouter le groupe de champs &quot;Détails web ExperienceEvent&quot; en sélectionnant **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]**.

   >[!NOTE]
   >
   >Vous pouvez ajouter plusieurs groupes de champs, le cas échéant.

1. Enregistrez le schéma et notez le nom que vous lui avez donné.

Pour plus d’informations sur les schémas, voir [Aide du système XDM (Modèle de données d’expérience)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr).

## Création d’une propriété de transfert d’événement

Dans l’interface utilisateur de la collecte de données, créez une propriété de type &quot;Edge&quot;.

1. Sélectionnez **[!UICONTROL Nouvelle propriété]**.

1. Attribuez un nom à la propriété.

1. Choisissez le type de plate-forme « Edge ».

1. Sélectionnez **[!UICONTROL Enregistrer]**.

Après avoir créé la propriété, accédez à lʼonglet **[!UICONTROL Environnements]** correspondant à la nouvelle propriété et
notez les identifiants de lʼenvironnement. Si l’organisation d’Adobe utilisée dans la file d’attente des données diffère de l’organisation d’Adobe utilisée dans le transfert d’événement, vous pouvez copier l’identifiant d’environnement de l’onglet **[!UICONTROL Environnements]** et le coller lors de la création d’un flux de données. Sinon, vous pouvez sélectionner l’environnement dans un menu déroulant.

## Création d’un flux de données

Pour créer votre flux de données dans Adobe Experience Platform, utilisez l’identifiant d’environnement généré lors de la création de la propriété de transfert d’événement.

1. Utilisez le lien situé dans le rail gauche de l’interface utilisateur de la collecte de données pour ouvrir l’interface des flux de données.

1. Sélectionnez **[!UICONTROL Flux de données]**.

1. Nommez la configuration et donnez une description facultative.
La description permet d’identifier les configurations dans une liste de plusieurs configurations.

1. Sélectionnez **[!UICONTROL Enregistrer]**.



## Activation du transfert d’événement

Ensuite, configurez Edge Network pour envoyer des données au transfert d’événement et à d’autres produits Adobe.

1. Dans l’interface utilisateur des flux de données, sélectionnez la propriété que vous avez créée.

1. Sélectionnez l’environnement de développement, de production ou d’évaluation.

   Ou, pour envoyer des données à un environnement de transfert d’événement en dehors de l’organisation d’Adobe, sélectionnez **[!UICONTROL Passer en mode avancé]** et collez-les dans un ID. L’identifiant est fourni lorsque vous créez une propriété de transfert d’événement.

1. Activez les outils nécessaires et configurez-les selon les besoins.

   * Adobe Analytics requiert un identifiant de suite de rapports.

   * Le transfert d’événement dans Adobe Experience Platform requiert un identifiant de propriété et un identifiant d’environnement. Il s’agit du chemin de publication de la propriété de transfert d’événement.

Après la configuration, prenez note des identifiants d’environnement pour la nouvelle propriété.

## Configurez l’extension SDK Web de balise pour envoyer des données à la banque de données créée précédemment

Créez votre propriété dans l’interface utilisateur de la collecte de données, puis utilisez l’extension SDK Web Adobe Experience Platform pour la configurer.

1. Attribuez un nom à la propriété.

   Vous pouvez avoir plusieurs instances d’Alloy. Par exemple, vous pourriez avoir différentes propriétés de suivi avant et après paywall.

1. Sélectionnez l’identifiant d’organisation.

1. Sélectionnez le domaine Edge.

Consultez la [documentation relative à l’extension SDK Web](../../extensions/web/sdk/overview.md) pour plus d’options de configuration.

## Créer une règle de balise pour envoyer des données au SDK Web Platform

Une fois que les balises ci-dessus sont en place, créez des définitions de données, des règles, etc. qui utilisent le transfert d’événement et les balises, mais qui ne nécessitent qu’une seule requête de la page.

Créez une règle de chargement de page à lʼaide de lʼextension SDK web Platform et du type dʼaction « Envoyer lʼévénement » :

1. Ouvrez lʼonglet **[!UICONTROL Règles]**, puis sélectionnez **[!UICONTROL Créer une règle]**.

1. Attribuez un nom à la règle.

1. Cliquez sur lʼicône **[!UICONTROL Ajouter]** sous Événements.

1. Ajoutez un événement en choisissant une extension et l’un des types d’événements disponibles pour cette extension, puis configurez les paramètres de l’événement. Par exemple, sélectionnez **[!UICONTROL Core - Fenêtre chargée]**.

1. Ajoutez une action à l’aide de l’extension du SDK Web Platform. Sélectionnez **[!UICONTROL Envoyer lʼévénement]** dans la liste **[!UICONTROL Type dʼaction]**, sélectionnez lʼinstance de votre choix (instance Alloy configurée précédemment), puis sélectionnez un élément de données à ajouter au bloc de données XDM dans lʼaccès Alloy.

1. Laissez le reste des paramètres par défaut pour cet exemple, puis sélectionnez **[!UICONTROL Enregistrer]**.

Autre exemple : vous pouvez créer une règle qui envoie la couche de données à Edge si l’utilisateur passe la souris sur un bouton spécifié.

## Résumé

Les éléments suivants étant en place, vous pouvez désormais créer des règles de transfert d’événement pour transférer des données vers des destinations autres que les Adobes.

* Schéma du modèle de données dʼexpérience (notez le nom que vous lui avez donné).
* Une propriété de transfert d’événement (suivez l’ID de propriété et les ID d’environnement).
* Un flux de données (notez l’ID d’environnement, à ne pas confondre avec l’ID d’environnement du transfert d’événement.)
* Propriété de balise
