---
title: Prise en main du développement des extensions
description: Commencez à développer vos propres extensions de balises dans Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 73%

---

# Prise en main du développement des extensions

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
* Platform - Indique si l’extension est développée pour le web, le mobile ou Edge
* Version : version de l’extension
* Description : brève description de l’objet de l’extension
* Auteur : nom de l’auteur de l’extension

>[!NOTE]
> Pour les extensions mobiles, plusieurs questions seront posées concernant la structure de vos applications Android et iOS.

L’outil de génération de modèles automatique fournit ensuite des options pour la construction de la structure d’extension :

* [Vue de configuration de l’extension](./configuration.md) : la vue, fichier HTML, depuis laquelle une extension rassemble les paramètres globaux d’un utilisateur.
* [Types d’événement](./web/event-types.md) : définit une activité d’observation. Par exemple, savoir quand un utilisateur fait défiler rapidement une page ou quand un utilisateur a interagi avec un élément de page. Les événements peuvent ensuite être utilisés dans les règles pour exécuter des actions.
* [Types de condition](./web/condition-types.md) : les types de condition évaluent si un élément est vrai ou faux. Par exemple, elle peut renvoyer la valeur si le navigateur de l’utilisateur est Chrome, s’il utilise une iPad ou si l’utilisateur se trouve sur un domaine spécifique.
* [Types d’action](./web/action-types.md) : action à effectuer lorsqu’un événement se produit. Par exemple, envoyer une balise d’analyse, afficher une offre, enregistrer un cookie ou ouvrir une conversation d’assistance.
* [Types d’éléments de données](./web/data-element-types.md) : un type d’élément de données récupère une donnée. Cette donnée peut se trouver dans un enregistrement local, dans un cookie, dans un élément DOM ou dans un emplacement personnalisé.
* [Modules partagés](./web/shared.md) (web uniquement) : un module partagé est un mécanisme par lequel les extensions peuvent communiquer avec d’autres extensions.
* [Vues](./web/views.md) : chaque type d’événement, de condition, d’action ou d’élément de données peut fournir une vue permettant à un utilisateur de fournir des paramètres.
* URL Exchange (web et Edge uniquement) : lorsqu’une extension est publiée sur le catalogue public d’Adobe, fournissez l’URL de liste ici.
* Chemin d’accès à l’icône : chemin d’accès à un fichier d’icône pour l’extension.

>[!NOTE]
>
>* Les exécutions suivantes de l’outil de génération de modèles automatique ignorent la configuration initiale.
>* Plusieurs événements, conditions, actions peuvent être ajoutés.
>* Une seule vue de configuration peut exister.

## Étapes suivantes

* Suivez le [Présentation du processus d’envoi](./submit/overview.md) et préparez-vous à [valider](./submit/upload-and-test.md#validate) et [télécharger](./submit/upload-and-test.md#integration) votre extension à des fins de test dans l’écosystème de balises.
