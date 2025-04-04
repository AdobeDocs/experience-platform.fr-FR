---
keywords: Experience Platform;accueil;rubriques populaires;Adobe Experience Platform;guide de l’api;guide de l’api platform;présentation de platform;guide du développeur
solution: Experience Platform
title: Postman dans Adobe Experience Platform
description: Ce document contient les étapes de configuration d’un environnement Postman, d’importation de collections Postman et d’une liste des collections disponibles pour chaque service Experience Platform.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Postman dans Adobe Experience Platform

Postman est une plateforme de collaboration pour le développement d’API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d’API, de rationaliser les requêtes CRUD, etc. La plupart des services d’API Experience Platform possèdent des collections Postman qui peuvent être utilisées pour faciliter l’émission d’appels d’API.

## Configuration d’un environnement Postman pour Experience Platform

Le guide vidéo suivant décrit la création et la configuration de votre environnement Postman. Un environnement Postman contient tous les en-têtes requis pour effectuer des appels API vers les différentes collections fournies ci-dessous. Une fois configurée, chaque fois qu’une valeur expire (par exemple, une `ACCESS_TOKEN`), vous pouvez mettre à jour la valeur actuelle dans l’environnement, et cette nouvelle valeur est utilisée dans toutes vos collections.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Collections Postman {#collections}

Vous trouverez un dossier contenant toutes les collections Postman disponibles en consultant le [référentiel GitHub d’exemples Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Vous pouvez également trouver un lien de collection Postman dans chaque fichier Swagger individuel dans la [documentation de référence de l’API](https://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

Pour télécharger une collection Postman, sélectionnez **[!DNL Raw]** dans la page GitHub pour charger le fichier JSON brut dans un nouvel onglet. Cliquez ensuite avec le bouton droit et sélectionnez **[!DNL Save as]** pour enregistrer le fichier vers une destination locale de votre choix.

![JSON brut](./images/api-guide/raw-collection.PNG)

## Importer une collection Postman {#import}

Pour utiliser une collection [Postman](#collections), vous devez avoir configuré un environnement. Une fois la configuration de l’environnement terminée, sélectionnez le sélecteur de **[!DNL Manage Environments]** dans le coin supérieur droit.

![gérer le sélecteur d’environnement](./images/api-guide/environment-selector.png)

Une fenêtre contextuelle s’affiche et affiche tous vos environnements actuels. Pour importer une collection, sélectionnez **[!DNL import]** .

![bouton importer](./images/api-guide/import-collection.png)

Vous êtes invité à choisir un fichier à importer. Sélectionnez le fichier de collection Postman à importer. Une fois sélectionnée, la collection est renseignée dans le rail de gauche sous l’onglet Collections .

![collection renseignée](./images/api-guide/imported-collection.png)

Chaque collection comporte différentes paires clé-valeur qui peuvent être nécessaires pour effectuer une opération CRUD réussie. Veuillez consulter le [guide du développement de l’API](api-guide.md#api-guides) du service pour en savoir plus sur les valeurs requises, obtenir des conseils et consulter des exemples.

Pour en savoir plus sur l’interface utilisateur de Postman et ses fonctionnalités disponibles, consultez la [documentation de Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Générer un jeton d’accès avec Postman pour une utilisation hors production

>[!WARNING]
>
>Comme indiqué dans la collection Postman du service Identity Management (IMS), les méthodes de génération mentionnées sont adaptées à une **utilisation hors production**. La signature locale charge une bibliothèque JavaScript à partir d’un hôte tiers et la signature à distance envoie la clé privée à un service web détenu et exploité par Adobe. Bien qu’Adobe ne stocke pas cette clé privée, les clés de production ne doivent jamais être partagées avec qui que ce soit.

La vidéo ci-dessous utilise la collection Postman [d’Identity Management Service (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) qui peut être téléchargée à partir du référentiel GitHub public.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Étapes suivantes

Ce document présente les environnements Postman, les collections et la manière d’importer des collections. Maintenant que Postman est prêt, consultez le [guide de prise en main d’Experience Platform](api-guide.md) pour plus d’informations sur les en-têtes requis, des exemples et une liste de [guides d’API](api-guide.md#api-guides) disponibles pour chaque service Experience Platform.
