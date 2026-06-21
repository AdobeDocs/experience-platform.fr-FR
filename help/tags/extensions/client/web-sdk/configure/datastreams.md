---
title: Paramètres de configuration du train de données
description: Configurez le flux de données pour envoyer des données à à l’aide de l’extension de balise Web SDK.
exl-id: 2d2504c6-b3f9-4e7b-aff4-a8d8d6c4e3dd
TQID: https://experienceleague.adobe.com/wasqc9Z1B34MbwssS0s4XBnpXKjzYJVjrOG3Otj1GrA
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 275
ht-degree: 8%

---

# Paramètres de configuration du train de données {#datastreams}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datastreams"
>title="Flux de données"
>abstract="Obligatoire. Définit le train de données dans Edge Network auquel vous souhaitez envoyer des données."

Cette section de configuration vous permet de déterminer à quel [flux de données](/help/datastreams/overview.md) vous souhaitez envoyer des données. **Un identifiant de flux de données est requis pour toutes les données envoyées à Edge Network.**

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Flux de données]**.

![Image montrant les paramètres de train de données de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/web-sdk-ext-datastreams.png)

Lors de la sélection de flux de données, vous pouvez le faire pour chaque [environnement](/help/tags/ui/publishing/environments.md) ([!UICONTROL développement], [!UICONTROL évaluation] et [!UICONTROL production]). Ces champs sont utiles lorsque vous souhaitez séparer les données envoyées entre les environnements de développement, d’évaluation et de production. Il active un workflow pratique où vous n’avez pas à vous soucier d’envoyer des données au mauvais flux de données, à condition d’installer le bon chargeur de balises dans chaque environnement respectif.

Vous pouvez renseigner les identifiants de train de données à l’aide de l’une des méthodes suivantes :

* **[!UICONTROL Choisir dans la liste]** : chaque environnement contient deux menus déroulants, qui vous permettent de sélectionner le sandbox et le flux de données de l’environnement sélectionné. Les valeurs de chaque menu déroulant dépendent de vos [flux de données](/help/datastreams/overview.md) configurés dans chaque [sandbox](/help/sandboxes/ui/overview.md) respectif.

* **[!UICONTROL Saisir des valeurs]** : au lieu d’utiliser des menus déroulants pour sélectionner le flux de données souhaité, vous pouvez spécifier manuellement l’identifiant du flux de données souhaité. Chaque environnement vous permet de saisir directement un identifiant de flux de données ou de renseigner ce champ à l’aide d’un [élément de données](/help/tags/ui/managing-resources/data-elements.md).
