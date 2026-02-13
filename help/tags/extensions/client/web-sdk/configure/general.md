---
title: Paramètres de configuration des instances SDK
description: Configurez les paramètres généraux de l’instance Web SDK.
exl-id: cc22b8b3-88c6-4030-91b4-60e14a3b0f42
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# Paramètres de configuration des instances SDK {#sdk-instance}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_sdkinstance"
>title="Instances de SDK"
>abstract="Définit le nom de l’instance SDK, l’organisation IMS à laquelle elle appartient et le domaine Edge."

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

Adobe recommande dans la plupart des cas d’utiliser un domaine propriétaire. Consultez le [programme de certificat géré par Adobe](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/adobe-managed-cert) pour obtenir des instructions sur la configuration d’un domaine propriétaire adapté à la collecte de données. Voir aussi [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) dans la documentation de la bibliothèque JavaScript pour obtenir des conseils sur la définition de cette valeur.
