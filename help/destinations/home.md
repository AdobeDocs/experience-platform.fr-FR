---
title: Présentation des destinations
description: Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant dʼAdobe Experience Platform. Vous pouvez utiliser les destinations dans Adobe Experience Platform pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 48%

---

# Présentation des [!DNL Destinations] {#overview}

![Bannière de présentation des destinations.](./assets/overview/destinations-overview-banner.png)

Les **[!DNL Destinations]** sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinations et sources {#destinations-and-sources}

L’une des principales fonctionnalités d’Experience Platform consiste à ingérer vos données propriétaires et à les activer en fonction des besoins de votre entreprise. Utilisez des [sources](../sources/home.md) pour ingérer des données dans Experience Platform et des destinations pour exporter des données à partir d’Experience Platform.

## Étapes des destinations {#steps}

* Effectuez un choix parmi un [catalogue en libre-service](./catalog/overview.md) de toutes les destinations disponibles dans Experience Platform.
* Utilisez les destinations pour envoyer des audiences ou des jeux de données aux plateformes d’automatisation marketing, de publicité numérique, etc.
* Planifiez régulièrement des exportations de données vers les destinations de votre choix.

## Commandes {#controls}

Les commandes de l’[espace de travail des destinations](./ui/destinations-workspace.md) vous permettent d’effectuer les opérations suivantes :

* parcourir le catalogue des plateformes de destination dans lesquelles vous pouvez activer vos données ;
* créer, modifier, activer et désactiver des flux de données vers les destinations du catalogue ;
* Créer un compte dans un emplacement de stockage ou lier Experience Platform au compte dans la plateforme de destination ;
* Sélectionner les audiences ou les jeux de données à activer pour les destinations ;
* Sélectionnez les [champs de modèle de données d’expérience (XDM)](../xdm/home.md) à exporter lors de l’activation d’audiences vers certaines destinations telles que les destinations de marketing par e-mail, les plateformes CRM, les emplacements d’espace de stockage, etc.
* Activez différents types de profils et d’audiences vers les destinations : personnes, comptes et prospects.

## Types et catégories de destination {#types-and-categories}

Avec Experience Platform, vous pouvez activer des données vers différents types de destinations, afin de répondre à vos cas d’utilisation d’activation. Les destinations vont des intégrations basées sur les API aux intégrations avec les systèmes de réception de fichiers, en passant par les destinations de recherche de profil, etc. Pour plus d’informations sur toutes les destinations disponibles, lisez la [présentation des types et catégories de destination](./destination-types.md).

## Destinations créées par Adobe et les partenaires {#adobe-and-partner-built-destinations}

Certains des connecteurs du catalogue des destinations Experience Platform sont créés et gérés par Adobe, tandis que d’autres sont créés et gérés par des sociétés partenaires qui utilisent [Destination SDK](/help/destinations/destination-sdk/overview.md). Une note en haut de la page de documentation pour chaque connecteur créé par un partenaire indique si une destination est créée et gérée par le partenaire. Par exemple, le [connecteur Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) est créé par Adobe, tandis que le [connecteur TikTok](/help/destinations/catalog/social/tiktok.md) est créé et géré par l’équipe TikTok.

Pour les connecteurs créés et gérés par un partenaire, les problèmes liés au connecteur peuvent devoir être résolus par l’équipe du partenaire (la méthode de contact est fournie dans la note de la page de documentation). Pour tout problème concernant les connecteurs créés et gérés par Adobe, contactez votre personne représentante d’Adobe ou l’Assistance clientèle.

## Destinations et contrôles d’accès {#access-controls}

La fonctionnalité de destinations d’Experience Platform fonctionne avec les autorisations de contrôle d’accès de Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. Pour plus d’informations sur les autorisations individuelles, accédez à [contrôle d’accès dans Adobe Experience Platform](../access-control/home.md) et faites défiler la page vers le bas, jusqu’au tableau.

Le tableau suivant décrit les autorisations et combinaisons d’autorisations requises pour effectuer certaines actions sur les destinations.

| Niveau d’autorisation | Description |
| ---- | ---- |
| **[!UICONTROL Affichage des destinations]** | Pour accéder à l’onglet Destinations dans l’interface utilisateur d’Experience Platform, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher les destinations]** [&#128279;](/help/access-control/home.md#permissions). |
| **[!UICONTROL Affichage Des Destinations]**, **[!UICONTROL Gestion Des Destinations]** | Pour vous connecter aux destinations, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). |
| **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Affichage des profils]** et **[!UICONTROL Affichage des segments]** | Pour activer les audiences vers les destinations et activer l’[étape de mappage](ui/activate-batch-profile-destinations.md#mapping) du workflow, vous devez disposer des **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Affichage des profils]** et **[!UICONTROL Affichage des segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). |
| **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation de segments sans mappage]**, **[!UICONTROL Affichage des profils]** et **[!UICONTROL Affichage des segments]** | Pour ajouter ou supprimer des audiences de flux de données existants sans avoir accès à l’[étape de mappage](ui/activate-batch-profile-destinations.md#mapping) du workflow, vous devez disposer des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer des segments sans mappage]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). |
| **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Gestion et activation des destinations de jeu de données]** | Pour exporter des jeux de données vers des destinations, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer et activer les destinations de jeu de données]** [&#128279;](/help/access-control/home.md#permissions). |
| **[!UICONTROL Afficher un graphique d’identité]** | Pour exporter des *identités* vers les destinations, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Le diagramme ci-dessous affiche visuellement les autorisations dont vous avez besoin en fonction des opérations que vous souhaitez effectuer sur les destinations.

![Diagramme affichant les autorisations requises pour effectuer certaines actions sur les destinations.](/help/destinations/assets/overview/permissions-diagram.png)

Pour plus d’informations sur les contrôles d’accès, consultez le [Guide de l’utilisateur du contrôle d’accès](../access-control/ui/overview.md).

### Contrôle d’accès basé sur les attributs pour les destinations {#attribute-based-access}

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs.

Grâce au contrôle d’accès basé sur les attributs, vous pouvez appliquer des configurations de mappage aux champs pour lesquels vous disposez d’autorisations. En outre, vous ne pouvez pas exporter de données vers une destination si vous n’avez pas accès à tous les champs du jeu de données.

Pour plus d’informations sur le fonctionnement des destinations avec les contrôles d’accès basés sur les attributs, consultez la section [Présentation du contrôle d’accès basé sur les attributs](../access-control/abac/overview.md#destinations).

## Suppression de profils des destinations {#profile-removal}

Lorsqu’un profil est supprimé d’une audience activée vers une destination, ce profil est également supprimé de l’audience correspondante dans la plateforme de destination. Par exemple, si un profil est supprimé d’une audience précédemment activée sur LinkedIn, ce profil est supprimé de l’[!UICONTROL audience correspondante LinkedIn] associée.

La suppression de profils des destinations, également appelée non segmentation, se produit à la même cadence que la segmentation. Dès qu’un profil est supprimé d’une audience dans Experience Platform, le prochain flux de données planifié vers la destination reflète cette modification et supprime le profil de l’audience de destination.

La vitesse réelle à laquelle la suppression du profil prend effet dans la plateforme de destination peut varier en fonction du comportement d’ingestion et de traitement de la destination.

## Surveillance des destinations {#destinations-monitoring}

Après avoir établi une connexion à une destination et terminé le workflow d’activation, vous pouvez surveiller les exportations de données vers votre système de réception. Lisez le [guide sur la surveillance des flux de données vers les destinations dans l’interface utilisateur](/help/dataflows/ui/monitor-destinations.md) pour plus d’informations.

![Exemple de page de surveillance des destinations.](./assets/overview/monitoring-page-example.png)

Vous pouvez également vérifier si les données arrivent à votre destination. La plupart des pages de documentation des destinations du catalogue ont une section *Valider l’exportation des données*, qui indique comment vous pouvez vérifier dans la plateforme de destination que les données sont importées depuis Experience Platform. Consultez un exemple de cette section pour la destination [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Restrictions de gouvernance des données concernant l’activation des données vers les destinations {#data-governance}

La gouvernance des données est appliquée aux destinations Experience Platform par le biais des actions suivantes :

* *Actions marketing* que vous pouvez sélectionner dans le workflow de création de destinations ;
* *Politiques d’utilisation des données* qui limitent l’activation des données contenant certains libellés d’utilisation vers les destinations avec certaines actions marketing.

Consultez la documentation sur la gouvernance des données dans Experience Platform pour plus d’informations sur les [actions marketing](../data-governance/policies/overview.md) et [résolution des violations de politique de données](../data-governance/enforcement/auto-enforcement.md).

Pour plus d’informations sur la sélection d’actions marketing dans le workflow de création de destination, consultez les pages suivantes pour les différents types de destinations dans Experience Platform :

* [Destinations publicitaires - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Destinations publicitaires - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinations publicitaires - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Destinations de stockage dans le cloud](./catalog/cloud-storage/overview.md)
* [Destinations de marketing par e-mail ](./catalog/email-marketing/overview.md)
* [Destinations sociales](./catalog/social/overview.md)

Pour plus d’informations sur les violations de politique de données dans le workflow Audience Activation, voir l’étape **[!UICONTROL Révision]** dans les guides suivants :

* [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](./ui/activate-segment-streaming-destinations.md#review)
* [Activer les données d’audience vers des destinations d’exportation de profils de diffusion en continu](./ui/activate-streaming-profile-destinations.md#review)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](./ui/activate-batch-profile-destinations.md#review)

## Conditions générales {#terms-and-conditions}

En utilisant l’une des destinations libellées comme étant en version Beta (« Beta »), vous reconnaissez que le Beta est fourni ***« en l’état », sans garantie d’aucune sorte***.

Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge cette version Beta. Il est conseillé d’utiliser le Beta et/ou les éléments qui l’accompagnent pour vous informer et de ne pas vous fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce dernier. La version Beta est considérée comme étant une information confidentielle dʼAdobe.

Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

Envoyez vos commentaires ou créez un ticket dʼassistance pour partager vos suggestions, signaler un bug ou demander une amélioration de fonctionnalité.