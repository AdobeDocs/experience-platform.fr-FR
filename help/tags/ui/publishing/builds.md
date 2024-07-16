---
title: Versions
description: Découvrez le concept des builds et leur fonctionnement dans Adobe Experience Platform.
exl-id: af899282-aa2d-4395-8dbd-18d91be3f041
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 100%

---

# Versions

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une version est l’ensemble de fichiers contenant tout le code qui s’exécute sur l’appareil du client.

Il s’agit d’un ensemble des modifications que vous avez spécifiées dans votre bibliothèque, ainsi que de tout ce qui a été soumis, approuvé ou publié auparavant.

La version se compose de fichiers de code côté client qui se font référence les uns aux autres. Ces fichiers sont transférés vers votre emplacement d’hébergement à l’aide de l’environnement et de l’hôte que vous avez choisis pour la bibliothèque. Le code que vous déployez sur votre site désigne ce même emplacement afin que les fichiers puissent se charger lorsqu’un utilisateur accède à votre site ou à votre application.

## Contenu du fichier

Une bibliothèque définit un ensemble distinct de ressources de balise (extensions, règles et éléments de données) qui doivent y être incluses.

Une version contient tout le code du module (fourni par les développeurs d’extensions) et la configuration (que vous avez entrée) nécessaire pour alimenter les ressources contenues dans la bibliothèque. Par exemple, si une extension fournit des actions qui ne sont pas utilisées dans vos règles, le code permettant d’effectuer ces actions n’est pas contenu dans la version.

Les versions se composent du fichier de bibliothèque principal et potentiellement de nombreux fichiers plus petits. Le fichier de bibliothèque principal est référencé dans votre code intégré et chargé sur la page au moment de l’exécution. Il contient les éléments suivants :

* Le moteur de règles
* L’intégralité de la configuration de l’extension
* L’intégralité de la configuration et du code d’élément de données
* L’intégralité de la configuration et du code d’événement de règle
* L’intégralité de la configuration et du code de condition
* Le code d’événement et la configuration pour toutes les règles qui ont pour événement Library Loaded (Bibliothèque chargée) ou Page Bottom (Bas de page) (puisque nous savons que nous en aurons besoin tout de suite).

Les plus petits fichiers contiennent du code et une configuration pour des actions individuelles chargées sur la page, le cas échéant. Lorsqu’une règle est déclenchée et que ses conditions sont évaluées de telle sorte que les actions doivent être exécutées, le code et la configuration nécessaires pour cette action spécifique sont récupérés depuis l’un des fichiers les plus petits. Cela signifie que seul le code nécessaire pour effectuer les actions nécessaires est chargé sur la page, rendant ainsi la bibliothèque principale aussi petite que possible.

## Format du fichier

Le format du fichier par défaut des versions est un ensemble de fichiers contenant tout le code requis pour que vos extensions, vos éléments de données et vos règles s’exécutent comme vous le souhaitez.

Cependant, dans certains cas, vous préférez peut-être une archive .zip des fichiers plutôt que le fichier de code côté client exécutable. Par exemple, vous pouvez créer une archive si vous hébergez vous-même votre version et si souhaitez l’utiliser dans un autre déploiement. Si vous fournissez des données dans le chemin d’accès d’auto-hébergement du champ de la bibliothèque, vous pouvez enregistrer votre environnement. Avec votre nouveau code, un lien d’accès au téléchargement archivé est mis à disposition. Une fois la bibliothèque créée, vous avez la possibilité de déployer un fichier zip sur Akamai et de le télécharger à partir de `assets.adobedtm.com/...`.

>[!NOTE]
>
>Cet emplacement ne contient rien jusqu’à ce que vous ayez créé une version.

Quel que soit le format de fichier, la version est toujours fournie à l’emplacement spécifié par l’hôte.

Pour terminer une version, sélectionnez une bibliothèque et cliquez sur l’option Version disponible à ce niveau du processus de publication (Créer à des fins de développement, Créer à des fins d’évaluation, etc.)

## Minimisation

La minimisation réduit les coûts liés à la bande passante et améliore la vitesse en supprimant les données inutiles à l’exécution depuis un fichier.

Pour accroître les performances, Platform minimise tout, notamment les éléments suivants :

* La bibliothèque Balise principale
* Le code de module fourni par les développeurs d’extensions dans le cadre d’une extension
* Le code personnalisé fourni par les utilisateurs de Platform 

>[!NOTE]
>
>Si votre code de module et le code personnalisé sont déjà minimisés, Platform les minimise à nouveau. Cette seconde minimisation ne procure pas d’avantages supplémentaires, mais elle n’entraîne aucun dommage, tout en rendant Platform moins complexe et plus facile à gérer.

Tout code côté client fourni pointe vers la version miniaturisée du code. Cela est visible dans les noms de fichiers qui sont conformes à la convention de dénomination standard pour les fichiers miniaturisés :

`launch-%environment_id%.min.js`

Si vous souhaitez afficher le code non miniaturisé, supprimez .min du nom de fichier :

`launch-%environment_id%.js`

Si un développeur d’extensions fournit du code miniaturisé avec son extension, Platform ne fournit pas de code non miniaturisé dans la version non miniaturisée. De même, si un utilisateur de Platform place un code miniaturisé dans une zone de code personnalisé, ce code est toujours miniaturisé dans des versions non miniaturisées. Platform n’empêche aucune miniaturisation.

Pour plus d’informations sur la miniaturisation, voir [cet article de chemin d’empilement](https://blog.stackpath.com/glossary/minification/).

Lors de la génération d’une version, Platform crée d’abord la bibliothèque non miniaturisée, puis la miniaturise entièrement en une fois.
