---
title: Extension SDK Web Adobe Experience Platform Présentation
description: En savoir plus sur Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 14%

---


# Présentation de l’extension SDK Web Adobe Experience Platform

L’extension Adobe Experience Platform Web SDK envoie des données à Adobe Experience Cloud à partir de propriétés web via Adobe Experience Platform Edge Network. L’extension vous permet de diffuser des données dans la plate-forme, de synchroniser les identités, de traiter les signaux de consentement des clients et de collecter automatiquement des données contextuelles.

Ce document explique comment configurer l’extension dans l’interface utilisateur Adobe Experience Platform Launch.

## Configurez l’extension

Si l&#39;extension Platform Web SDK a déjà été installée pour une propriété, ouvrez la propriété dans l&#39;interface utilisateur du Platform launch et sélectionnez l&#39;onglet **[!UICONTROL Extensions]**. Sous Platform Web SDK, sélectionnez **[!UICONTROL Configurer]**.

![](../images/extension/overview/configure.png)

Si vous n’avez pas encore installé l’extension, sélectionnez l’onglet **[!UICONTROL Catalogue]**. Dans la liste des extensions disponibles, recherchez l&#39;extension Platform Web SDK et sélectionnez **[!UICONTROL Installer]**.

![](../images/extension/overview/install.png)

Dans les deux cas, vous accédez à la page de configuration du SDK Web de la plate-forme. Les sections ci-dessous décrivent les options de configuration de l&#39;extension.

![](../images/extension/overview/config-screen.png)

## Options de configuration générales

Les options de configuration situées en haut de la page indiquent à Adobe Experience Platform où router les données et les configurations à utiliser sur le serveur.

### [!UICONTROL Nom]

L’extension Adobe Experience Platform Web SDK prend en charge plusieurs instances sur la page. Le nom est utilisé pour envoyer des données à plusieurs organisations avec une configuration de Platform launch unique.

Le nom de l&#39;extension est par défaut &quot;[!DNL alloy]&quot;. Vous pouvez toutefois remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide.

### **[!UICONTROL Identifiant IMS de l’organisation]**

[!UICONTROL L&#39;ID d&#39;organisation IMS] est l&#39;organisation à laquelle vous souhaitez envoyer les données à l&#39;Adobe. La plupart du temps, utilisez la valeur par défaut qui est automatiquement renseignée. Lorsque la page contient plusieurs instances, renseignez ce champ avec la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.

### **[!UICONTROL Domaine Edge]**

Le [!UICONTROL domaine Edge] est le domaine à partir duquel l&#39;extension Adobe Experience Platform envoie et reçoit des données. L’extension exige l’utilisation d’un CNAME propriétaire pour le trafic de production. Le domaine tiers par défaut fonctionne pour les environnements de développement, mais ne convient pas aux environnements de production. Les instructions de configuration d’un CNAME propriétaire sont répertoriées [ici](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Configurations Edge]

Lorsqu’une requête est envoyée au réseau Edge de Adobe Experience Platform, un ID de configuration Edge est utilisé pour référencer la configuration côté serveur. Vous pouvez mettre à jour la configuration sans avoir à modifier le code de votre site Web.

Pour plus d&#39;informations, consultez le guide sur les [configurations des arêtes](../fundamentals/edge-configuration.md).

## [!UICONTROL Confidentialité]

La section [!UICONTROL Confidentialité] permet de configurer la manière dont le SDK traite les signaux de consentement des clients à partir de votre site Web. En particulier, il vous permet de sélectionner le niveau de consentement par défaut supposé d’un client si aucune autre préférence explicite de consentement n’a été fournie. Le tableau suivant ventile ce que chaque option implique :

| [!UICONTROL Niveau de consentement par défaut] | Description |
| --- | --- |
| [!UICONTROL In] | Inscription. Utilisez cette option si vous supposez que le consentement du client est donné par défaut et que vous n’acceptez que les signaux d’exclusion. |
| [!UICONTROL En attente] | Les clients avec le consentement &quot;en attente&quot; sont désactivés jusqu’à ce qu’un signal d’inclusion soit envoyé. Utilisez cette option si vous avez besoin du consentement explicite du client pour vos activités commerciales. |
| [!UICONTROL Fourni par l’élément de données] | Le niveau de consentement par défaut est déterminé par un élément de données distinct que vous définissez. Lorsque vous utilisez cette option, vous devez spécifier l’élément de données à l’aide du menu déroulant fourni. |