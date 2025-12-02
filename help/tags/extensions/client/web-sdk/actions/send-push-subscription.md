---
title: Envoyer un abonnement push
description: Enregistrez, envoyez et collectez des données pour les abonnements push du navigateur.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 7%

---

# Envoyer un abonnement push

>[!AVAILABILITY]
>
>Les notifications push pour le Web SDK sont actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

L’action **[!UICONTROL Send push subscription]** enregistre les abonnements aux notifications push auprès de Adobe Experience Platform. Il gère la récupération des détails d’abonnement push à partir du navigateur et les envoie à votre flux de données configuré. Il est disponible dans les versions 2.32.0 ou ultérieures de l’extension Web SDK.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]** et définissez la [!UICONTROL Action Type] sur **[!UICONTROL Send push subscription]**.

L’action ne comporte aucun paramètre de configuration, à part la sélection d’une instance SDK.

Assurez-vous d’avoir défini une [clé publique valide](../configure/push-notifications.md) lors de la configuration de l’extension avant d’utiliser cette commande.

Cette action est l’extension de balise équivalente à la commande [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md). Consultez la page liée pour plus d’informations sur les conditions préalables, la fréquence d’exécution recommandée, le fonctionnement de la commande et la gestion des erreurs.

>[!MORELIKETHIS]
>
>* [Configurer les notifications push](../configure/push-notifications.md)
>* [Spécification de l’API Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [ API Service Worker ](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
