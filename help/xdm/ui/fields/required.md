---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;obligatoire;champ;
title: Définition des champs obligatoires dans l’interface utilisateur
description: Découvrez comment définir un champ XDM obligatoire dans l’interface utilisateur de l’Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Définition des champs requis dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ obligatoire indique qu’il doit recevoir une valeur valide pour qu’un enregistrement ou un événement de série temporelle particulier soit accepté lors de l’ingestion des données. Les cas d’utilisation courants pour les champs obligatoires incluent les informations d’identité de l’utilisateur et les horodatages.

>[!IMPORTANT]
>
>Qu’un champ de schéma soit obligatoire ou non, Platform n’accepte pas `null` ou les valeurs vides pour un champ ingéré. S’il n’existe aucune valeur pour un champ particulier dans un enregistrement ou un événement, la clé de ce champ doit être exclue de la charge utile d’ingestion.

Lorsque [vous définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le définir comme champ obligatoire en cochant la case **[!UICONTROL Obligatoire]** dans le rail de droite. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![Case à cocher requise](../../images/ui/fields/required/root.png)

Si le champ est un attribut de niveau racine sous l’objet ID du client, son chemin d’accès apparaît immédiatement sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche.

![Champ racine requis](../../images/ui/fields/required/applied.png)

Toutefois, si un champ obligatoire est imbriqué dans un objet qui n’est pas marqué comme obligatoire, le champ imbriqué n’apparaît pas sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche.

Dans l’exemple ci-dessous, le champ `internalSKU` est défini comme requis, mais pas son objet parent `SKUs`. Dans ce cas, aucune erreur de validation ne se produirait si `SKUs` est exclu lors de l’ingestion de données, même si le champ enfant `internalSKU` est marqué comme obligatoire. En d’autres termes, même si `SKUs` est facultatif, il doit contenir un champ `internalSKU` dans l’événement qu’il est inclus.

![Champ obligatoire imbriqué](../../images/ui/fields/required/nested.png)

Si vous souhaitez qu’un champ imbriqué soit toujours requis dans un schéma, vous devez également définir tous les champs parents selon les besoins (à l’exception de l’objet d’identifiant du client).

![Champs requis parents et enfants](../../images/ui/fields/required/parent-and-child.png)

## Étapes suivantes

Ce guide explique comment définir un champ obligatoire dans l’interface utilisateur. Consultez la présentation de la [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans [!DNL Schema Editor].
