---
keywords: Experience Platform ; accueil ; rubriques populaires ; Adobe Experience Platform ; guide d’api ; guide d’api de la plate-forme ; présentation de la plate-forme ; guide du développeur
solution: Experience Platform
title: Postman à Adobe Experience Platform
topic: api guide
description: Ce document décrit la procédure à suivre pour configurer un environnement Postman, importer des collections Postman et une liste des collections disponibles pour chaque service Platform.
translation-type: tm+mt
source-git-commit: effc8fef666ffbf62c2e0874d048245f19c12111
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Postman à Adobe Experience Platform

Postman est une plateforme de collaboration pour le développement d&#39;API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d&#39;API, de rationaliser les demandes CRUD, etc. La plupart des services d’API de plate-forme disposent de collections Postman qui peuvent être utilisées pour faciliter les appels d’API.

## Configuration d&#39;un environnement Postman pour Experience Platform

Le guide vidéo suivant décrit la création et la configuration de votre environnement Postman. Un environnement Postman contient tous les en-têtes requis pour effectuer des appels d&#39;API aux différentes collections fournies ci-dessous. Une fois configurée, chaque fois qu’une valeur arrive à expiration (par exemple `ACCESS_TOKEN`), vous pouvez mettre à jour la valeur actuelle dans l’environnement et cette nouvelle valeur est utilisée dans toutes vos collections.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Collections Postman {#collections}

Un dossier contenant toutes les collections Postman disponibles est accessible en visitant les [exemples Postman Experience Platform de GitHub repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Vous pouvez également trouver un lien de collecte Postman dans chaque fichier swagger individuel dans la [documentation de référence de l&#39;API](http://www.adobe.com/go/platform-api-reference-en) sur l&#39;Adobe I/O.

Pour télécharger une collection Postman, sélectionnez **[!DNL Raw]** dans la page GitHub pour charger le fichier JSON brut dans un nouvel onglet. Cliquez ensuite avec le bouton droit de la souris et sélectionnez **[!DNL Save as]** pour enregistrer le fichier vers une destination locale de votre choix.

![JSON brut](./images/api-guide/raw-collection.PNG)

## Importer une collection Postman {#import}

Pour utiliser une collection [Postman](#collections), vous devez configurer un environnement. Une fois que vous avez terminé la configuration de votre environnement, sélectionnez le sélecteur **[!DNL Manage Environments]** dans le coin supérieur droit.

![gérer le sélecteur d’environnements](./images/api-guide/environment-selector.png)

Une fenêtre contextuelle s’affiche et affiche tous vos environnements actuels. Pour importer une collection, sélectionnez **[!DNL import]**.

![bouton d’importation](./images/api-guide/import-collection.png)

Vous êtes invité à choisir un fichier à importer. Sélectionnez le fichier de collection Postman à importer. Une fois sélectionnée, la collection est renseignée dans le rail de gauche sous l’onglet Collections.

![collection renseignée](./images/api-guide/imported-collection.png)

Chaque collection comporte différentes paires clé-valeur qui peuvent être nécessaires pour effectuer une opération CRUD réussie. Consultez le [guide du développeur d&#39;API](api-guide.md#api-guides) du service pour en savoir plus sur les valeurs requises, des conseils et des exemples.

Pour en savoir plus sur l&#39;interface utilisateur de Postman et ses fonctionnalités disponibles, consultez la [documentation de Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Générer un jeton d&#39;accès avec Postman pour une utilisation autre que la production

>[!WARNING]
>
>Comme l&#39;indique la collection Postman de la génération de jetons d&#39;accès d&#39;Adobes I/O, les méthodes de génération indiquées sont adaptées à **utilisation sans production**. La signature locale charge une bibliothèque JavaScript à partir d’un hôte tiers et la signature à distance envoie la clé privée à un service Web détenu et exploité par Adobe. Bien que l’Adobe ne stocke pas cette clé privée, les clés de production ne doivent jamais être partagées avec quiconque.

La vidéo ci-dessous utilise la [collection de génération de jetons d&#39;accès d&#39;Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) qui peut être téléchargée à partir du référentiel GitHub public.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Étapes suivantes

Ce document présente les environnements Postman, les collections et comment importer les collections. Maintenant que Postman est prêt, consultez le [Guide de prise en main de la plate-forme](api-guide.md) pour plus d&#39;informations sur les en-têtes, les exemples et la liste de [guides d&#39;API](api-guide.md#api-guides) disponibles pour chaque service de plate-forme.