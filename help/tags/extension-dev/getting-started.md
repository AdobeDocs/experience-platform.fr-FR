---
title: Prise en main du développement des extensions
description: Commencez à développer vos propres extensions de balises dans Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 100%

---

# Prise en main du développement des extensions

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Pour vous aider à vous préparer à construire des extensions, nous utiliserons l’outil de génération de modèles automatique en open-source fourni par les ingénieurs Adobe pour créer les fichiers et la structure de fichiers nécessaires pour votre package d’extensions, afin que tout ce qu’il vous reste à faire soit la partie qui vous intéresse : écrire le code.

## Conditions préalables

* Installez [Node.js](https://nodejs.org/fr/download/).

## Configuration de l’extension

Créez un répertoire dans lequel vos fichiers d’extension seront installés.

```shell
mkdir example && cd example
```

Ce guide utilise l’outil de génération automatique de modèles d’extension pour élaborer la structure d’extension initiale afin que les développeurs puissent rapidement commencer à coder. Si vous le souhaitez, ce processus peut être effectué manuellement sans l’outil de génération de modèles automatique.

Exécutez l’outil de génération de modèles automatique.

```shell
npx @adobe/reactor-scaffold
```

L’outil de génération de modèles automatique vous invite à définir certaines options de configuration initiales comme suit :

* Nom d’affichage : nom visible de l’extension
* Version : version de l’extension
* Description : brève description de l’objet de l’extension
* Auteur : nom de l’auteur de l’extension

L’outil de génération de modèles automatique fournit ensuite des options pour la construction de la structure d’extension :

* [Vue de configuration de l’extension](./configuration.md) : la vue, fichier HTML, depuis laquelle une extension rassemble les paramètres globaux d’un utilisateur.
* [Types d’événement](./web/event-types.md) : définit une activité d’observation. Par exemple, savoir quand un utilisateur fait défiler rapidement une page ou quand un utilisateur a interagi avec un élément de page. Les événements peuvent ensuite être utilisés dans les règles pour exécuter des actions.
* [Types de condition](./web/condition-types.md) : les types de condition évaluent si un élément est vrai ou faux. Par exemple, le type de condition peut renvoyer si le navigateur de l’utilisateur est Chrome, s’il utilise un iPad ou s’il se trouve sur un domaine spécifique.
* [Types d’action](./web/action-types.md) : action à effectuer lorsqu’un événement se produit. Par exemple, envoyer une balise d’analyse, afficher une offre, enregistrer un cookie ou ouvrir une conversation d’assistance.
* [Types d’éléments de données](./web/data-element-types.md) : un type d’élément de données récupère une donnée. Cette donnée peut se trouver dans un enregistrement local, dans un cookie, dans un élément DOM ou dans un emplacement personnalisé.
* [Modules partagés](./web/shared.md) : un module partagé est un mécanisme par lequel les extensions peuvent communiquer avec d’autres extensions.
* [Vues](./web/views.md) : chaque type d’événement, de condition, d’action ou d’élément de données peut fournir une vue permettant à un utilisateur de fournir des paramètres.

>[!NOTE]
>
>* Les exécutions suivantes de l’outil de génération de modèles automatique ignorent la configuration initiale.
>* Plusieurs événements, conditions, actions peuvent être ajoutés.
>* Une seule vue de configuration peut exister.

