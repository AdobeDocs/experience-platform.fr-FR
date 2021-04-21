---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;enum;field;
solution: Experience Platform
title: Définition des champs Enum dans l’interface utilisateur
description: Découvrez comment définir un champ d’énumération dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Définition des champs d’énumération dans l’interface utilisateur

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
