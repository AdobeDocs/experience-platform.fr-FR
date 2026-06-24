---
keywords: Experience Platform;prise en main;contenu;balisage de contenu
solution: Experience Platform
title: Prise en main du balisage de contenu
description: Le balisage de contenu utilise les API Adobe I/O. Pour lancer des appels aux API Adobe I/O et à l’intégration de la console I/O, vous devez d’abord suivre le tutoriel sur l’authentification.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
TQID: https://experienceleague.adobe.com/HOT682PuFoU2fyxdRtKHScIOQSxRSVthbsyd9Yxz8os
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 584
ht-degree: 16%

---

# Prise en main du balisage de contenu

[!DNL Content tagging] utilise les API Adobe I/O. Pour lancer des appels aux API Adobe I/O et à l’intégration de la console I/O, vous devez d’abord suivre le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

Cependant, lorsque vous accédez à l’étape **Ajouter une API**, l’API se trouve sous Creative Cloud au lieu de Adobe Experience Platform, comme illustré dans la capture d’écran suivante :

![ajout du balisage de contenu](./images/add-api-updated.png)

Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API d’Adobe I/O, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Création d’un environnement Postman (facultatif)

Une fois que vous avez configuré votre projet et votre API dans Adobe Developer Console, vous avez la possibilité de télécharger un fichier d’environnement pour Postman. Sous **[!UICONTROL API]** dans le rail de gauche du projet, sélectionnez **[!UICONTROL Balisage de contenu]**. Un nouvel onglet s’ouvre, contenant une carte intitulée « [!DNL Try it out] ». Sélectionnez **Télécharger pour Postman** pour télécharger un fichier JSON utilisé pour configurer votre environnement Postman.

![télécharger pour postman](./images/add-to-postman-updated.png)

Une fois le fichier téléchargé, ouvrez Postman et sélectionnez l’icône **engrenage** en haut à droite pour ouvrir la boîte de dialogue **gérer les environnements**.

![&#x200B; icône d’engrenage &#x200B;](./images/select-gear-icon.png)

Sélectionnez ensuite **Importer** dans la boîte de dialogue **Gérer les environnements**.

![import](./images/import-updated.png)

Vous êtes redirigé et invité à sélectionner un fichier d’environnement sur votre ordinateur. Sélectionnez le fichier JSON que vous avez téléchargé précédemment, puis sélectionnez **Ouvrir** pour charger l’environnement.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Vous êtes redirigé vers l’onglet *Gérer les environnements* avec un nouveau nom d’environnement renseigné. Sélectionnez le nom de l’environnement pour afficher et modifier les variables disponibles dans Postman. Vous devez toujours renseigner manuellement les `JWT_TOKEN` et les `ACCESS_TOKEN`. Ces valeurs doivent avoir été obtenues en suivant le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

![](./images/re-direct-updated.png)

Une fois l’opération terminée, vos variables doivent ressembler à la capture d’écran ci-dessous. Sélectionnez **Mettre à jour** pour terminer la configuration de votre environnement.

![](./images/final-environment-updated.png)

Vous pouvez désormais sélectionner votre environnement dans le menu déroulant du coin supérieur droit et renseigner automatiquement toutes les valeurs enregistrées. Il vous suffit de modifier à nouveau les valeurs à tout moment pour mettre à jour tous vos appels API.

![exemple](./images/select-environment-updated.png)

Pour plus d’informations sur l’utilisation des API Adobe I/O à l’aide de Postman, consultez la publication de Medium sur [Utilisation de Postman pour l’authentification JWT sur Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lecture d&#39;exemples d&#39;appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Une fois que vous disposez de toutes vos informations d’identification, vous êtes prêt à configurer un programme de travail personnalisé pour [!DNL Content tagging]. Les documents suivants aident à comprendre le framework d’extensibilité et la configuration de l’environnement.

Pour en savoir plus sur le framework d’extensibilité, commencez par lire le document [introduction à l’extensibilité](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=fr). Ce document décrit les conditions préalables et les exigences d’approvisionnement.

Pour en savoir plus sur la configuration d’un environnement pour [!DNL Content tagging], commencez par lire le guide de [configuration d’un environnement de développement](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html?lang=fr). Ce document fournit des instructions de configuration qui vous permettent de développer pour le service Asset Compute.
