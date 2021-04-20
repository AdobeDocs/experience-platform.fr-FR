---
keywords: Experience Platform;prise en main;content ai;commerce ai;content and commerce ai
solution: Experience Platform, Intelligent Services
title: Prise en main de Content and Commerce AI
topic: Getting started 
description: Content and Commerce AI utilise les API Adobe I/O. Pour appeler les API Adobe I/O et l'intégration de la console d'E/S, vous devez d'abord suivre le didacticiel d'authentification.
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 13%

---


# Prise en main de Content and Commerce AI

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

[!DNL Content and Commerce AI] utilise les API Adobe I/O. Pour appeler les API Adobe I/O et l&#39;intégration de la console d&#39;E/S, vous devez d&#39;abord suivre le didacticiel d&#39;authentification [](https://www.adobe.com/go/platform-api-authentication-en).

Cependant, lorsque vous atteignez l’étape **Ajouter API**, l’API se trouve sous Experience Cloud au lieu de Adobe Experience Platform, comme indiqué dans la capture d’écran suivante :

![ajout d’une API de contenu et de commerce](./images/add-api.png)

Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Adobe I/O, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Créer un environnement Postman (facultatif)

Une fois que vous avez configuré votre projet et votre API dans Adobe Developer Console, vous avez la possibilité de télécharger un fichier d&#39;environnement pour Postman. Sous **[!UICONTROL API]** le rail gauche de votre projet, sélectionnez **[!UICONTROL Contenu et commerce AI]**. Un nouvel onglet s’ouvre, contenant une carte intitulée &quot;[!DNL Try it out]&quot;. Sélectionnez **Télécharger pour Postman** pour télécharger un fichier JSON utilisé pour configurer votre environnement postman.

![téléchargement pour postman](./images/add-to-postman.png)

Après avoir téléchargé le fichier, ouvrez Postman et sélectionnez l&#39;icône **engrenage** en haut à droite pour ouvrir la boîte de dialogue **gérer les environnements**.

![icône d&#39;engrenage](./images/select-gear-icon.png)

Ensuite, sélectionnez **Importer** dans la boîte de dialogue **Gérer les environnements**.

![import](./images/import.png)

Vous êtes redirigé et invité à sélectionner un fichier d’environnement sur votre ordinateur. Sélectionnez le fichier JSON que vous avez téléchargé précédemment, puis sélectionnez **Ouvrir** pour charger l’environnement.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Vous êtes redirigé vers l&#39;onglet *Gérer les environnements* avec un nouveau nom d&#39;environnement renseigné. Sélectionnez le nom de l&#39;environnement à vue et modifiez les variables disponibles dans Postman. Vous devez toujours renseigner manuellement les éléments `JWT_TOKEN` et `ACCESS_TOKEN`. Ces valeurs auraient dû être obtenues lors de l&#39;exécution du didacticiel d&#39;authentification [](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

Une fois les variables terminées, elles doivent ressembler à la capture d’écran ci-dessous. Sélectionnez **Mettre à jour** pour terminer la configuration de votre environnement.

![](./images/final-environment.png)

Vous pouvez désormais sélectionner votre environnement dans le menu déroulant situé dans le coin supérieur droit et renseigner automatiquement toutes les valeurs enregistrées. Il vous suffit de modifier à tout moment les valeurs pour mettre à jour tous vos appels d’API.

![example](./images/select-environment.png)

Pour plus d&#39;informations sur l&#39;utilisation des API Adobe I/O avec Postman, consultez la publication Medium sur [Utilisation de Postman pour l&#39;authentification JWT sur Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Une fois que vous disposez de toutes vos informations d’identification, vous êtes prêt à configurer un programme de travail personnalisé pour [!DNL Content and Commerce AI]. Les documents suivants aident à comprendre le cadre d&#39;extensibilité et la configuration des environnements.

Pour en savoir plus sur le cadre d&#39;extensibilité, début en lisant le document [introduction à l&#39;extensibilité](https://docs.adobe.com/content/help/fr-FR/asset-compute/using/extend/understand-extensibility.html). Ce document décrit les conditions préalables et les exigences de mise en service.

Pour en savoir plus sur la configuration d&#39;un environnement pour [!DNL Content and Commerce AI], début en lisant le guide de [configuration d&#39;un environnement développeur](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html). Ce document fournit des instructions de configuration qui vous permettent de développer pour Asset compute Service.