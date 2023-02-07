---
title: Paramètres d’exportation configurables et communs des destinations
description: Découvrez les paramètres d’exportation des destinations configurables au niveau de la destination, fixes et impossibles à modifier.
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 2%

---


# Paramètres d’exportation configurables et communs des destinations

Lorsque vous réfléchissez au comportement de l’exportation vers des destinations Experience Platform, vous devez tenir compte de trois niveaux distincts sur lesquels les configurations agissent.

* À un premier niveau, certains des paramètres liés au comportement d’exportation de profils et aux paramètres de configuration sont communs à toutes les destinations appartenant à un type de destination. Ces paramètres se rapportent à ce qui déclenche un export de destination et à ce qui est inclus dans un export et ne peuvent pas être modifiés par les développeurs de destination ou les utilisateurs de la plateforme de données clients en temps réel.
* À un second niveau, certains paramètres peuvent être personnalisés à un niveau de destination par le développeur de destination lors de la création de destinations à l’aide de Destination SDK.
* À un troisième niveau, il existe des paramètres de configuration que les utilisateurs de la plateforme de données clients en temps réel peuvent définir dans les workflows d’activation.

![Diagramme montrant l’interaction entre les paramètres d’exportation communs et configurables pour les destinations](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Cette page décrit ou fournit des liens vers tous les paramètres d’exportation communs et configurables pour les destinations, aux trois niveaux décrits ci-dessus.

## Paramètres d’exportation courants pour les types de destination {#common-settings-across-destination-types}

Le comportement de l’exportation de destination est cohérent entre les destinations appartenant à un type de destination en ce qui concerne *ce qui déclenche une exportation de destination* et *qui est inclus dans les exportations de destination*. Les exportations de destination sont déclenchées par des notifications que le service de destinations reçoit de la [service Real-time Customer Profile en amont](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Ce qui est inclus dans les exportations de destination varie légèrement d’un type de destination à l’autre. En savoir plus sur les [modèles de comportement d’exportation courants par type de destination](/help/destinations/how-destinations-work/profile-export-behavior.md). Ces paramètres ne peuvent pas être modifiés par les développeurs de destination ou les utilisateurs de la plateforme de données clients en temps réel.

## Paramètres d’exportation personnalisables par les développeurs de destination {#customizable-settings-by-destination-developers}

Les développeurs de destinations peuvent utiliser [Destination SDK](/help/destinations/destination-sdk/overview.md) pour créer des destinations personnalisées ou productives (privées ou publiques). Destination SDK offre aux développeurs une grande flexibilité pour configurer des destinations en fonction des fonctionnalités en aval de leurs points de terminaison d’API et de leurs systèmes de réception de fichiers. En fonction des fonctionnalités en aval, les développeurs de destinations disposent des options de configuration suivantes lors de la configuration d’une destination à l’aide de Destination SDK :

* Déterminez les attributs et les identités pouvant être exportés hors Experience Platform vers la destination. Déterminez également les identités requises par leurs destinations pour une exportation réussie des données.
* Définissez une stratégie d’agrégation qui détermine la durée pendant laquelle l’Experience Platform doit attendre lors de l’agrégation des messages HTTP à envoyer aux intégrations API. Les développeurs de destinations peuvent configurer différents types d’agrégation pour déterminer le nombre de profils à inclure dans les messages HTTP sortants et la durée pendant laquelle l’Experience Platform doit attendre jusqu’à la distribution du message HTTP. Obtenez des informations détaillées sur la variable [options de configuration des stratégies d’agrégation](/help/destinations/destination-sdk/destination-configuration.md#aggregation) disponibles pour les développeurs de destination dans la documentation de la Destination SDK.
* Déterminez si les exportations de messages HTTP doivent inclure les profils qui remplissent les critères pour les segments, qui sont supprimés des segments, ou les deux.
* Déterminez les configurations de nom de fichier et de mise en forme de fichier qui doivent être disponibles pour les utilisateurs lors de l’exportation de fichiers.

## Paramètres au niveau d’un flux de données personnalisables par les utilisateurs {#settings-on-dataflow-level}

Outre les paramètres non modifiables qui dépendent du type de destination et des paramètres configurés par le développeur de destination, il existe certains paramètres d’exportation que les utilisateurs peuvent configurer dans le workflow d’activation. Ces paramètres concernent le planning d’exportation d’un certain flux de données vers une destination, les attributs et les champs d’identité qui doivent être exportés dans un flux de données ou les options de formatage des fichiers pour les fichiers exportés.

Les paramètres disponibles pour les utilisateurs lors de la connexion à une destination dépendent de la manière dont la destination a été configurée par le développeur de destination et des paramètres qu’ils ont mis à la disposition des utilisateurs.

Par exemple, pour [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations), un développeur de destination peut configurer les identités que sa destination accepte et seules ces identités seront affichées pour l’utilisateur dans [étape de mappage du workflow d’activation](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), comme illustré ci-dessous :

![Enregistrement de l’écran de sélection de l’identité pour le champ cible dans l’étape de mappage du workflow d’activation. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

De même, pour [destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based), le développeur de destination peut déterminer lequel [options d’ajout du nom de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) ils veulent rendre disponible pour leur destination, ou laquelle [options de formatage de fichier](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) ils souhaitent rendre disponible et l’utilisateur pourra sélectionner uniquement l’une de ces options, comme illustré ci-dessous :

![Enregistrement de l’option de formatage de fichier lors de la connexion à une destination basée sur un fichier.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Enregistrement de l’écran de l’option d’ajout du nom de fichier à l’étape de planification du workflow d’activation. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

En savoir plus sur les différentes options et étapes disponibles dans le workflow d’activation :

* [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Activation des données d’audience vers les destinations d’entreprise](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportation de fichiers à la demande vers des destinations par lot](/help/destinations/ui/export-file-now.md)
* [(Version bêta) Exporter des jeux de données vers des destinations d’espace de stockage](/help/destinations/ui/export-datasets.md)

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez désormais quels paramètres d’exportation des destinations sont communs à tous les types de destination, lesquels peuvent être configurés par les développeurs à un niveau de destination spécifique, et quels paramètres peuvent être modifiés par les utilisateurs dans le processus d’activation.

Vous pouvez ensuite lire des informations plus détaillées sur la variable [modèles de comportement d’exportation courants par type de destination](/help/destinations/how-destinations-work/profile-export-behavior.md).

Pour les développeurs de destinations, vous pouvez : [prise en main](/help/destinations/destination-sdk/getting-started.md) avec Destination SDK. Pour les utilisateurs qui souhaitent activer des données, vous pouvez extraire toutes les destinations disponibles dans la variable [catalogue](/help/destinations/catalog/overview.md).