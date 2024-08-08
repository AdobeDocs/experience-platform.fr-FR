---
title: Prise en main du transfert dʼévénements
description: Suivez ce tutoriel détaillé pour commencer à utiliser le transfert d’événement dans Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 0a95d09eb1ce59e45d52372c4b08725c009001c3
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 84%

---

# Prise en main du transfert dʼévénements

>[!NOTE]
>
>Le transfert d’événement est une fonctionnalité payante uniquement incluse dans les offres Connections, Prime, ou Ultimate d’Adobe Real-Time Customer Data Platform.

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Pour utiliser le transfert dʼévénements dans Adobe Experience Platform, les données doivent être envoyées à Adobe Experience Platform Edge Network à lʼaide de lʼune ou de plusieurs des trois options suivantes :

* [SDK web Adobe Experience Platform](../../extensions/client/web-sdk/overview.md)
* [ SDK Mobile Adobe Experience Platform](https://sdkdocs.com)
* [API du serveur réseau Edge](/help/server-api/overview.md)

>[!NOTE]
>Le SDK web Platform et le SDK mobile Platform ne nécessitent pas de déploiement par le biais de balises dans Adobe Experience Platform. Toutefois, il est recommandé dʼutiliser des balises pour déployer ces SDK.

Après avoir envoyé les données au réseau Edge, vous pouvez basculer sur des solutions Adobe pour y envoyer des données. Pour envoyer des données à une solution non Adobe, configurez-la dans le transfert dʼévénements.

## Conditions préalables

* Connexions Adobe Real-Time CDP, Prime ou Ultimate (contactez l’équipe de votre compte Adobe pour connaître les tarifs)
* Transfert d’événement dans Adobe Experience Platform
* SDK Web Adobe Experience Platform, SDK Mobile ou API de serveur Edge Network configurés pour envoyer des données à l’Edge Network
* Mettez en correspondance les données avec le modèle de données dʼexpérience (XDM) (cette mise en correspondance peut être effectuée à lʼaide de balises).

## Créer un schéma XDM

Créez votre schéma dans Adobe Experience Platform.

1. Créez un schéma en sélectionnant **[!UICONTROL Schémas]** > **[!UICONTROL Créer un schéma]** et en choisissant lʼoption **[!UICONTROL XDM ExperienceEvent]**.

1. Donnez un nom et une brève description au schéma.

1. Vous pouvez ajouter le groupe de champs &quot;Détails web ExperienceEvent&quot; en sélectionnant **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]**.

   >[!NOTE]
   >
   >Plusieurs groupes de champs peuvent être ajoutés, si nécessaire.

1. Enregistrez le schéma et notez le nom que vous lui avez donné.

Pour plus d’informations sur les schémas, voir [Aide du système XDM (Modèle de données d’expérience)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr).

## Création dʼune propriété de transfert dʼévénements

Dans l’espace de travail **[!UICONTROL Tags]**, créez une propriété de type **[!UICONTROL Edge]**.

1. Sélectionnez **[!UICONTROL Nouvelle propriété]**.

1. Attribuez un nom à la propriété.

1. Choisissez le type de plateforme &quot;Edge&quot;.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

Après avoir créé la propriété, accédez à lʼonglet **[!UICONTROL Environnements]** correspondant à la nouvelle propriété et
notez les identifiants de lʼenvironnement. Si lʼorganisation Adobe utilisée dans le flux de données diffère de celle utilisée dans le transfert dʼévénement, vous pouvez copier lʼidentifiant dʼenvironnement de lʼonglet **[!UICONTROL Environnements]** et le coller lors de la création dʼun flux de données. Sinon, vous pouvez sélectionner l’environnement dans un menu déroulant.

## Création dʼun flux de données

Pour créer votre flux de données dans Adobe Experience Platform, utilisez l’identifiant d’environnement généré lors de la création de la propriété de transfert d’événement.

1. Sélectionnez **[!UICONTROL Datastreams]** dans le volet de navigation de gauche.

1. Nommez la configuration et donnez une description facultative.
La description permet d’identifier les configurations dans une liste de plusieurs configurations.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

## Activation du transfert dʼévénements

Ensuite, configurez Edge Network pour envoyer des données au transfert dʼévénements et à dʼautres produits Adobe.

1. Dans l’espace de travail **[!UICONTROL Datastreams]**, sélectionnez la propriété que vous avez créée.

1. Sélectionnez l’environnement de développement, de production ou d’évaluation.

   Ou, pour envoyer des données à un environnement de transfert dʼévénements en dehors de lʼorganisation Adobe, sélectionnez la commande **[!UICONTROL Passer en mode avancé]** et collez-la dans un identifiant. Lʼidentifiant est fourni lorsque vous créez une propriété de transfert dʼévénements.

1. Activez les outils nécessaires et configurez-les selon les besoins.

   * Adobe Analytics requiert un identifiant de suite de rapports.

   * Le transfert d’événement dans Adobe Experience Platform nécessite un identifiant de propriété et un identifiant d’environnement. Il sʼagit du chemin de publication pour la propriété de transfert dʼévénements.

Après la configuration, prenez note des identifiants d’environnement pour la nouvelle propriété.

## Configurez l’extension SDK web de Platform pour envoyer des données au flux de données créé précédemment.

Créez votre propriété dans l’espace de travail **[!UICONTROL Balises]**, puis accédez à **[!UICONTROL Extensions]** et sélectionnez l’extension SDK Web Experience Platform dans le catalogue pour la configurer et l’installer.

Pour plus d’informations sur les options de configuration, voir la [documentation de l’extension SDK Web](../../extensions/client/web-sdk/overview.md) .

## Création dʼune règle de balise pour envoyer des données au SDK Web Platform

Quand les éléments ci-dessus sont en place, créez les définitions des données, règles, etc. qui utilisent le transfert dʼévénements et les balises, mais qui ont uniquement besoin dʼune seule requête provenant de la page.

Créez une règle de chargement de page à l’aide de l’extension SDK Web Platform et du type d’action &quot;Envoyer l’événement&quot; :

1. Ouvrez lʼonglet **[!UICONTROL Règles]**, puis sélectionnez **[!UICONTROL Créer une règle]**.

1. Attribuez un nom à la règle.

1. Cliquez sur lʼicône **[!UICONTROL Ajouter]** sous Événements.

1. Ajoutez un événement en choisissant une extension et l’un des types d’événements disponibles pour cette extension, puis configurez les paramètres de l’événement. Par exemple, sélectionnez **[!UICONTROL Core - Fenêtre chargée]**.

1. Ajoutez une action à l’aide de l’extension du SDK Web Platform. Sélectionnez **[!UICONTROL Envoyer lʼévénement]** dans la liste **[!UICONTROL Type dʼaction]**, sélectionnez lʼinstance de votre choix (instance Alloy configurée précédemment), puis sélectionnez un élément de données à ajouter au bloc de données XDM dans lʼaccès Alloy.

1. Laissez le reste des paramètres par défaut pour cet exemple, puis sélectionnez **[!UICONTROL Enregistrer]**.

Autre exemple : vous pouvez créer une règle qui envoie la couche de données à Edge si l’utilisateur passe la souris sur un bouton spécifié.

## Résumé

Les éléments suivants étant en place, vous pouvez désormais créer des règles de transfert dʼévénements pour transférer des données vers des destinations autres quʼAdobe.

* Schéma du modèle de données dʼexpérience (notez le nom que vous lui avez donné).
* Propriété de transfert dʼévénements (gardez une trace de lʼidentifiant de propriété et des identifiants dʼenvironnements).
* Flux de données (prenez note de lʼidentifiant dʼenvironnement, qui ne doit pas être confondu avec lʼidentifiant dʼenvironnement du transfert dʼévénements.)
* Propriété de balise
