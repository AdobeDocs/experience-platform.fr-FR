---
title: Guide de l’API Reactor
description: L’API Reactor permet aux développeurs de gérer toutes les ressources de balises par programme dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: ht
source-wordcount: '1039'
ht-degree: 100%

---

# Guide de l’API [!DNL Reactor]

L’API Reactor fournit plusieurs points d’entrée qui vous permettent de gérer toutes les ressources de balises par programme dans Adobe Experience Platform.

Ces points d’entrée sont décrits ci-dessous. Consultez les guides des points d’entrée individuels pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur la manière de vous authentifier auprès de l’API.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez le document de [référence de l’API Reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml).

## Sociétés

Une société représente l’organisation d’un utilisateur de balises, généralement une entreprise. La correspondance de ces sociétés est de 1:1 avec les identifiants de l’organisation IMS. Les utilisateurs d’API n’auront de visibilité que sur les sociétés auxquelles ils ont accès.

Consultez le [guide des points d’entrée de sociétés](./endpoints/companies.md) pour savoir comment afficher les sociétés disponibles dans l’API.

## Propriétés

Une propriété est un conteneur qui contient la plupart des autres ressources disponibles dans l’API Reactor. Les seules ressources qui ne sont pas détenues par une propriété sont les événements d’audit, les sociétés, les packages d’extension et les profils. Une propriété appartient à une seule société exactement. Par ailleurs, une société peut avoir plusieurs propriétés.

Consultez le [guide des points d’entrée des propriétés](./endpoints/properties.md) pour savoir comment gérer les propriétés dans l’API.

## Éléments de données

Un élément de données fonctionne comme une variable qui pointe vers un élément de données important dans votre application. Les éléments de données sont utilisés dans les règles et les configurations d’extension. Lorsque la règle est déclenchée, au moment de l’exécution dans un navigateur ou une application, la valeur de l’élément de données est résolue et utilisée dans la règle.

Consultez le [guide des points d’entrée des éléments de données](./endpoints/data-elements.md) pour savoir comment gérer les éléments de données dans l’API.

## Règles

Les règles contrôlent le comportement des ressources contenues dans une bibliothèque déployée. Une règle correspond à un groupe d’un ou plusieurs composants de règle. Elle existe pour lier les composants de règle de manière logique.

Consultez le [guide des points d’entrée des règles](./endpoints/rules.md) pour savoir comment gérer les règles dans l’API.

## Composants de  règle

Les composants de règle sont les éléments individuels qui constituent une règle. Les composants de règle ont trois types de base :

* **Événements** : ce qui déclenche une règle
* **Conditions** : ce que vérifie la règle pour déterminer une action
* **Actions** : ce que la règle exécute, en fonction du respect de la condition

Consultez le [guide des points d’entrée de règles](./endpoints/rules.md) pour savoir comment gérer les règles dans l’API.

## Packages d’extension

Un package d’extension représente un groupement de fonctionnalités individuelles qui peuvent être mises à la disposition d’un utilisateur de balises. La plupart du temps, ces fonctionnalités se présentent sous la forme de composants de règle et d’éléments de données, mais peuvent également inclure des modules principaux et des modules partagés. Les fonctionnalités fournies par un package d’extension sont installées sous forme d’extension lorsque ce package est inclus dans une bibliothèque.

Consultez le [guide des points d’entrée de packages d’extension](./endpoints/extension-packages.md) pour savoir comment gérer les packages d’extension dans l’API.

## Extensions

Une extension représente l’instance installée d’un package d’extension. Une extension met à disposition les fonctionnalités définies par un package d’extension pour une propriété. Ces fonctionnalités sont exploitées lors de la création d’éléments de données et de composants de règle.

Consultez le [guide des points d’entrée d’extensions](./endpoints/extensions.md) pour savoir comment gérer les extensions dans l’API.

## Bibliothèques

Une bibliothèque est un ensemble de ressources (extensions, règles et éléments de données) qui représente le comportement souhaité d’une propriété. Les bibliothèques sont compilées dans des versions, lesquelles sont affectées à différents environnements lorsqu’elles descendent le flux de publication et passent du test à la production.

Consultez le [guide du point d’entrée des bibliothèques](./endpoints/libraries.md) pour savoir comment gérer les bibliothèques dans l’API.

## Versions

Une bibliothèque de balises est compilée dans une version afin d’être affectée à un environnement à des fins de test et de déploiement. Le contenu d’une version varie en fonction des ressources incluses dans la bibliothèque, de la configuration de l’environnement auquel elle est affectée et de la plateforme de la propriété à laquelle elle appartient.

Consultez le [guide du point d’entrée des versions](./endpoints/builds.md) pour savoir comment gérer les versions dans l’API.

## Environnements

Un environnement indique l’hôte spécifique sur lequel une version peut être déployée et si cette version doit être déployée sous la forme d’un ensemble de fichiers ou compressée dans un format d’archive. Dans l’API Reactor, les environnements sont distincts des hôtes eux-mêmes, lesquels sont gérés par le point d’entrée `/hosts`.

Consultez le [guide du point d’entrée des versions](./endpoints/builds.md) pour savoir comment gérer les versions dans l’API.

## Hôtes

Un hôte représente une destination hébergée dans laquelle une version de bibliothèque peut être diffusée et finalement déployée. Les hôtes peuvent être des serveurs Akamai ou SFTP.

Consultez le [guide du point d’entrée des hôtes](./endpoints/hosts.md) pour savoir comment gérer les hôtes dans l’API.

## Configurations des applications

Les configurations d’application permettent de stocker et de récupérer les informations d’identification en vue d’une utilisation ultérieure. Consultez le [guide du point d’entrée des configurations d’application](./endpoints/app-configurations.md) pour savoir comment gérer les configurations d’application dans l’API.

## Événements d’audit

Un événement d’audit correspond à l’enregistrement d’une modification spécifique apportée à une autre ressource de balise, généré au moment de la modification. Il s’agit d’événements système auxquels il est possible de s’abonner à l’aide d’une fonction de rappel.

Consultez le [guide du point d’entrée des événements d’audit](./endpoints/audit-events.md) pour savoir comment gérer les événements d’audit dans l’API.

## Rappels

Un rappel est un message que Platform envoie à un hôte d’URL chaque fois qu’un nouvel événement d’audit est généré. Consultez le [guide du point d’entrée des rappels](./endpoints/callbacks.md) pour savoir comment gérer les rappels dans l’API.

## Notes

Les notes sont des annotations textuelles que vous pouvez ajouter à certaines ressources de balise, telles que les éléments de données, les extensions, les bibliothèques, les propriétés, les règles et les composants de règle. Consultez le [guide du point d’entrée des notes](./endpoints/notes.md) pour savoir comment gérer les notes dans l’API.

## Profil

Un profil contient toutes les informations relatives à l’utilisateur connecté, y compris l’ensemble des organisations d’Adobe auxquelles il appartient, les profils de produit auxquels il appartient dans chaque organisation ainsi que les droits dont il dispose pour chaque profil de produit.

Consultez le [guide du point d’entrée des profils](./endpoints/profile.md) pour savoir comment afficher ces informations dans l’API.

## Recherche

Le point d’entrée `/search` permet de trouver des ressources correspondant à un critère souhaité, exprimé sous la forme d’une requête. Toutes les requêtes sont incluses dans votre société actuelle et les propriétés accessibles. Consultez le [guide du point d’entrée de recherche](./endpoints/search.md) pour découvrir comment utiliser cette fonctionnalité.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API Schema Registry, consultez le [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides de point d’entrée pour savoir comment utiliser des points d’entrée spécifiques.
