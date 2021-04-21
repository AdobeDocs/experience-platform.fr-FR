---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API
title: Exemples d’Expressions PQL pour les attributs calculés
topic-legacy: guide
type: Documentation
description: Les attributs calculés sont des fonctions utilisées pour agrégat des données au niveau du événement en attributs au niveau du profil. Ces fonctions nécessitent l’utilisation d’expressions PQL (Profil Requête Language) valides. Ce guide décrit certaines des expressions PQL les plus couramment utilisées pour les attributs calculés.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha) Exemples d’expressions PQL pour les attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé est actuellement en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Dans Adobe Experience Platform, les attributs calculés sont des fonctions utilisées pour agrégat des données au niveau du événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation. Chaque attribut calculé est défini avec des informations de base, telles qu&#39;un nom et une description, la classe de schéma et le chemin d&#39;accès au champ dans lequel la valeur sera conservée, ainsi qu&#39;une expression, dont la valeur calculée est la valeur que vous souhaitez stocker dans l&#39;attribut calculé.

Les expressions utilisées dans les attributs calculés sont créées à l’aide de [!DNL Profile Query Language] (PQL), un langage de requête compatible avec le modèle de données d’expérience (XDM) conçu pour prendre en charge la définition et l’exécution de requêtes pour les données de Profil client en temps réel.

Les attributs calculés prennent actuellement en charge les fonctions suivantes : sum, count, min, max et booléen. Ce guide décrit certaines des expressions PQL les plus couramment utilisées que vous pouvez utiliser lors de la définition de vos propres attributs calculés pour votre organisation. Pour plus d&#39;informations sur PQL et des liens vers d&#39;autres directives de mise en forme et des exemples de requêtes prises en charge, consultez la [présentation PQL](../../segmentation/pql/overview.md).

## Expressions de diffusion en continu

Le tableau suivant fournit des détails sur les expressions de requête couramment utilisées prises en charge en mode de diffusion en continu.

| Description | Expression PQL | Type d’entrée : <br/>Profil ou Événement d’expérience (EE[]) | Type de résultat |
|---|---|---|---|
| Nombre de téléchargements d’images au cours des 7 derniers jours. | xEvent[(l&#39;horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;download&quot; et contentType = &quot;image&quot;].count() | Profil et EE[] | Entier |
| Somme des clients dépensés pour des articles de sport au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].sum(commerce.order.priceTotal) | Profil et EE[] | Entier ou Doublon |
| Les clients dépensent en moyenne pour les articles de sport au cours des 7 derniers jours.<br/><br/>**Remarque :** Nécessite la création de trois attributs calculés. | **ca1:** xEvent[(l’horodatage survient  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(l’horodatage survient  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()ca3:ca1 / ca2]]<br/><br/>**** | Profil et EE[] | Double |
| Le client a-t-il dépensé plus de 100 $ en biens sportifs au cours des 7 derniers jours ?<br/><br/>**Remarque :** Nécessite la création de deux attributs calculés. | **ca1:** xEvent[(l’horodatage se produit  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Profil et EE[] | Booléen |
| Le client a-t-il effectué un achat au cours des 7 derniers jours ? | chain(xEvent, horodatage, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 jours auparavant)]) | Profil et EE[] | Booléen |
| Les dépenses les plus faibles des utilisateurs pour les articles de sport au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].min(commerce.order.priceTotal) | Profil et EE[] | Entier ou Doublon |
| Les plus gros consommateurs dépensent dans les produits sportifs au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].max(commerce.order.priceTotal) | Profil et EE[] | Entier ou Doublon |
| Nombre de téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexé par produit. | xEvent[(l&#39;horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()) | Profil et EE[] | Map[String, Integer] |
| Somme de la propriété numérique sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexée par produit. | xEvent[(l&#39;horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)) | Profil et EE[] | Map[String, Integer] ou Map[String, Doublon] |
| Moyenne des propriétés numériques sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexées par produit.<br/><br/>**Remarque :** Nécessite la création de trois attributs calculés. | **ca1:** xEvent[(l’horodatage se produit  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(l’horodatage se produit  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => map Entry(K, G))))ca3:ca2 / ca1]]<br/><br/>**** | Profil et EE[] | Carte[Chaîne, Doublon] |
| Nombre minimum de propriétés numériques sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexées par produit. | xEvent[(l&#39;horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Profil et EE[] | Map[String, Integer] ou Map[String, Doublon] |
| Nombre maximal de propriétés numériques sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexées par produit. | xEvent[(l&#39;horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Profil et EE[] | Map[String, Integer] ou Map[String, Doublon] |
| Expression numérique sur le profil, et non sur les événements. | if(person.gender = &quot;women&quot;, 60, 65) | Profile | Entier ou Doublon |
| Expression booléenne sur le profil, et non sur les événements. | person.bornYear >= 2000 | Profil | Booléen |
| Expression de chaîne sur le profil, et non sur les événements. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profil | Chaîne |

## Expressions du lot

Le tableau suivant fournit des détails sur les expressions d’requête qui ne sont disponibles qu’en mode batch, ce qui signifie qu’elles ne sont actuellement pas disponibles en flux continu.

| Description | Expression PQL | Type d’entrée : <br/>Profil ou Événement d’expérience (EE[]) | Type de résultat |
|---|---|---|---|
| Indique si la somme des expressions numériques sur les téléchargements de produits au cours des 7 derniers jours dépasse 100, indexée par produit. | xEvent[(horodatage survenant &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profil et EE[] | Map[String, Boolean] |
| Indique si la moyenne de l’expression numérique sur les téléchargements de produits au cours des 7 derniers jours dépasse 100, indexée par produit. | xEvent[(horodatage survenant &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Profil et EE[] | Map[String, Boolean] |
| Cumul de différentes mesures pour chaque produit téléchargé, au cours des 7 derniers jours, indexé par produit. | xEvent[(l&#39;horodatage a lieu &lt; 7 jours auparavant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot; : G.sum(commerce.order.priceTotal)}) | Profil et EE[] | Map[String, Object] où Object est un type XDM personnalisé |
