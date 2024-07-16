---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;tableau;champ;
solution: Experience Platform
title: Définition des champs de tableau dans l’interface utilisateur
description: Découvrez comment définir un champ de tableau dans l’interface utilisateur de l’Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Définition des champs de tableau dans l’interface utilisateur

Lors de la définition d’un champ de modèle de données d’expérience (XDM) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le désigner comme un tableau.

Le contenu du tableau dépend du [!UICONTROL Type] sélectionné pour ce champ. Par exemple, si le [!UICONTROL Type] d’un champ est défini sur &quot;[!UICONTROL String]&quot;, la définition de ce champ en tant que tableau désignera le champ comme un tableau de chaînes. Si le champ [!UICONTROL Type] est défini sur un type de données à plusieurs champs tel que &quot;[!UICONTROL Adresse postale]&quot;, il deviendra un tableau d’objets d’adresse postale conformes au type de données.

Après avoir [défini un nouveau champ dans l’interface utilisateur](./overview.md#define), vous pouvez le définir comme champ de tableau en cochant la case **[!UICONTROL Tableau]** dans le rail de droite.

![](../../images/ui/fields/special/array.png)

Une fois la case à cocher sélectionnée, d’autres contrôles s’affichent dans le rail de droite, ce qui vous permet de limiter davantage le tableau. Si vous ne souhaitez pas imposer de contrainte spécifique, laissez le champ vide.

Les contrôles de configuration supplémentaires pour les tableaux sont les suivants :

| Propriété du champ | Description |
| --- | --- |
| [!UICONTROL Longueur minimale] | Le nombre minimum d’éléments que le tableau doit contenir pour que l’ingestion soit réussie. |
| [!UICONTROL Longueur maximale] | Le nombre maximal d’éléments que le tableau doit contenir pour que l’ingestion soit réussie. |
| [!UICONTROL Éléments uniques uniquement] | Si celle-ci est définie sur &quot;[!UICONTROL True]&quot;, chaque élément du tableau doit être unique pour que l’ingestion soit réussie. |

{style="table-layout:auto"}

Une fois que vous avez fini de configurer le champ, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/array-config.png)

Le canevas se met à jour pour prendre en compte les modifications apportées au champ. Notez que le type de données affiché en regard du nom du champ dans la zone de travail est ajouté avec une paire de crochets (`[]`), indiquant que le champ représente un tableau de ce type de données.

![](../../images/ui/fields/special/array-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ de tableau dans l’interface utilisateur. Consultez la présentation de la [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans [!DNL Schema Editor].
