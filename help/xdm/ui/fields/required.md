---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
solution: Experience Platform
title: Définir un champ obligatoire dans l’interface utilisateur
description: Découvrez comment définir un champ XDM obligatoire dans l’interface utilisateur de l’Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 48025fc11558bf6773ce5c48054483758c7e993f
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 1%

---


# Définir un champ obligatoire dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ obligatoire indique qu’il doit être fourni une valeur valide pour qu’un enregistrement ou un événement de série chronologique particulier soit accepté lors de l’assimilation des données. Les cas d’utilisation courants pour les champs obligatoires incluent les informations d’identité de l’utilisateur et les horodatages.

Lorsque [vous définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le définir comme champ obligatoire en cochant la case **[!UICONTROL Obligatoire]** dans le rail de droite. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/required.png)

Une fois le champ appliqué, son chemin apparaît sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche. Si le champ est imbriqué, tous les champs parents s’affichent également selon les besoins.

![](../../images/ui/fields/special/required-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ obligatoire dans l’interface utilisateur. Consultez l&#39;aperçu sur [la définition des champs dans l&#39;interface utilisateur](./overview.md#special) pour savoir comment définir d&#39;autres types de champs XDM dans [!DNL Schema Editor].