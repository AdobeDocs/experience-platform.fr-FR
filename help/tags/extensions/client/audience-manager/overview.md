---
title: Présentation de l’extension Adobe Audience Manager
description: Découvrez lʼextension de balises d’Adobe Audience Manager dans Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
TQID: https://experienceleague.adobe.com/4fU8whgMl6AX1tmn2rIV5YAokblPJIAOF5U8zlfwQh0
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 100%

---

# Présentation de l’extension Adobe Audience Manager

Avec l’extension de balises d’Audience Manager, vous pouvez intégrer le code DIL utilisé par Audience Manager à vos propriétés dans Adobe Experience Platform

Utilisez cette référence pour obtenir des informations sur les options disponibles lors de l’utilisation de cette extension pour créer une règle.

>[!NOTE]
>
>Cette extension n’est pas destinée à être utilisée pour le transfert d’événement des données d’Adobe Analytics. Pour le transfert d’événement, utilisez [l’extension Adobe Analytics](../analytics/overview.md).

## Configuration de l’extension Adobe Audience Manager

Si l’extension Adobe Audience Manager n’est pas encore installée, ouvrez votre propriété, puis cliquez sur **[!UICONTROL Extensions > Catalog]**, survolez l’extension Adobe Audience Manager avec la souris et cliquez sur **[!UICONTROL Install]**.

Pour configurer l’extension, ouvrez l’onglet [!UICONTROL Extensions], survolez l’extension avec la souris, puis cliquez sur **[!UICONTROL Configure]**.

### Paramètres DIL

Configurez vos paramètres DIL. Les options de configuration disponibles sont les suivantes :

![](../../../images/ext-aam-config.png)

#### Version de DIL

Affiche la version de la Data Integration Library (« Bibliothèque d’intégration de données », ou DIL).

Ce paramètre ne peut pas être modifié.

#### Exclusion de chemins d’accès spécifiques

Si l’URL correspond à l’un des chemins exclus, l’extension n’est pas chargée.

Cliquez sur **[!UICONTROL Add Path]** pour spécifier une URL exclue.

Activez les Regex si l’URL est une expression régulière.

#### Utilisation du module Site Catalyst pour DIL

Le [module SiteCatalyst](https://experiencecloud.adobe.com/resources/help/fr_FR/aam/r_dil_sc_init.html) fonctionne avec la DIL pour envoyer des éléments de balises Analytics à Audience Manager.

Utilisez l’éditeur de code pour configurer le fichier siteCatalyst.init.

Vous pouvez aussi créer une note contenant des informations sur cette configuration.

#### Utilisation du module Google Analytics pour DIL

Activez le [module Google Analytics](https://experiencecloud.adobe.com/resources/help/fr_FR/aam/dil-google-universal-analytics.html).

#### Propriétés d’initialisation DIL.create

Ajoutez les propriétés d’initialisation utilisées par [DIL.create](https://experiencecloud.adobe.com/resources/help/fr_FR/aam/r_dil_create.html) et la sous-propriété de l’espace de noms pour l’[objet visitorService](https://experiencecloud.adobe.com/resources/help/fr_FR/aam/r_dil_visitor_service.html). Dans l’éditeur de code, deux exemples d’utilisation sont inclus dans les commentaires de code.

Cliquez sur **[!UICONTROL Choose an Item]** pour ajouter des propriétés supplémentaires.

Survolez les icônes « i » avec la souris pour connaître les fonctions de chaque propriété. Vous trouverez plus d’informations sur les propriétés dans la [documentation DIL pour Audience Manager](https://experiencecloud.adobe.com/resources/help/fr_FR/aam/r_dil_create.html).

Cliquez sur **[!UICONTROL Save]** quand vous avez fini de configurer l’extension.

## Types d’actions de l’extension Adobe Audience Manager

Cette section décrit les types d’actions disponibles dans l’extension Audience Manager.

L’extension Adobe Audience Manager permet d’effectuer les actions suivantes dans la partie « Then » d’une règle :

### Exécuter un code personnalisé

Exécutez le code personnalisé configuré dans l’éditeur de code.

Saisissez le code de votre choix dans l’éditeur de code, puis attribuez un nom au code. Ce code sera disponible dans la partie « Then » du créateur de règles.

![](../../../images/ext-aam-then.png)

Vous pouvez aussi ajouter une note avec des informations sur cette configuration.
