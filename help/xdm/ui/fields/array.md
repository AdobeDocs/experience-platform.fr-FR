---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;tableau;champ;
solution: Experience Platform
title: Définition des champs de tableau dans l’interface utilisateur
description: Découvrez comment définir un champ de tableau dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# Définition des champs de tableau dans l’interface utilisateur

Lors de la définition d’un champ de modèle de données d’expérience (XDM) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez le désigner comme un tableau.

Le contenu du tableau dépend de la variable [!UICONTROL Type] sélectionné pour ce champ. Par exemple, si un champ de [!UICONTROL Type] est défini sur &quot;[!UICONTROL Chaîne]&quot;, la définition de ce champ en tant que tableau désignera le champ en tant que tableau de chaînes. Si le champ est [!UICONTROL Type] est défini sur un type de données à plusieurs champs tel que &quot;[!UICONTROL Adresse postale]&quot;, il deviendrait alors un tableau d’objets d’adresse postale conformes au type de données.

Après avoir [définition d’un nouveau champ dans l’interface utilisateur](./overview.md#define), vous pouvez la définir en tant que champ de tableau en sélectionnant **[!UICONTROL Tableau]** dans le rail de droite.

![](../../images/ui/fields/special/array.png)

Une fois la case à cocher sélectionnée, d’autres contrôles s’affichent dans le rail de droite, ce qui vous permet de limiter davantage le tableau. Si vous ne souhaitez pas imposer de contrainte spécifique, laissez le champ vide.

Les contrôles de configuration supplémentaires pour les tableaux sont les suivants :

| Propriété du champ | Description |
| --- | --- |
| [!UICONTROL Longueur minimale] | Le nombre minimum d’éléments que le tableau doit contenir pour que l’ingestion soit réussie. |
| [!UICONTROL Longueur maximale] | Nombre maximal d’éléments que le tableau doit contenir pour que l’ingestion soit réussie. |
| [!UICONTROL Éléments uniques uniquement] | Si la variable est définie sur &quot;[!UICONTROL True]&quot;, chaque élément du tableau doit être unique pour que l’ingestion réussisse. |

{style=&quot;table-layout:auto&quot;}

Lorsque vous avez terminé de configurer le champ, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/array-config.png)

Le canevas se met à jour pour prendre en compte les modifications apportées au champ. Notez que le type de données affiché en regard du nom du champ dans la zone de travail est ajouté avec une paire de crochets (`[]`), indiquant que le champ représente un tableau de ce type de données.

![](../../images/ui/fields/special/array-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ de tableau dans l’interface utilisateur. Consultez la présentation sur [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champ XDM dans [!DNL Schema Editor].
