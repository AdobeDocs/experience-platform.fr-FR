---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Prise en main de Content and Commerce AI]
topic: Getting started
description: Content and Commerce AI utilise des API d'E/S d'Adobe. Pour appeler les API d'E/S d'Adobe et l'intégration de la console d'E/S, vous devez d'abord suivre le didacticiel d'authentification.
translation-type: tm+mt
source-git-commit: 9ee888b02b4a402200ca4fcaed4a59c0a7eb94cd
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 12%

---


# Getting started with [!DNL Content and Commerce AI]

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

[!DNL Content and Commerce AI] utilise les API d&#39;E/S d&#39;Adobe. Pour appeler les API d&#39;E/S d&#39;Adobe et l&#39;intégration de la console d&#39;E/S, vous devez d&#39;abord suivre le didacticiel [d&#39;](../../tutorials/authentication.md)authentification.

Cependant, lorsque vous atteignez l’étape de l’API **** Ajoute, l’API se trouve sous Experience Cloud et non pas Adobe Experience Platform, comme illustré dans la capture d’écran suivante :

![ajout d’une API de contenu et de commerce](./images/add-api.png)

Le didacticiel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API d&#39;E/S d&#39;Adobe, comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Créer un environnement Postman (facultatif)

Une fois que vous avez configuré votre projet et votre API dans Adobe Developer Console, vous avez la possibilité de télécharger un fichier d&#39;environnement pour Postman. Sous **[!UICONTROL API]** dans le rail de gauche de votre projet, sélectionnez **[!UICONTROL Contenu et Commerce AI]**. Un nouvel onglet s’ouvre, contenant une carte intitulée &quot;[!DNL Try it out]&quot;. Sélectionnez **Télécharger pour Postman** pour télécharger un fichier JSON utilisé pour configurer votre environnement postman.

![téléchargement pour postman](./images/add-to-postman.png)

Après avoir téléchargé le fichier, ouvrez Postman et sélectionnez l&#39;icône **d&#39;** engrenage dans le coin supérieur droit pour ouvrir la boîte de dialogue **gérer les environnements** .

![icône d&#39;engrenage](./images/select-gear-icon.png)

Ensuite, sélectionnez **Importer** dans la boîte de dialogue **Gérer les environnements** .

![import](./images/import.png)

Vous êtes redirigé et invité à sélectionner un fichier d’environnement sur votre ordinateur. Sélectionnez le fichier JSON que vous avez téléchargé précédemment, puis sélectionnez **Ouvrir** pour charger l’environnement.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Vous êtes redirigé vers l’onglet *Gérer les environnements* avec un nouveau nom d’environnement renseigné. Sélectionnez le nom de l&#39;environnement à vue et modifiez les variables disponibles dans Postman. Vous devez quand même renseigner manuellement les champs `JWT_TOKEN` et `ACCESS_TOKEN`. Ces valeurs auraient dû être obtenues lors de l’exécution du didacticiel [d’](../../tutorials/authentication.md)authentification.

![](./images/re-direct.png)

Une fois les variables terminées, elles doivent ressembler à la capture d’écran ci-dessous. Sélectionnez **Mettre à jour** pour terminer la configuration de votre environnement.

![](./images/final-environment.png)

Vous pouvez désormais sélectionner votre environnement dans le menu déroulant situé dans le coin supérieur droit et renseigner automatiquement toutes les valeurs enregistrées. Il vous suffit de modifier à tout moment les valeurs pour mettre à jour tous vos appels d’API.

![example](./images/select-environment.png)

Pour plus d&#39;informations sur l&#39;utilisation des API d&#39;E/S d&#39;Adobe avec Postman, consultez le post Medium sur l&#39; [utilisation de Postman pour l&#39;authentification JWT sur les E/S](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)d&#39;Adobe.

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Une fois que vous disposez de toutes vos informations d’identification, vous êtes prêt à configurer un collaborateur personnalisé pour [!DNL Content and Commerce AI]. Les documents suivants aident à comprendre le cadre d&#39;extensibilité et la configuration des environnements.

Pour en savoir plus sur le Cadre d&#39;extensibilité, début en lisant l&#39; [introduction au document d&#39;extensibilité](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) . Ce document décrit les conditions préalables et les exigences de mise en service.

Pour en savoir plus sur la configuration d&#39;un environnement pour [!DNL Content and Commerce AI], consultez le début en lisant le guide de [configuration d&#39;un environnement](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)de développement. Ce document fournit des instructions de configuration qui vous permettent de développer pour le service Asset Compute.