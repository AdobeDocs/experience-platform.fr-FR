---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;énumération;champ;
solution: Experience Platform
title: Définition des champs d’énumération dans l’interface utilisateur
description: Découvrez comment définir un champ d’énumération dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Définition des champs d’énumération dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ d’énumération représente un champ limité à une liste prédéfinie de valeurs acceptables.

Lorsque vous [définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le définir comme champ d’énumération en cochant la case **[!UICONTROL Enum]** dans le rail de droite.

![](../../images/ui/fields/special/enum.png)

D’autres contrôles s’affichent après avoir coché la case, ce qui vous permet de spécifier les contraintes de valeur pour l’énumération. Sous la colonne **[!UICONTROL Valeur]**, vous devez indiquer la valeur exacte à laquelle vous souhaitez limiter le champ. Cette valeur doit être conforme au [!UICONTROL type] que vous avez sélectionné pour le champ d’énumération. Vous pouvez également fournir un **[!UICONTROL Libellé]** convivial pour la contrainte.

Pour ajouter des contraintes supplémentaires à l’énumération, sélectionnez **[!UICONTROL Ajouter une ligne]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continuez à ajouter les contraintes souhaitées et les libellés facultatifs à l’énumération. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer les modifications au schéma.

![](../../images/ui/fields/special/enum-configured.png)

Le canevas se met à jour pour refléter les modifications. Lorsque vous explorez ce schéma à l’avenir, vous pouvez afficher et modifier les contraintes du champ d’énumération dans le rail de droite.

![](../../images/ui/fields/special/enum-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ d’énumération dans l’interface utilisateur. Consultez la présentation sur la [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans la [!DNL Schema Editor].
