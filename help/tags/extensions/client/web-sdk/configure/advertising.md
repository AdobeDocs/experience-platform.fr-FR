---
title: Paramètres de configuration d’Adobe Advertising
description: Activez ou désactivez la fonctionnalité Demand-side Platform.
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
TQID: https://experienceleague.adobe.com/LgIPs8Gke0ApLPRaiegkbd-sFJUnHLQsqHqn0GfajNI
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e0e9cace-366e-4b9c-b3b9-31ec233dfc89
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: ee30758d-9ffe-4cd7-8f26-0d4394f041f6
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 26%

---

# Paramètres de configuration d’Adobe Advertising {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Configurez les paramètres des intégrations Adobe Advertising. Notez qu’aucune configuration publicitaire n’est nécessaire pour activer la mesure des clics publicitaires. Aucune autre action n’est requise de la part des clientes et clients Search, Social et Commerce. Toutefois, les utilisateurs et utilisatrices de la plateforme côté demande (DSP) doivent configurer les annonceurs dans cette section afin de mesurer les conversions d’affichage publicitaire."

La section **&#x200B;**&#x200B;vous permet d’activer ou de désactiver la fonctionnalité de plateforme côté demande (DSP) si elle est utilisée dans votre implémentation. Vous ne devez définir ce champ que si votre implémentation utilise un DSP.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Faites défiler l’écran jusqu’à la section **&#x200B;**.

Actuellement, une option est disponible.

## &#x200B;

Un menu déroulant qui active ou désactive la fonctionnalité DSP pour Adobe Advertising.

* **[!UICONTROL Activé]** : active le suivi des vues publicitaires.
* **[!UICONTROL Désactivé]** : désactive le suivi des affichages publicitaires.

Lorsqu’ils sont activés, les paramètres suivants sont disponibles :

* **[!UICONTROL Annonceurs]** : annonceurs pour lesquels le suivi des affichages publicitaires doit être activé.
* **[!UICONTROL ID5 de partenaire]** : facultatif. Identifiant partenaire ID5 de votre organisation. Ce paramètre permet au SDK Web de collecter les ID5 universels.
* **[!UICONTROL Chemin JavaScript RampID]** : facultatif. Chemin d’accès au code JavaScript [!DNL LiveRamp RampID] de votre organisation (`ats.js`).  Ce paramètre permet au SDK Web de collecter les identifiants universels [!DNL RampID].
