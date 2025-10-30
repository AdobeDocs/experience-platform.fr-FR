---
title: Paramètres d’exportation configurables et communs des destinations
description: Découvrez quels paramètres d’exportation des destinations sont configurables au niveau de la destination et lesquels sont fixes et impossibles à modifier.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 88%

---

# Paramètres d’exportation configurables et communs des destinations

Lorsque vous réfléchissez au comportement de l’exportation vers des destinations Experience Platform, vous devez tenir compte de trois niveaux distincts sur lesquels les configurations agissent.

* À un premier niveau, certains des paramètres liés au comportement d’exportation de profils et aux paramètres de configuration sont communs à toutes les destinations appartenant à un type de destination. Ces paramètres se rapportent à ce qui déclenche une exportation de destination et à ce qui est inclus dans une exportation et ne peut pas être modifié par les développeurs et développeuses de destinations ou les utilisateurs et utilisatrices de Real-Time CDP.
* À un deuxième niveau, certains paramètres peuvent être personnalisés à un niveau de destination par le développeur ou la développeuse de destinations lors de la création de destinations à l’aide de Destination SDK.
* À un troisième niveau, il existe des paramètres de configuration que les utilisateurs de Real-Time CDP peuvent définir dans les workflows d’activation.

![Diagramme montrant l’interaction entre les paramètres d’exportation communs et configurables pour les destinations](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Cette page fournit des liens vers tous les paramètres d’exportation communs et configurables pour les destinations ou les décrit, aux trois niveaux présentés ci-dessus.

## Paramètres d’exportation communs pour les types de destination {#common-settings-across-destination-types}

Le comportement d’exportation de destination est cohérent sur toutes les destinations appartenant à un type de destination concernant *ce qui déclenche une exportation de destination* et *ce qui est inclus dans les exportations de destination*. Les exportations de destination sont déclenchées par des notifications que le service de destinations reçoit du [service Real-time Customer Profile en amont](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=fr#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Ce qui est inclus dans les exportations de destination varie légèrement d’un type de destination à l’autre. En savoir plus sur les [modèles communs de comportement d’exportation par type de destination](/help/destinations/how-destinations-work/profile-export-behavior.md). Ces paramètres ne peuvent pas être modifiés par les développeurs et développeuses de destinations ou les utilisateurs et utilisatrices de Real-Time CDP.

## Paramètres d’exportation personnalisables par les développeurs et développeuses de destinations {#customizable-settings-by-destination-developers}

Les développeurs et développeuses de destinations peuvent utiliser [Destination SDK](/help/destinations/destination-sdk/overview.md) pour créer des destinations personnalisées ou mises en production (privées ou publiques). Destination SDK offre aux développeurs et aux développeuses une grande flexibilité pour configurer des destinations en fonction des fonctionnalités en aval de leurs points d’entrée d’API et de leurs systèmes de réception de fichiers. En fonction des fonctionnalités en aval, les développeurs et développeuses de destinations disposent, lors de la configuration d’une destination à l’aide de Destination SDK, des options de configuration suivantes :

* Déterminer les identités et les attributs pouvant être exportés hors d’Experience Platform vers la destination. Déterminer également les identités requises par leurs destinations pour une exportation réussie des données.
* Définir une politque d’agrégation qui détermine la durée pendant laquelle Experience Platform doit attendre lors de l’agrégation des messages HTTP à envoyer aux intégrations d’API. Les développeurs et développeuses de destinations peuvent configurer différents types d’agrégation pour déterminer le nombre de profils à inclure dans les messages HTTP sortants et la durée pendant laquelle Experience Platform doit attendre jusqu’à la distribution du message HTTP. Obtenez des informations détaillées sur les [options de configuration des politiques d’agrégation](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) disponibles pour les développeurs et développeuses de destinations dans la documentation de Destination SDK.
* Déterminer si les exportations de messages HTTP doivent inclure les profils qui remplissent les critères pour les segments, qui sont supprimés des segments, ou les deux.
* Déterminer les configurations de nom et de mise en forme des fichiers qui doivent être disponibles pour les utilisateurs et utilisatrices lors de l’exportation de fichiers.

## Paramètres au niveau d’un flux de données personnalisables par les utilisateurs et les utilisatrices {#settings-on-dataflow-level}

Outre les paramètres non modifiables qui dépendent du type de destination et les paramètres configurés par le développeur ou la développeuse de destination, il existe certains paramètres d’exportation que les utilisateurs et utilisatrices peuvent configurer dans le workflow d’activation. Ces paramètres concernent le planning d’exportation d’un certain flux de données vers une destination, les attributs et les champs d’identité qui doivent être exportés dans un flux de données ou les options de formatage des fichiers pour les fichiers exportés.

Les paramètres disponibles pour les utilisateurs et utilisatrices lors de la connexion à une destination dépendent de la manière dont la destination a été configurée par le développeur ou la développeuse de destination et des paramètres mis à la disposition des utilisateurs et utilisatrices.

Par exemple, pour les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations), un développeur ou une développeuse de destination peut configurer les identités que sa destination accepte et seules ces identités seront affichées pour l’utilisateur ou l’utilisatrice dans l’[étape de mappage du workflow d’activation](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), comme illustré ci-dessous :

![Enregistrement de l’écran de sélection de l’identité pour le champ cible dans l’étape de mappage du workflow d’activation.](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

De même, pour les[destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based), le développeur ou la développeuse de destination peut déterminer quelles [options d’ajout de nom de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) rendre disponibles pour sa destination, ou quelles [options de formatage de fichier](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) rendre disponibles et l’utilisateur ou l’utilisatrice pourra sélectionner uniquement l’une de ces options, comme illustré ci-dessous :

![Enregistrement de l’écran de l’option de formatage de fichier lors de la connexion à une destination basée sur des fichiers.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Enregistrement de l’écran de l’option d’ajout de nom de fichier à l’étape de planification du workflow d’activation.](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

En savoir plus sur les différentes options et étapes disponibles dans le workflow d’activation :

* [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Activer les données d’audience vers les destinations d’entreprise](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exporter des fichiers à la demande vers des destinations par lots](/help/destinations/ui/export-file-now.md)
* [Exporter des jeux de données vers des destinations d’espace de stockage](/help/destinations/ui/export-datasets.md)

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez désormais quels paramètres d’exportation des destinations sont communs à tous les types de destination, lesquels peuvent être configurés par les développeurs et développeuses à un niveau de destination spécifique, et quels paramètres peuvent être modifiés par les utilisateurs et utilisatrices dans le processus d’activation.

Vous pouvez ensuite lire des informations plus détaillées sur les [modèles communs de comportement d’exportation par type de destination](/help/destinations/how-destinations-work/profile-export-behavior.md).

Pour les développeurs et développeuses de destinations, vous pouvez : [commencer](/help/destinations/destination-sdk/getting-started.md) avec Destination SDK. Pour les utilisateurs et utilisatrices qui souhaitent activer des données, vous pouvez extraire toutes les destinations disponibles dans le [catalogue](/help/destinations/catalog/overview.md).
