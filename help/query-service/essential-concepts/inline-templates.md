---
title: Modèles intégrés
description: Découvrez comment réutiliser plusieurs conditions dans de nombreuses requêtes avec des modèles intégrés.
source-git-commit: f8ec94b4c93e3b36667bdb179ce12c10d20fa30f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Modèles intégrés

Les modèles intégrés permettent de réutiliser plusieurs conditions dans de nombreuses requêtes. Vous pouvez enregistrer les critères dans un modèle, puis les réutiliser dans plusieurs requêtes. Les modèles SQL réutilisables réduisent les efforts de développement et le risque d’erreur lors de la copie d’instructions longues entre requêtes. Avec les modèles intégrés, vous pouvez apporter des modifications dans un emplacement et les faire refléter dans n’importe quelle requête qui référence ce modèle.

Ce document couvre l’utilisation et les limites des modèles intégrés dans Query Editor.

## Conditions préalables

Les modèles intégrés sont pris en charge à la fois par l’interface utilisateur et par l’API Query Service. Avant de poursuivre avec ce guide, lisez la documentation sur la façon de [créer un modèle de requête via l’API ;](../api/query-templates.md#create-a-query-template) ou avec la fonction [Éditeur de requêtes](../ui/user-guide.md#query-authoring).

## Syntaxe du modèle intégré {#syntax}

Une fois une requête enregistrée, elle est appelée modèle. Lorsque le modèle fait référence à un autre modèle dans l’instruction, il est appelé modèle intégré. Les modèles intégrés sont indiqués dans votre code SQL à l’aide du symbole de hachage (#) suivi du nom du modèle. Voici un exemple de cette syntaxe : `#YOUR_TEMPLATE_NAME`.

## Cas d’utilisation {#use-case}

Les modèles SQL suivants montrent l’utilité des modèles intégrés, avec un exemple pour comptabiliser le nombre de clients américains de n’importe quelle région ayant dépensé plus que le &quot;revenu maximum&quot; et commandé avant juin 2023. L’avantage du modèle intégré est que vous pouvez facilement modifier le modèle enfant (dans ce cas, le chiffre d’affaires maximal et la date de commande) et ne pas avoir à modifier le modèle parent.

**Exemple**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Lors de l’exécution de la requête, Query Service remplace le nom du modèle à partir du symbole de hachage par l’instruction SQL du modèle nommé.

>[!NOTE]
>
>Les modèles de requête peuvent appeler n’importe quel autre nombre de modèles intégrés. Il n’existe aucune restriction quant au nombre de modèles intégrés que vous pouvez appeler à partir d’une seule requête. Les modèles peuvent également être imbriqués dans d’autres modèles intégrés.

Vous pouvez utiliser des modèles pour stocker une ou plusieurs conditions. Il n’est pas nécessaire qu’ils constituent eux-mêmes une requête complète. Si votre modèle contient une requête valide, vous pouvez exécuter la requête simplement en appelant le nom du modèle précédé d’un symbole de hachage. Par exemple, si vous avez stocké `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` comme modèle nommé `JUNE_2023_LOYALTY_MEMBERS`, la commande  `#JUNE_2023_LOYALTY_MEMBERS;` exécute la requête valide contenue dans le modèle.

>
>
>Dans l’interface utilisateur de Adobe Experience Platform, les modèles intégrés sous la forme de requêtes paramétrées ne sont pris en charge qu’au niveau parent. Cela signifie que les requêtes paramétrées ne fonctionnent que lorsqu’elles sont utilisées dans le modèle d’origine. Le modèle enfant doit être un modèle statique et ne peut pas comporter de paramètres dynamiques.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment référencer d’autres modèles dans votre SQL, soit dans Query Editor, soit via l’API Query Service.

En outre, vous devez lire le [guide de blocage anonyme](./anonymous-block.md), qui explique comment réduire les surcharges de développement en enchaînant une ou plusieurs instructions SQL exécutées en séquence.
