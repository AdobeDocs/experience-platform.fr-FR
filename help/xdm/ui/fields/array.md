---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;array;field;
solution: Experience Platform
title: Définition des champs d'un tableau dans l'interface utilisateur
description: Découvrez comment définir un champ de tableau dans l'interface utilisateur de l'Experience Platform.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Définition des champs de tableau dans l’interface utilisateur

Lors de la définition d’un champ de modèle de données d’expérience (XDM) dans l’interface utilisateur de Adobe Experience Platform, vous pouvez désigner ce champ comme tableau.

Le contenu du tableau dépend du [!UICONTROL Type] sélectionné pour ce champ. Par exemple, si [!UICONTROL Type] d&#39;un champ est défini sur &quot;[!UICONTROL String]&quot;, le fait de définir ce champ comme un tableau désigne le champ comme un tableau de chaînes. Si le champ [!UICONTROL Type] est défini sur un type de données à plusieurs champs tel que &quot;[!UICONTROL Adresse postale]&quot;, il deviendra alors un tableau d’objets d’adresse postale conformes au type de données.

Une fois que [a défini un nouveau champ dans l&#39;interface utilisateur](./overview.md#define), vous pouvez le définir en tant que champ de tableau en cochant la case **[!UICONTROL Tableau]** dans le rail de droite.

![](../../images/ui/fields/special/array.png)

Une fois la case à cocher sélectionnée, d&#39;autres commandes apparaissent dans le rail de droite, ce qui vous permet de limiter éventuellement davantage la baie. Si vous ne souhaitez pas appliquer une contrainte particulière, laissez le champ vide.

Les contrôles de configuration supplémentaires pour les baies sont les suivants :

| Propriété de champ | Description |
| --- | --- |
| [!UICONTROL Longueur minimale] | Nombre minimum d&#39;éléments que le tableau doit contenir pour que l&#39;assimilation réussisse. |
| [!UICONTROL Longueur maximale] | Nombre maximal d&#39;éléments que le tableau doit contenir pour que l&#39;assimilation réussisse. |
| [!UICONTROL Éléments uniques uniquement] | Si elle est définie sur &quot;[!UICONTROL True]&quot;, chaque élément du tableau doit être unique pour que l&#39;assimilation soit réussie. |

Une fois le champ configuré, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/array-config.png)

Le canevas se met à jour pour refléter les modifications apportées au champ. Notez que le type de données affiché en regard du nom du champ dans la zone de travail est ajouté avec une paire de crochets (`[]`), indiquant que le champ représente un tableau de ce type de données.

![](../../images/ui/fields/special/array-applied.png)

## Étapes suivantes

Ce guide explique comment définir un champ de tableau dans l&#39;interface utilisateur. Consultez l&#39;aperçu sur [la définition des champs dans l&#39;interface utilisateur](./overview.md#special) pour savoir comment définir d&#39;autres types de champs XDM dans [!DNL Schema Editor].
