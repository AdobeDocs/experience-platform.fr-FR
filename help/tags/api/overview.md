---
title: Guide de lʼAPI Reactor
description: L’API Reactor permet aux développeurs de gérer toutes les ressources de balises par programme dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 97%

---

# Guide de l’API [!DNL Reactor]

L’API Reactor fournit plusieurs points d’entrée qui vous permettent de gérer toutes les ressources de balises par programme dans Adobe Experience Platform.

Ces points d’entrée sont décrits ci-dessous. Consultez les guides des différents points dʼentrée pour obtenir plus dʼinformations et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur la manière de vous authentifier auprès de lʼAPI.

Pour afficher tous les points dʼentrée et opérations CRUD disponibles, consultez la section [Informations de référence sur lʼAPI Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Sociétés

Une société représente lʼorganisation dʼun utilisateur de balises, généralement une entreprise. Ces sociétés correspondent à 1:1 avec les ID d’organisation. Les utilisateurs de l’API nʼauront une visibilité que sur les sociétés auxquelles ils ont accès.

Pour savoir comment afficher les sociétés disponibles dans lʼAPI, consultez le [guide du point dʼentrée des sociétés](./endpoints/companies.md).

## Propriétés

Une propriété est un conteneur qui contient la plupart des autres ressources disponibles dans lʼAPI Reactor. Les seules ressources qui ne sont pas détenues par une propriété sont les événements dʼaudit, les sociétés, les packages dʼextension et les profils. Une propriété appartient à une seule et unique société, mais une société peut posséder plusieurs propriétés.

Pour savoir comment gérer les propriétés dans lʼAPI, consultez le [guide du point dʼentrée des propriétés](./endpoints/properties.md).

## Éléments de données

Un élément de données fonctionne comme une variable qui pointe vers une donnée importante dans votre application. Les éléments de données sont utilisés dans les règles et les configurations dʼextension. Lorsque la règle est déclenchée au moment de lʼexécution dans un navigateur ou une application, la valeur de lʼélément de données est résolue et utilisée dans la règle.

Pour savoir comment gérer les éléments de données dans lʼAPI, consultez le [guide du point dʼentrée des éléments de données](./endpoints/data-elements.md).

## Règles

Les règles contrôlent le comportement des ressources contenues dans une bibliothèque déployée. Une règle regroupe un ou plusieurs composants de règle dans le but de les lier de manière logique.

Pour savoir comment gérer les règles dans lʼAPI, consultez le [guide du point dʼentrée des règles](./endpoints/rules.md).

## Composants de règle

Les composants de règle sont les éléments individuels constitutifs dʼune règle. Les composants de règle possèdent trois types de base :

* **Événements** : ce qui déclenche une règle
* **Conditions** : ce que la règle vérifie pour déterminer une action
* **Actions** : ce que la règle exécute selon que la condition est remplie ou non.

Pour savoir comment gérer les règles dans lʼAPI, consultez le [guide du point dʼentrée des règles](./endpoints/rules.md).

## Packages d’extension

Un package dʼextension représente un ensemble de fonctionnalités individuelles qui peuvent être mises à la disposition dʼun utilisateur de balises. La plupart du temps, ces fonctionnalités se présentent sous la forme de composants de règle et dʼéléments de données, mais peuvent également inclure des modules principaux et partagés. Les fonctionnalités fournies par un package dʼextension sont installées en tant quʼextension lorsquʼil est inclus dans une bibliothèque.

Pour savoir comment gérer les packages dʼextension dans lʼAPI, reportez-vous au [guide du point dʼentrée des packages dʼextension](./endpoints/extension-packages.md).

## Extensions

Une extension représente lʼinstance installée dʼun package dʼextension. Une extension permet de rendre disponibles pour une propriété les fonctionnalités définies par un package dʼextension. Ces fonctionnalités sont utiles lors de la création dʼéléments de données et de composants de règle.

Pour savoir comment gérer les extensions dans lʼAPI, consultez le [guide du point dʼentrée des extensions](./endpoints/extensions.md).

## Bibliothèques

Une bibliothèque est une collection de ressources (extensions, règles et éléments de données) qui représente le comportement souhaité dʼune propriété. Les bibliothèques sont compilées dans des versions, qui sont affectées à différents environnements à mesure de leur progression dans le flux de publication, du test à la production.

Pour savoir comment gérer les bibliothèques dans lʼAPI, consultez le [guide du point dʼentrée des bibliothèques](./endpoints/libraries.md).

## Versions

Une bibliothèque de balises est compilée dans une version afin dʼêtre affectée à un environnement à des fins de test et de déploiement. Le contenu dʼune version varie en fonction des ressources incluses dans la bibliothèque, de la configuration de lʼenvironnement auquel elle est affectée et de la plateforme de la propriété à laquelle elle appartient.

Consultez le [guide du point dʼentrée des versions](./endpoints/builds.md) pour savoir comment gérer les versions dans lʼAPI.

## Environnements

Un environnement indique lʼhôte spécifique dans lequel une version peut être déployée, et si la version doit être déployée sous la forme dʼun ensemble de fichiers ou compressée dans un format dʼarchive. Dans lʼAPI Reactor, les environnements sont distincts des hôtes eux-mêmes, qui sont gérés par le point dʼentrée `/hosts`.

Consultez le [guide du point dʼentrée des versions](./endpoints/builds.md) pour savoir comment gérer les versions dans lʼAPI.

## Hôtes

Un hôte représente une destination hébergée dans lequel une version de bibliothèque peut être diffusée et finalement déployée. Les hôtes peuvent être des serveurs Akamai ou SFTP.

Pour savoir comment gérer les hôtes dans lʼAPI, consultez le [guide du point dʼentrée des hôtes](./endpoints/hosts.md).

## Configurations d’application

Les configurations dʼapplication permettent de stocker et de récupérer les informations dʼidentification en vue dʼune utilisation ultérieure. Pour savoir comment gérer les configurations dʼapplication dans lʼAPI, consultez le [guide du point dʼentrée des configurations dʼapplication](./endpoints/app-configurations.md).

## Événements d’audit

Un événement dʼaudit est un enregistrement dʼune modification spécifique apportée à une autre ressource de balise, générée au moment de la modification. Il sʼagit dʼévénements système auxquels vous pouvez souscrire à lʼaide dʼune fonction de rappel.

Pour savoir comment gérer les événements dʼaudit dans lʼAPI, reportez-vous au [guide du point dʼentrée des événements dʼaudit](./endpoints/audit-events.md).

## Rappels

Un rappel est un message qu’Experience Platform envoie à un hôte d’URL chaque fois qu’un nouvel événement d’audit est généré. Pour savoir comment gérer les rappels dans lʼAPI, consultez le [guide du point dʼentrée des rappels](./endpoints/callbacks.md).

## Notes

Les notes sont des annotations textuelles que vous pouvez ajouter à certaines ressources de balise, telles que les éléments de données, les extensions, les bibliothèques, les propriétés, les règles et les composants de règle. Pour savoir comment gérer les notes dans lʼAPI, consultez le [guide du point dʼentrée des notes](./endpoints/notes.md).

## Profile

Un profil contient toutes les informations sur lʼutilisateur connecté, y compris toutes les organisations Adobe auxquelles il appartient, les profils de produits auxquels il appartient dans chaque organisation et les droits dont il dispose pour chaque profil de produit.

Pour savoir comment afficher ces informations dans lʼAPI, consultez le [guide du point dʼentrée de profil](./endpoints/profile.md).

## Recherche

Le point dʼentrée `/search` permet de trouver des ressources correspondant à un critère donné, exprimé sous la forme dʼune requête. Toutes les requêtes sont limitées à votre société actuelle et aux propriétés accessibles. Pour savoir comment utiliser cette fonctionnalité, consultez le [guide du point dʼentrée de recherche](./endpoints/search.md).

## Secrets

Un secret contient des informations d’identification qui permettent au transfert d’événements de s’authentifier sur un autre système pour un échange de données sécurisé. Voir le [guide des secrets](./guides/secrets.md) pour une présentation du fonctionnement des secrets dans le transfert d’événements et le [guide des points d’entrée des secrets](./endpoints/secrets.md) pour apprendre à les gérer dans l’API Reactor.

## Étapes suivantes

Pour commencer à effectuer des appels à lʼaide de lʼAPI Schema Registry, consultez le [guide de prise en main](./getting-started.md), puis sélectionnez lʼun des guides des points dʼentrée pour savoir comment utiliser des points dʼentrée spécifiques.
