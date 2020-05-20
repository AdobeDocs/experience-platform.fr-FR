---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identity Service d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 1%

---


# Présentation de l&#39;espace de nommage d&#39;identité

Les espaces de nommage d&#39;identité sont un composant du service [d&#39;](./home.md) identité qui sert d&#39;indicateur du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur de &quot;name<span>@email.com&quot; en tant qu’adresse électronique ou de &quot;443522&quot; en tant qu’identifiant CRM numérique.

## Prise en main

L’utilisation d’espaces de nommage d’identité nécessite une compréhension des différents services Adobe Experience Platform impliqués. Avant de commencer à travailler avec des espaces de nommage, veuillez consulter la documentation relative aux services suivants :

- [Profil](../profile/home.md)client en temps réel : Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Service](./home.md)d&#39;identité : Obtenez une meilleure vue des clients individuels et de leur comportement en rapprochant les identités entre les périphériques et les systèmes.
- [Privacy Service](../privacy-service/home.md): Les espaces de nommage d&#39;identité sont utilisés pour se conformer au Règlement général sur la protection des données (RGPD), où les demandes de RGPD peuvent être faites par rapport à un espace de nommage.

## Comprendre les espaces de nommage d&#39;identité

Une identité pleinement qualifiée comprend une valeur d’identifiant et un espace de nommage. Lors de la mise en correspondance de données d’enregistrement entre des fragments de profil, comme lorsque le Profil client en temps réel fusionne des données de profil, la valeur d’identité et l’espace de nommage doivent correspondre.

Par exemple, deux fragments de profil peuvent contenir des identifiants principaux différents mais ils partagent la même valeur pour l’espace de nommage &quot;E-mail&quot;. Par conséquent, Platform peut voir que ces fragments sont en fait le même individu et rassembler les données dans le graphique d’identité de l’individu.

![](images/identity-service-stitching.png)

### Types d’identité

Les données peuvent être identifiées par différents types d&#39;identité. Le type d&#39;identité est spécifié au moment de la création de l&#39;espace de nommage d&#39;identité et contrôle si les données sont conservées ou non sur le graphique d&#39;identité, ainsi que toute instruction spéciale sur la manière de gérer ces données.

Les types d&#39;identité suivants sont disponibles dans Platform :

| Type d&#39;identité | Description |
| --- | --- |
| Cookie | Ces identités sont essentielles à l&#39;expansion et constituent la majorité du graphique d&#39;identité. Cependant, par nature, ils se désintègrent rapidement et perdent leur valeur au fil du temps. La suppression des cookies est gérée spécialement dans le graphique d&#39;identité. |
| Périphériques croisés | Cela indique que Identity Service doit considérer qu&#39;il s&#39;agit d&#39;un identifiant de personne puissant et donc le préserver pour toujours. Par exemple, un identifiant de connexion, un identifiant de gestion de la relation client, un identifiant de fidélité, etc. |
| Device | Inclut les identifiants IDFA, GAID et autres identifiants IOT. Ceux-ci peuvent être partagés par les ménages. |
| Courriel | Les identités de ce type incluent des informations d’identification personnelle (PII). Il s&#39;agit d&#39;une indication au service d&#39;identité pour qu&#39;il traite la valeur de façon sensible. |
| Mobile | Les identités de ce type incluent les informations d’identification personnelle. Il s&#39;agit d&#39;une indication au service d&#39;identité pour qu&#39;il traite la valeur de façon sensible. |
| Non-personnes | Utilisé pour stocker les identifiants qui ont besoin d’espaces de nommage, mais qui ne sont pas liés à une grappe de personnes. Ces identifiants sont ensuite filtrés à partir du graphique d’identité. Les cas d&#39;utilisation possibles incluent les données relatives aux produits, organisations, magasins, etc. (Par exemple, un SKU de produit.) |
| Téléphone | Les identités de ce type incluent les informations d’identification personnelle. Ceci indique au service d’identité de gérer la valeur de manière sensible. |

### espaces de nommage standard

Adobe Experience Platform fournit plusieurs espaces de nommage d’identité disponibles pour toutes les entreprises. Ils sont appelés espaces de nommage standard et sont visibles à l’aide de l’API Identity Service ou via l’interface utilisateur de la plate-forme.

Pour vue des espaces de nommage standard dans l’interface utilisateur, cliquez sur **Identités** dans le rail de gauche, puis cliquez sur l’onglet *Parcourir* . Tous les espaces de nommage d’identité accessibles à votre organisation s’affichent, mais ceux dont le propriétaire est Standard sont les espaces de nommage standard fournis par Adobe.

Vous pouvez ensuite cliquer sur l’un des espaces de nommage répertoriés pour obtenir les détails de la vue.

![](./images/standard-namespace-detail.png)

## Gestion des espaces de nommage de votre organisation

Selon les données de votre organisation et les cas d’utilisation, vous pouvez avoir besoin d’espaces de nommage personnalisés.

Ils sont visibles dans l’interface utilisateur sous la forme des espaces de nommage dont le &quot;propriétaire&quot; est défini sur &quot;Personnalisé&quot;. Les espaces de nommage personnalisés peuvent être créés à l&#39;aide de l&#39;API Identity Service ou via l&#39;interface utilisateur.

Pour créer un espace de nommage personnalisé à l’aide de l’interface utilisateur, cliquez sur **Créer un espace de nommage** d’identité, puis complétez la boîte de dialogue et cliquez sur **Créer**.

Les Espaces de nommage que vous définissez sont privés à votre organisation et nécessitent un &quot;symbole d’identité&quot; unique (ou &quot;code&quot; si vous utilisez l’API) pour être créés avec succès.

![](./images/create-identity-namespace.png)

Comme pour les espaces de nommage standard, vous pouvez cliquer sur un espace de nommage personnalisé dans l’onglet *Parcourir* pour en vue les détails. Toutefois, avec un espace de nommage personnalisé, vous pouvez également modifier son nom d’affichage et sa description dans la zone de détails.

>[!NOTE] Une fois un espace de nommage créé, il ne peut plus être supprimé et son &quot;symbole d’identité&quot; (ou &quot;code&quot; dans l’API) et son &quot;type&quot; ne peuvent plus être modifiés.

## Espaces de nommage des données d&#39;identité

La fourniture de l&#39;espace de nommage pour une identité dépend de la méthode que vous utilisez pour fournir les données d&#39;identité. Pour plus d&#39;informations sur la fourniture de données d&#39;identité, reportez-vous à la section relative à la [fourniture de données](./home.md#supplying-identity-data-to-identity-service) d&#39;identité dans la présentation du service d&#39;identité.
