---
title: Envoyer un abonnement push
description: Enregistrez, envoyez et collectez des données pour les abonnements push du navigateur.
exl-id: 5a19dab9-cd47-4920-9864-6094b89ab1a1
TQID: https://experienceleague.adobe.com/39epFLTnbR6-1veSp-a7pd4tfvustc-SdkGabLdsQSE
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 221
ht-degree: 9%

---

# Envoyer un abonnement push

>[!AVAILABILITY]
>
>Les notifications push pour le Web SDK sont actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

L’action **[!UICONTROL Envoyer un abonnement push]** enregistre les abonnements aux notifications push auprès de Adobe Experience Platform. Il gère la récupération des détails d’abonnement push à partir du navigateur et les envoie à votre flux de données configuré. Il est disponible dans les versions 2.32.0 ou ultérieures de l’extension Web SDK.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]** puis définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’abonnement push]**.

L’action ne comporte aucun paramètre de configuration, à part la sélection d’une instance SDK.

Assurez-vous d’avoir défini une [clé publique valide](../configure/push-notifications.md) lors de la configuration de l’extension avant d’utiliser cette commande.

Cette action est l’extension de balise équivalente à la commande [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md). Consultez la page liée pour plus d’informations sur les conditions préalables, la fréquence d’exécution recommandée, le fonctionnement de la commande et la gestion des erreurs.

>[!MORELIKETHIS]
>
>* [Configurer les notifications push](../configure/push-notifications.md)
>* [Spécification de l’API Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [ API Service Worker ](https://developer.mozilla.org/fr/docs/Web/API/Service_Worker_API)
