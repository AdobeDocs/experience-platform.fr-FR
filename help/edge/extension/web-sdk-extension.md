---
title: Présentation de l’extension SDK Web Adobe Experience Platform
description: En savoir plus sur Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: b70fe5f3a4de2501730cc799125a7181b61186c0
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 13%

---

# Présentation de l’extension SDK Web d’Adobe Experience Platform

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

## [!UICONTROL Datastreams]

Lorsqu’une requête est envoyée au réseau Edge de Adobe Experience Platform, un ID de flux de données est utilisé pour référencer la configuration côté serveur. Vous pouvez mettre à jour la configuration sans avoir à modifier le code de votre site Web.

Pour plus d&#39;informations, consultez le guide [datastreams](../fundamentals/datastreams.md).


## [!UICONTROL Confidentialité]

La section [!UICONTROL Confidentialité] permet de configurer la manière dont le SDK traite les signaux de consentement des utilisateurs de votre site Web. En particulier, il vous permet de sélectionner le niveau de consentement par défaut supposé d’un utilisateur si aucune autre préférence explicite de consentement n’a été fournie. Le niveau de consentement par défaut n’est pas enregistré au profil de l’utilisateur. Le tableau suivant ventile ce que chaque option implique :

| [!UICONTROL Niveau de consentement par défaut] | Description |
| --- | --- |
| [!UICONTROL In] | Collectez les événements qui surviennent avant que l’utilisateur ne donne ses préférences de consentement. |
| [!UICONTROL Sortie] | Ignorer les événements qui surviennent avant que l’utilisateur ne donne ses préférences de consentement. |
| [!UICONTROL En attente] | Événements de file d’attente qui surviennent avant que l’utilisateur ne donne ses préférences de consentement. Lorsque les préférences de consentement sont fournies, les événements seront collectés ou rejetés selon les préférences fournies. |
| [!UICONTROL Fourni par l’élément de données] | Le niveau de consentement par défaut est déterminé par un élément de données distinct que vous définissez. Lorsque vous utilisez cette option, vous devez spécifier l’élément de données à l’aide du menu déroulant fourni. |

Utilisez l’option Sortie ou En attente si vous avez besoin du consentement explicite de l’utilisateur pour vos activités commerciales.
