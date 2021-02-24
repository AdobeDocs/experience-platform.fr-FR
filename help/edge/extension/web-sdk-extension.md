---
title: Extension SDK Web Adobe Experience Platform Présentation
description: En savoir plus sur Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 53%

---


# Présentation de l’extension SDK Web Adobe Experience Platform

L’extension Adobe Experience Platform Web SDK envoie des données au Adobe Experience Cloud à partir de propriétés web, via Adobe Experience Platform Edge Network. L’extension SDK Web Adobe Experience Platform permet la diffusion en flux continu de données dans la plateforme, la synchronisation des identités, l’accord préalable et la collecte automatique de données contextuelles.

## Configurez l’extension

Cette section fournit une référence pour les options disponibles pendant la configuration de l’extension SDK Web Adobe Experience Platform.

Si l’extension Adobe Experience Platform Web SDK n’est pas encore installée, ouvrez votre propriété, puis sélectionnez **[!UICONTROL Extensions > Catalog]**, passez la souris sur l’extension Adobe Experience Platform Web SDK et sélectionnez **[!UICONTROL Installer]**.

Pour configurer l&#39;extension, ouvrez l&#39;onglet **[!UICONTROL Extensions]**, passez la souris sur l&#39;extension, puis sélectionnez **[!UICONTROL Configurer]**.

![](./assets/ext-aep-config.png)

### Nom d’instance

L’extension Adobe Experience Platform Web SDK prend en charge plusieurs instances sur la page. Elle permet d’envoyer des données à plusieurs organisations à l’aide d’une configuration Adobe Experience Platform Launch unique. Le **[!UICONTROL nom]** est par défaut un alliage. Vous pouvez toutefois remplacer le nom de l’instance par n’importe quel nom d’objet JavaScript valide. L’extension Adobe Experience Platform exige que chaque instance ait un **[!UICONTROL ID de configuration]** différent et un **[!UICONTROL ID d’organisation]** différent.

## **[!UICONTROL ID de configuration]**

**[!UICONTROL L&#39;ID de configuration]** indique à Adobe Experience Platform où les données doivent être routées et quelles configurations doivent être utilisées sur le serveur. Cela est nécessaire au fonctionnement de l’extension Adobe Experience Platform. Vous pouvez obtenir un ID de configuration en contactant le service à la clientèle.


### **[!UICONTROL ID d’organisation]**

**[!UICONTROL ID d&#39;organisation]** est l&#39;organisation à laquelle vous souhaitez envoyer les données à l&#39;Adobe. La plupart du temps, vous devez utiliser la valeur par défaut renseignée automatiquement. Si vous avez plusieurs instances sur la page, indiquez la valeur de la deuxième organisation à laquelle vous souhaitez envoyer des données.

### **[!UICONTROL Domaine Edge]**

Le **[!UICONTROL domaine Edge]** est le domaine à partir duquel l&#39;extension Adobe Experience Platform envoie et reçoit des données. L’extension exige l’utilisation d’un CNAME propriétaire pour le trafic de production. Le domaine tiers par défaut fonctionne pour les environnements de développement, mais ne convient pas aux environnements de production. Les instructions de configuration d’un CNAME propriétaire sont répertoriées [ici](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html).

### **[!UICONTROL Activer les erreurs]**

En cas d’erreur avec l’extension, l’erreur est consignée par défaut dans la console. Si vous souhaitez masquer les erreurs dans un environnement de production, vous pouvez décocher la case **[!UICONTROL Activer les erreurs]**. Les erreurs seront toujours imprimées lorsque le débogage est activé dans Platform Launch.

### **[!UICONTROL Activer l’inclusion]**

Si **[!UICONTROL Activer l’inclusion]** est activé, l’extension peut contenir les accès jusqu’à ce que l’inclusion soit reçue. L’extension expose une action permettant de définir les préférences de l’inclusion.

### **[!UICONTROL Activer la migration ECID]**

L’extension Platform Web SDK utilise un nouveau cookie pour stocker l’ECID. Ce paramètre assure la compatibilité entre le nouveau cookie et l’ancien cookie à des fins de migration. Adobe recommande vivement de l’activer, sauf si aucun visiteur existant ne dispose d’un ECID.

### **[!UICONTROL Utiliser des cookies tiers]**

Adobe Experience Platform stocke toujours les cookies dans le domaine propriétaire. Cette option vous permet d’utiliser un cookie tiers défini sur demdex.net en plus du cookie du domaine propriétaire. Cela peut s’avérer utile lorsque des utilisateurs se déplacent entre plusieurs domaines. Cela désactive les appels vers demdex.net.

### **[!UICONTROL Contexte]**

L’extension recueille automatiquement des informations sur le contexte de la requête (par exemple, des détails sur l’URL et sur le navigateur). Vous pouvez désactiver cette option en désélectionnant des contextes spécifiques.

- **[!UICONTROL web]**  - Détails sur la page Web tels que l’URL, le parrain, etc.
- **[!UICONTROL périphérique]**  - Détails sur le périphérique, tels que l’orientation de l’écran, la hauteur d’écran et la largeur d’écran.
- **[!UICONTROL environnement]**  - Informations sur l&#39;environnement informatique (Navigateur, connexion, etc.)
- **[!UICONTROL emplacement]**  - Informations limitées sur l&#39;emplacement de l&#39;utilisateur

## Eléments à suivre

1. Définissez [types d&#39;action](action-types.md).
2. Définissez [types d’éléments de données](data-element-types.md).
