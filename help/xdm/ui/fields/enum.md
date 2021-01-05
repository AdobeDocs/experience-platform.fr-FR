---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;enum;field;
solution: Experience Platform
title: Définition d’un champ d’énumération dans l’interface utilisateur
description: Découvrez comment définir un champ d’énumération dans l’interface utilisateur de l’Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Définition d’un champ d’énumération dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ d’énumération représente un champ limité à une liste prédéfinie de valeurs acceptables.

Lorsque [vous définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le définir en tant que champ d’énumération en cochant la case **[!UICONTROL Enum]** dans le rail de droite.

![](../../images/ui/fields/special/enum.png)

D’autres contrôles s’affichent après avoir coché la case, ce qui vous permet de spécifier les contraintes de valeur pour l’énumération. Sous la colonne **[!UICONTROL Valeur]**, vous devez indiquer la valeur exacte à laquelle vous souhaitez contraindre le champ. Cette valeur doit être conforme au [!UICONTROL Type] que vous avez sélectionné pour le champ enum. Vous pouvez également fournir une étiquette **[!UICONTROL conviviale]** pour la contrainte.

Pour ajouter des contraintes supplémentaires à l&#39;énumération, sélectionnez **[!UICONTROL Ajouter la ligne]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continuez à ajouter les contraintes souhaitées et les étiquettes facultatives à l’énumération. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer les modifications au schéma.

![](../../images/ui/fields/special/enum-configured.png)

La trame se met à jour pour refléter les modifications. Lorsque vous explorerez ce schéma dans le futur, vous pourrez vue et modifier les contraintes du champ enum dans le rail de droite.

![](../../images/ui/fields/special/enum-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ d’énumération dans l’interface utilisateur. Consultez l&#39;aperçu sur [la définition des champs dans l&#39;interface utilisateur](./overview.md#special) pour savoir comment définir d&#39;autres types de champs XDM dans [!DNL Schema Editor].