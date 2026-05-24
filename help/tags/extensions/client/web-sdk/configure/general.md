---
title: Paramètres de configuration de l’instance du SDK
description: Configurez les paramètres généraux de l’instance Web SDK.
exl-id: cc22b8b3-88c6-4030-91b4-60e14a3b0f42
TQID: https://experienceleague.adobe.com/YcT1bzlpS8kUyB-agr5inPv2adRL8V1y2R8LweccnRU
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 293
ht-degree: 11%

---

# Paramètres de configuration de l’instance du SDK {#sdk-instance}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_sdkinstance"
>title="Instances du SDK"
>abstract="Définit le nom de l’instance du SDK, l’organisation IMS à laquelle elle appartient et le domaine Edge."

Cette section de configuration régit le nom de l’instance Web SDK, l’organisation IMS à laquelle elle s’applique et l’emplacement auquel vous souhaitez envoyer des données. Par défaut, une instance est nommée `alloy`.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Recherchez le nom de l’instance juste en dessous de l’accordéon [!UICONTROL SDK instances] développé.

![Image montrant les paramètres généraux de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/web-sdk-ext-general.png)

Les options disponibles sont les suivantes :

## [!UICONTROL Name]

L’extension de balise Adobe Experience Platform Web SDK prend en charge plusieurs instances sur la page. Le nom permet d’envoyer des données à plusieurs organisations sans avoir besoin de bibliothèques de balises Web SDK en double. Vous pouvez remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide.

## [!UICONTROL IMS organization ID]

L’identifiant de l’organisation à laquelle vous souhaitez que les données soient envoyées chez Adobe. La plupart du temps, utilisez la valeur par défaut qui est automatiquement renseignée. Lorsque la page comporte plusieurs instances, renseignez ce champ avec la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.

## [!UICONTROL Edge domain]

Domaine vers lequel/à partir duquel l’extension envoie et reçoit des données. Par défaut, le champ contient `<COMPANYID>.data.adobedc.net`. Les implémentations plus anciennes peuvent contenir une valeur par défaut de `edge.adobedc.net`, qui est également valide.

Adobe recommande dans la plupart des cas d’utiliser un domaine propriétaire. Consultez le [programme de certificat géré par ](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) pour obtenir des instructions sur la configuration d’un domaine propriétaire adapté à la collecte de données. Voir aussi [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) dans la documentation de la bibliothèque JavaScript pour obtenir des conseils sur la définition de cette valeur.
