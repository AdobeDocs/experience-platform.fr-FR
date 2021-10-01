---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;obligatoire;champ;
solution: Experience Platform
title: Définition des champs obligatoires dans l’interface utilisateur
description: Découvrez comment définir un champ XDM obligatoire dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 1%

---

# Définition des champs requis dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ obligatoire indique qu’il doit recevoir une valeur valide pour qu’un enregistrement ou un événement de série temporelle particulier soit accepté lors de l’ingestion des données. Les cas d’utilisation courants pour les champs obligatoires incluent les informations d’identité de l’utilisateur et les horodatages.

Lorsque vous [définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le définir comme un champ obligatoire en cochant la case **[!UICONTROL Obligatoire]** dans le rail de droite. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/required.png)

Une fois le champ appliqué, son chemin apparaît sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche. Si le champ est imbriqué, tous les champs parents s’affichent également selon les besoins.

![](../../images/ui/fields/special/required-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ obligatoire dans l’interface utilisateur. Consultez la présentation sur la [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans la [!DNL Schema Editor].
