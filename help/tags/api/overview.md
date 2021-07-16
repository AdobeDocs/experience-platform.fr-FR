---
title: Guide de l’API Reactor
description: L’API Reactor permet aux développeurs de gérer par programmation toutes les ressources pour les balises dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 3%

---

# Guide de l’API [!DNL Reactor]

L’API Reactor fournit plusieurs points de terminaison qui vous permettent de gérer par programmation toutes les ressources pour les balises dans Adobe Experience Platform.

Ces points d’entrée sont décrits ci-dessous. Consultez les guides des différents points de terminaison pour plus d’informations et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur la manière de vous authentifier à l’API.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez la [référence de l’API Reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml).

## Sociétés

Une entreprise représente l’organisation d’un utilisateur de balises, généralement une entreprise. Ces sociétés correspondent à 1:1 avec les identifiants de l’organisation IMS. Les utilisateurs d’API n’auront de visibilité que sur les entreprises auxquelles ils ont accès.

Consultez le [guide de point de terminaison des entreprises](./endpoints/companies.md) pour savoir comment afficher les entreprises disponibles dans l’API.

## Propriétés

Une propriété est un conteneur qui contient la plupart des autres ressources disponibles dans l’API Reactor. Les seules ressources qui ne sont pas détenues par une propriété sont les événements de contrôle, les entreprises, les packages d’extension et les profils. Une propriété appartient exactement à une seule société et une société peut avoir plusieurs propriétés.

Pour savoir comment gérer les propriétés dans l’API, consultez le [guide de point d’entrée des propriétés](./endpoints/properties.md) .

## Éléments de données

Un élément de données fonctionne comme une variable qui pointe vers un élément de données important dans votre application. Les éléments de données sont utilisés dans les règles et les configurations d’extension. Lorsque la règle est déclenchée au moment de l’exécution dans un navigateur ou une application, la valeur de l’élément de données est résolue et utilisée dans la règle.

Pour savoir comment gérer les éléments de données dans l’API, consultez le [guide de point de terminaison des éléments de données](./endpoints/data-elements.md) .

## Règles

Les règles contrôlent le comportement des ressources contenues dans une bibliothèque déployée. Une règle est un groupe d’un ou de plusieurs composants de règle et existe pour lier les composants de règle de manière logique.

Pour savoir comment gérer les règles dans l’API, consultez le [guide de point de terminaison des règles](./endpoints/rules.md) .

## Composants de  règle

Les composants de règle sont les éléments individuels qui constituent une règle. Les composants de règle ont trois types de base :

* **Événements** : Ce qui déclenche une règle
* **Conditions** : Vérification de la règle pour déterminer une action
* **Actions** : Exécution de la règle selon si la condition est remplie

Pour savoir comment gérer les règles dans l’API, consultez le [guide de point de terminaison des règles](./endpoints/rules.md) .

## Packages d’extension

Un package d’extension représente un groupe de fonctionnalités individuelles qui peuvent être mises à la disposition d’un utilisateur de balises. La plupart du temps, ces fonctionnalités se présentent sous la forme de composants de règle et d’éléments de données, mais peuvent également inclure des modules principaux et des modules partagés. Les fonctionnalités fournies par un package d’extension sont installées en tant qu’extension lorsqu’elle est incluse dans une bibliothèque.

Pour savoir comment gérer les modules d’extension dans l’API, reportez-vous au [guide de point d’entrée des modules d’extension](./endpoints/extension-packages.md) .

## Extensions

Une extension représente l’instance installée d’un package d’extension. Une extension rend les fonctionnalités définies par un package d’extension disponibles pour une propriété. Ces fonctionnalités sont exploitées lors de la création d’éléments de données et de composants de règle.

Pour savoir comment gérer les extensions dans l’API, consultez le [guide de point d’entrée des extensions](./endpoints/extensions.md) .

## Bibliothèques

Une bibliothèque est un ensemble de ressources (extensions, règles et éléments de données) qui représente le comportement souhaité d’une propriété. Les bibliothèques sont compilées dans des versions, qui sont affectées à différents environnements lorsqu’elles passent du test à la production.

Pour savoir comment gérer les bibliothèques dans l’API, consultez le [guide de point d’entrée des bibliothèques](./endpoints/libraries.md) .

## Versions

Une bibliothèque de balises est compilée dans une version afin d’être affectée à un environnement à des fins de test et de déploiement. Le contenu d’une version varie en fonction des ressources incluses dans la bibliothèque, de la configuration de l’environnement auquel elle est affectée et de la plateforme de la propriété à laquelle elle appartient.

Consultez le [guide de point de terminaison des versions](./endpoints/builds.md) pour savoir comment gérer les versions dans l’API.

## Environnements

Un environnement indique l’hôte spécifique sur lequel une version peut être déployée et si la version doit être déployée sous la forme d’un ensemble de fichiers ou compressée dans un format d’archive. Dans l’API Reactor, les environnements sont distincts des hôtes eux-mêmes, qui sont gérés par le point de terminaison `/hosts`.

Consultez le [guide de point de terminaison des versions](./endpoints/builds.md) pour savoir comment gérer les versions dans l’API.

## Hôtes

Un hôte représente une destination hébergée où une version de bibliothèque peut être diffusée et finalement déployée. Les hôtes peuvent être des serveurs Akamai ou SFTP.

Pour savoir comment gérer les hôtes dans l’API, consultez le [guide de point de terminaison hosts](./endpoints/hosts.md) .

## Configurations d’application

Les configurations d’application permettent de stocker et de récupérer les informations d’identification en vue d’une utilisation ultérieure. Voir le [guide de point d’entrée des configurations d’application](./endpoints/app-configurations.md) pour savoir comment gérer les configurations d’application dans l’API.

## Événements d’audit

Un événement d’audit est un enregistrement d’une modification spécifique apportée à une autre ressource de balise, générée au moment de la modification. Il s’agit d’événements système auxquels vous pouvez vous abonner à l’aide d’une fonction de rappel.

Pour savoir comment gérer les événements de contrôle dans l’API, reportez-vous au [guide de point de terminaison des événements de contrôle](./endpoints/audit-events.md) .

## Rappels

Un rappel est un message que Platform envoie à un hôte d’URL chaque fois qu’un nouvel événement d’audit est généré. Pour savoir comment gérer les rappels dans l’API, consultez le [guide de point de terminaison des rappels](./endpoints/callbacks.md) .

## Notes

Les notes sont des annotations textuelles que vous pouvez ajouter à certaines ressources de balise, telles que les éléments de données, les extensions, les bibliothèques, les propriétés, les règles et les composants de règle. Pour savoir comment gérer les notes dans l’API, consultez le [guide de point de fin de notes](./endpoints/notes.md) .

## Profile

Un profil contient toutes les informations sur l’utilisateur connecté, y compris toutes les organisations d’Adobe auxquelles il appartient, les profils de produit auxquels il appartient dans chaque organisation et les droits qu’il a de chaque profil de produit.

Consultez le [guide de point de terminaison de profil](./endpoints/profile.md) pour savoir comment afficher ces informations dans l’API.

## Recherche

Le point de terminaison `/search` permet de trouver des ressources correspondant à un critère souhaité, exprimé sous la forme d’une requête. Toutes les requêtes sont incluses dans votre société actuelle et les propriétés accessibles. Consultez le [guide de point de terminaison de recherche](./endpoints/search.md) pour découvrir comment utiliser cette fonctionnalité.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API Schema Registry, lisez le [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides de point de terminaison pour savoir comment utiliser des points de terminaison spécifiques.
