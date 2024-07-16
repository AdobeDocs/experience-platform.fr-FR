---
keywords: Experience Platform;prise en main;contenu;balisage de contenu
solution: Experience Platform
title: Prise en main du balisage de contenu
description: Le balisage de contenu utilise des API d’Adobe I/O. Pour lancer des appels aux API Adobe I/O et à l’intégration de la console I/O, vous devez d’abord suivre le tutoriel sur l’authentification.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 12%

---

# Prise en main du balisage de contenu

[!DNL Content tagging] utilise des API d’Adobe I/O. Pour lancer des appels aux API Adobe I/O et à l’intégration de la console I/O, vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

Cependant, lorsque vous atteignez l’étape **Ajouter une API**, l’API se trouve sous Creative Cloud au lieu de Adobe Experience Platform, comme illustré dans la capture d’écran suivante :

![ajout de balisage de contenu](./images/add-api-updated.png)

Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API d’Adobe I/O, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Création d’un environnement Postman (facultatif)

Une fois que vous avez configuré votre projet et votre API dans Adobe Developer Console, vous avez la possibilité de télécharger un fichier d’environnement pour Postman. Sous **[!UICONTROL APIs]** dans le rail gauche de votre projet, sélectionnez **[!UICONTROL Balisage de contenu]**. Un nouvel onglet s’ouvre, contenant une carte intitulée &quot;[!DNL Try it out]&quot;. Sélectionnez **Télécharger pour Postman** pour télécharger un fichier JSON utilisé pour configurer votre environnement Postman.

![télécharger pour postman](./images/add-to-postman-updated.png)

Une fois que vous avez téléchargé le fichier, ouvrez Postman et sélectionnez l’icône **engrenage** en haut à droite pour ouvrir la boîte de dialogue **gérer les environnements**.

![icône d’engrenage](./images/select-gear-icon.png)

Sélectionnez ensuite **Importer** dans la boîte de dialogue **Gérer les environnements**.

![import](./images/import-updated.png)

Vous êtes redirigé et invité à sélectionner un fichier d’environnement sur votre ordinateur. Sélectionnez le fichier JSON que vous avez téléchargé précédemment, puis sélectionnez **Ouvrir** pour charger l’environnement.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Vous êtes redirigé vers l’onglet *Gérer les environnements* avec un nouveau nom d’environnement renseigné. Sélectionnez le nom de l’environnement pour afficher et modifier les variables disponibles dans Postman. Vous devez toujours renseigner manuellement les `JWT_TOKEN` et `ACCESS_TOKEN`. Ces valeurs doivent avoir été obtenues lors de l’exécution du [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

![](./images/re-direct-updated.png)

Une fois que vous avez terminé, vos variables doivent ressembler à la capture d’écran ci-dessous. Sélectionnez **Mettre à jour** pour terminer la configuration de votre environnement.

![](./images/final-environment-updated.png)

Vous pouvez désormais sélectionner votre environnement dans le menu déroulant dans le coin supérieur droit et renseigner automatiquement toutes les valeurs enregistrées. Il vous suffit de modifier à tout moment les valeurs pour mettre à jour tous vos appels d’API.

![exemple](./images/select-environment-updated.png)

Pour plus d’informations sur l’utilisation des API Adobe I/O avec Postman, reportez-vous à la publication Medium sur [l’utilisation de Postman pour l’authentification JWT sur Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Une fois que vous disposez de toutes vos informations d’identification, vous êtes prêt à configurer un programme de travail personnalisé pour [!DNL Content tagging]. Les documents suivants aident à comprendre le framework d’extensibilité et la configuration de l’environnement.

Pour en savoir plus sur Extensibility Framework, commencez par lire le document [introduction à l’extensibilité](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html). Ce document décrit les conditions préalables et les exigences en matière de configuration.

Pour en savoir plus sur la configuration d’un environnement pour [!DNL Content tagging], commencez par lire le guide de [configuration d’un environnement de développement](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Ce document fournit des instructions de configuration qui vous permettent de développer pour Asset Compute Service.
