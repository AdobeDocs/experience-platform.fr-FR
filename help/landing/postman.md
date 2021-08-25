---
keywords: Experience Platform;accueil;rubriques les plus consultées;Adobe Experience Platform;guide de l’api;guide de l’api de la plateforme;présentation de Platform;guide de développement
solution: Experience Platform
title: Postman dans Adobe Experience Platform
topic-legacy: api guide
description: Ce document décrit les étapes à suivre pour configurer un environnement Postman, importer des collections Postman et une liste des collections disponibles pour chaque service Platform.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: a0f4e49192a54075ce7c48620c9729e61ecdfdac
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Postman dans Adobe Experience Platform

Postman est une plateforme de collaboration pour le développement d’API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d’API, de rationaliser les requêtes CRUD, etc. La plupart des services d’API Platform disposent de collections Postman qui peuvent être utilisées pour faciliter les appels d’API.

## Configuration d’un environnement Postman pour Experience Platform

Le guide vidéo suivant décrit la création et la configuration de votre environnement Postman. Un environnement Postman contient tous les en-têtes requis pour effectuer des appels API vers les différentes collections fournies ci-dessous. Une fois configurée, chaque fois qu’une valeur arrive à expiration (par exemple, `ACCESS_TOKEN`), vous pouvez mettre à jour la valeur actuelle dans l’environnement. Cette nouvelle valeur est alors utilisée dans toutes vos collections.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Collections Postman {#collections}

Vous trouverez un dossier contenant toutes les collections Postman disponibles en vous rendant sur les [exemples Postman Experience Platform de référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Vous pouvez également trouver un lien de collection Postman dans chaque fichier swagger individuel dans la [documentation de référence de l’API](https://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

Pour télécharger une collection Postman, sélectionnez **[!DNL Raw]** dans la page GitHub pour charger le fichier JSON brut dans un nouvel onglet. Cliquez ensuite avec le bouton droit et sélectionnez **[!DNL Save as]** pour enregistrer le fichier vers une destination locale de votre choix.

![JSON brut](./images/api-guide/raw-collection.PNG)

## Importation d’une collection Postman {#import}

Pour utiliser une [collection Postman](#collections), un environnement doit être configuré. Une fois la configuration de l’environnement terminée, sélectionnez le sélecteur **[!DNL Manage Environments]** dans le coin supérieur droit.

![gestion du sélecteur d’environnement](./images/api-guide/environment-selector.png)

Une fenêtre contextuelle s’affiche et affiche tous vos environnements actuels. Pour importer une collection, sélectionnez **[!DNL import]** .

![bouton d&#39;import](./images/api-guide/import-collection.png)

Vous êtes invité à choisir un fichier à importer. Sélectionnez le fichier de collection Postman que vous souhaitez importer. Une fois sélectionnée, la collection est renseignée dans le rail de gauche sous l’onglet Collections .

![collection renseignée](./images/api-guide/imported-collection.png)

Chaque collection comporte des paires clé-valeur différentes qui peuvent être requises pour effectuer une opération CRUD réussie. Consultez le [guide de développement de l’API](api-guide.md#api-guides) du service pour en savoir plus sur les valeurs requises, des conseils et consulter des exemples.

Pour en savoir plus sur l’interface utilisateur de Postman et ses fonctionnalités disponibles, consultez la [documentation de Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Générer un jeton d’accès avec Postman pour une utilisation hors production

>[!WARNING]
>
>Comme indiqué dans la collection Postman de génération de jeton d’accès aux Adobes I/O, les méthodes de génération signalées sont adaptées à **utilisation hors production**. La signature locale charge une bibliothèque JavaScript à partir d’un hôte tiers et la signature à distance envoie la clé privée à un service Web détenu et exploité par Adobe. Bien qu’Adobe ne stocke pas cette clé privée, les clés de production ne doivent jamais être partagées avec personne.

La vidéo ci-dessous utilise la [collection de génération de jetons d’accès d’Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) qui peut être téléchargée à partir du référentiel GitHub public.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Étapes suivantes

Ce document présente les environnements Postman, les collections et la manière d’importer des collections. Maintenant que Postman est prêt, consultez le [guide de prise en main de Platform](api-guide.md) pour plus d’informations sur les en-têtes, les exemples requis et une liste de [guides de l’API](api-guide.md#api-guides) disponibles pour chaque service Platform.
