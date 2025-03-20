---
title: Modèles intégrés
description: Découvrez comment réutiliser plusieurs conditions dans de nombreuses requêtes à l’aide de modèles intégrés.
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: ef4c7f20710f56ca0de7c0dfdb99751ff2fe8ebe
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 100%

---

# Modèles intégrés

Les modèles intégrés permettent de réutiliser plusieurs conditions dans une multitude de requêtes. Vous pouvez enregistrer les critères dans un modèle, puis les réutiliser dans plusieurs requêtes. Les modèles SQL réutilisables permettent de réduire les efforts de développement et le risque d’erreur lors de la copie de longues instructions entre les requêtes. Grâce aux modèles intégrés, apportez des modifications à un seul emplacement et reflétez ces modifications dans toutes les requêtes qui font référence à ce modèle.

Ce document couvre l’utilisation et les limites des modèles intégrés dans Query Editor.

## Conditions préalables

Les modèles intégrés sont pris en charge par l’interface utilisateur et par l’API Query Service. Avant de poursuivre avec ce guide, lisez la documentation sur la façon de [créer un modèle de requête via l’API](../api/query-templates.md#create-a-query-template) ou à l’aide de [Query Editor](../ui/user-guide.md#query-authoring).

## Syntaxe du modèle intégré {#syntax}

Une fois une requête enregistrée, elle devient un modèle. Lorsque le modèle fait référence à un autre modèle dans l’instruction, il est appelé modèle intégré. Les modèles intégrés sont indiqués dans le code SQL à l’aide du symbole de hachage (#) suivi du nom du modèle. Exemple de cette syntaxe : `#YOUR_TEMPLATE_NAME`.

## Cas d’utilisation {#use-case}

Les modèles SQL suivants montrent toute l’utilité des modèles intégrés. Consultez un exemple permettant de comptabiliser le nombre de clientes et clients américains, de n’importe quel état, ayant dépensé plus que le « chiffre d’affaires maximal » et placé une commande avant juin 2023. L’avantage du modèle intégré est le suivant : vous pouvez facilement modifier le modèle enfant (dans ce cas, le chiffre d’affaires maximal et la date de commande), sans devoir modifier le modèle parent.

**Exemple**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Lors de l’exécution de la requête, Query Service remplace le nom du modèle par le symbole de hachage suivi de l’instruction SQL du modèle nommé.

>[!NOTE]
>
>Les modèles de requête peuvent appeler n’importe quel autre nombre de modèles intégrés. Il n’existe aucune restriction quant au nombre de modèles intégrés que vous pouvez appeler à partir d’une seule requête. Les modèles peuvent également être imbriqués dans d’autres modèles intégrés.

Vous pouvez utiliser des modèles pour stocker une ou plusieurs conditions. Il n’est pas nécessaire qu’ils constituent à eux seuls une requête complète. Si votre modèle contient une requête valide, vous pouvez exécuter la requête simplement en appelant le nom du modèle précédé d’un symbole de hachage. Par exemple, si vous avez stocké `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` comme modèle nommé `JUNE_2023_LOYALTY_MEMBERS`, la commande `#JUNE_2023_LOYALTY_MEMBERS;` exécute la requête valide contenue dans le modèle.

>[!NOTE]
>
>Dans l’interface utilisateur d’Adobe Experience Platform, les modèles intégrés sous la forme de requêtes paramétrées ne sont pris en charge qu’au niveau parent. Cela signifie que les requêtes paramétrées ne fonctionnent que lorsqu’elles sont utilisées dans le modèle d’origine. Le modèle enfant doit être un modèle statique et ne peut pas comporter de paramètres dynamiques. Consultez la [documentation des requêtes paramétrées](../ui/parameterized-queries.md) pour en savoir plus.

## Étapes suivantes

À la lecture de ce document, vous savez désormais comment référencer d’autres modèles dans votre requête SQL, soit dans Query Editor, soit via l’API Query Service.

Consultez également le [guide des blocs anonymes](./anonymous-block.md) et découvrez comment réduire les efforts de développement en enchaînant une ou plusieurs instructions SQL exécutées en séquence.
