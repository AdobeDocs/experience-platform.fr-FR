---
keywords: Experience Platform;prise en main;contenu;commerce ai;contenu et commerce ai
solution: Experience Platform
title: Prise en main de Content and Commerce AI
topic-legacy: Getting started
description: Content and Commerce AI utilise des API d’Adobe I/O. Pour lancer des appels aux API Adobe I/O et à l’intégration de la console I/O, vous devez d’abord suivre le tutoriel sur l’authentification.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 15%

---

# Prise en main de Content and Commerce AI

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

[!DNL Content and Commerce AI] utilise les API d’Adobe I/O. Pour passer des appels aux API Adobe I/O et à l’intégration de la console I/O, vous devez d’abord renseigner la variable [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

Cependant, lorsque vous accédez à la variable **Ajout d’une API** , l’API se trouve sous Experience Cloud au lieu de Adobe Experience Platform, comme illustré dans la capture d’écran suivante :

![Ajout de Content and Commerce AI](./images/add-api.png)

Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API d’Adobe I/O, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Création d’un environnement Postman (facultatif)

Une fois que vous avez configuré votre projet et votre API dans la console Adobe Developer, vous avez la possibilité de télécharger un fichier d’environnement pour Postman. Sous **[!UICONTROL API]** dans le rail de gauche du projet, sélectionnez **[!UICONTROL IA dédiée au contenu et au commerce]**. Un nouvel onglet s’ouvre, contenant une carte intitulée &quot;[!DNL Try it out]&quot;. Sélectionner **Téléchargement pour Postman** pour télécharger un fichier JSON utilisé pour configurer votre environnement postman.

![téléchargement pour postman](./images/add-to-postman.png)

Une fois le fichier téléchargé, ouvrez Postman et sélectionnez l’option **icône d’engrenage** en haut à droite pour ouvrir la **gestion des environnements** boîte de dialogue.

![icône d’engrenage](./images/select-gear-icon.png)

Ensuite, sélectionnez **Importer** de dans **Gestion des environnements** boîte de dialogue.

![import](./images/import.png)

Vous êtes redirigé et invité à sélectionner un fichier d’environnement sur votre ordinateur. Sélectionnez le fichier JSON que vous avez téléchargé précédemment, puis sélectionnez **Ouvrir** pour charger l’environnement.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Vous êtes redirigé vers le *Gestion des environnements* avec un nouveau nom d’environnement renseigné. Sélectionnez le nom de l’environnement pour afficher et modifier les variables disponibles dans Postman. Vous devez toujours renseigner manuellement la variable `JWT_TOKEN` et `ACCESS_TOKEN`. Ces valeurs doivent avoir été obtenues lors de la [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

Une fois que vous avez terminé, vos variables doivent ressembler à la capture d’écran ci-dessous. Sélectionner **Mettre à jour** pour terminer la configuration de votre environnement.

![](./images/final-environment.png)

Vous pouvez désormais sélectionner votre environnement dans le menu déroulant dans le coin supérieur droit et renseigner automatiquement toutes les valeurs enregistrées. Il vous suffit de modifier à tout moment les valeurs pour mettre à jour tous vos appels d’API.

![exemple](./images/select-environment.png)

Pour plus d’informations sur l’utilisation des API Adobe I/O à l’aide de Postman, reportez-vous à la publication sur le site Medium de [utilisation de Postman pour l’authentification JWT sur Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Une fois que vous disposez de toutes vos informations d’identification, vous êtes prêt à configurer un programme de travail personnalisé pour [!DNL Content and Commerce AI]. Les documents suivants aident à comprendre le framework d’extensibilité et la configuration de l’environnement.

Pour en savoir plus sur le framework d’extensibilité, commencez par lire le [introduction à l’extensibilité](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=fr) document. Ce document décrit les conditions préalables et les exigences en matière de configuration.

Pour en savoir plus sur la configuration d’un environnement pour [!DNL Content and Commerce AI], commencez par lire le guide pour [configuration d’un environnement de développement](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Ce document fournit des instructions de configuration qui vous permettent de développer pour Asset compute Service.
