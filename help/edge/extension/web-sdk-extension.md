---
title: Présentation de l’extension SDK Web Adobe Experience Platform
description: En savoir plus sur l’extension SDK Web Adobe Experience Platform pour Adobe Experience Platform Launch
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 12%

---

# Présentation de l’extension SDK Web d’Adobe Experience Platform

L’extension SDK Web Adobe Experience Platform envoie des données à Adobe Experience Cloud à partir de propriétés web par le biais du réseau Adobe Experience Platform Edge. L’extension vous permet de diffuser des données dans Platform, de synchroniser les identités, de traiter les signaux de consentement du client et de collecter automatiquement des données contextuelles.

Ce document explique comment configurer l’extension dans l’interface utilisateur d’Adobe Experience Platform Launch.

## Configurez l’extension

Si l’extension SDK Web Platform a déjà été installée pour une propriété, ouvrez la propriété dans l’interface utilisateur de Platform launch et sélectionnez l’onglet **[!UICONTROL Extensions]** . Sous Platform Web SDK, sélectionnez **[!UICONTROL Configurer]**.

![](../images/extension/overview/configure.png)

Si vous n’avez pas encore installé l’extension, sélectionnez l’onglet **[!UICONTROL Catalogue]** . Dans la liste des extensions disponibles, recherchez l’extension SDK Web Platform et sélectionnez **[!UICONTROL Installer]**.

![](../images/extension/overview/install.png)

Dans les deux cas, vous accédez à la page de configuration du SDK Web Platform. Les sections ci-dessous expliquent les options de configuration de l’extension.

![](../images/extension/overview/config-screen.png)

## Options de configuration générales

Les options de configuration en haut de la page indiquent à Adobe Experience Platform où acheminer les données et quelles configurations utiliser sur le serveur.

### [!UICONTROL Nom]

L’extension SDK Web Adobe Experience Platform prend en charge plusieurs instances sur la page. Le nom est utilisé pour envoyer des données à plusieurs organisations avec une configuration de Platform launch unique.

Le nom de l’extension est par défaut &quot;[!DNL alloy]&quot;. Vous pouvez toutefois remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide.

### **[!UICONTROL Identifiant IMS de l’organisation]**

[!UICONTROL L’ID d’organisation IMS] est l’organisation à laquelle vous souhaitez envoyer les données à Adobe. La plupart du temps, utilisez la valeur par défaut qui est renseignée automatiquement. Si la page contient plusieurs instances, renseignez ce champ avec la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.

### **[!UICONTROL Domaine Edge]**

[!UICONTROL Domaine Edge] est le domaine à partir duquel l’extension Adobe Experience Platform envoie et reçoit des données. L’extension exige l’utilisation d’un CNAME propriétaire pour le trafic de production. Le domaine tiers par défaut fonctionne pour les environnements de développement, mais ne convient pas aux environnements de production. Les instructions de configuration d’un CNAME propriétaire sont répertoriées [ici](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Datastreams]

Lorsqu’une demande est envoyée au réseau Adobe Experience Platform Edge, un identifiant de flux de données est utilisé pour référencer la configuration côté serveur. Vous pouvez mettre à jour la configuration sans avoir à apporter de modifications au code sur votre site web.

Pour plus d’informations, consultez le guide sur [les flux de données](../fundamentals/datastreams.md) .


## [!UICONTROL Confidentialité]

La section [!UICONTROL Confidentialité] vous permet de configurer la manière dont le SDK traite les signaux de consentement des utilisateurs de votre site web. Plus précisément, il vous permet de sélectionner le niveau de consentement par défaut supposé d’un utilisateur si aucune autre préférence de consentement explicite n’a été fournie. Le niveau de consentement par défaut n’est pas enregistré dans le profil de l’utilisateur. Le tableau suivant décompose les fonctions de chaque option :

| [!UICONTROL Niveau de consentement par défaut] | Description |
| --- | --- |
| [!UICONTROL In] | Collectez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL Out] | Ignorer les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. |
| [!UICONTROL En attente] | Événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. Lorsque les préférences de consentement sont fournies, les événements sont collectés ou ignorés en fonction des préférences fournies. |
| [!UICONTROL Fourni par l’élément de données] | Le niveau de consentement par défaut est déterminé par un élément de données distinct que vous définissez. Lorsque vous utilisez cette option, vous devez spécifier l’élément de données à l’aide du menu déroulant fourni. |

Utilisez Out ou Pending (En attente) si vous avez besoin du consentement explicite de l’utilisateur pour vos activités commerciales.
