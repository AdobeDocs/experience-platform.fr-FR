---
title: Appliquer la réponse
description: Exécutez une action basée sur une réponse d’Edge Network.
exl-id: 64ea7d48-ce20-4694-a3f1-415fc5a97ac5
TQID: https://experienceleague.adobe.com/HAeiB4M-sGxM9KMqkzwsJYocmoXYqvElOlpysKgc8BE
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: ee602049-8a18-43df-9299-a689a025a371
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 327
ht-degree: 1%

---

# Appliquer la réponse

Le type d’action **[!UICONTROL Apply response]** permet d’effectuer différentes actions en fonction d’une réponse d’Edge Network. Ce type d’action est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial à l’Edge Network, puis ce type d’action prend la réponse de cet appel et initialise le SDK Web dans le navigateur. L’utilisation de ce type d’action peut réduire les temps de chargement des clients pour les cas d’utilisation de personnalisation hybride.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant du [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Action type] sur **[!UICONTROL Apply response]**.

![Image de l’interface utilisateur d’Experience Platform affichant le type d’action Appliquer la réponse.](../assets/apply-response.png)

## Cas d’utilisation

* **Répartition manuelle entre la collecte de données et la personnalisation** : vous pouvez déclencher une action [Envoyer l’événement](send-event.md) avec des décisions de rendu définies sur `false`, puis laisser une règle « Envoyer l’événement terminé » capturer la promesse. La première action de cette règle peut être « Appliquer la réponse ». Ce workflow vous permet de différer la manipulation DOM jusqu’à ce que le code de votre organisation termine un autre travail.
* **Réponse Edge reçue de l&#39;extérieur de Web SDK** : si vous utilisez une autre bibliothèque pour communiquer avec Edge Network, vous pouvez permettre à Web SDK de gérer toujours la réponse d&#39;Edge Network à l&#39;aide de cette action.

## Champs disponibles

Ce type d’action prend en charge les options de configuration suivantes :

* **[!UICONTROL Instance]** : instance SDK à laquelle l’action s’applique. Ce menu déroulant est désactivé si votre implémentation utilise une seule instance SDK.
* **[!UICONTROL Response headers]** : sélectionnez l’élément de données qui renvoie un objet contenant les clés et valeurs d’en-tête renvoyées par l’appel au serveur Edge Network.
* **[!UICONTROL Response body]** : sélectionnez l’élément de données qui renvoie l’objet contenant la payload JSON fournie par la réponse Edge Network.
* **[!UICONTROL Render visual personalization decisions]** : activez cette option pour effectuer automatiquement le rendu du contenu de personnalisation fourni par Edge Network et pré-masquer le contenu pour éviter le scintillement.
