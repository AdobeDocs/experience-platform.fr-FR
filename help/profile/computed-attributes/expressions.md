---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Exemples d’expressions PQL pour les attributs calculés
topic-legacy: guide
type: Documentation
description: Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions nécessitent l’utilisation d’expressions PQL (Profile Query Language) valides. Ce guide décrit certaines des expressions PQL les plus couramment utilisées pour les attributs calculés.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 4%

---

# (Alpha) Exemples d’expressions PQL pour les attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé est actuellement en version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Dans Adobe Experience Platform, les attributs calculés sont des fonctions utilisées pour agréger les données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Chaque attribut calculé est défini avec des informations de base, telles qu’un nom et une description, la classe de schéma et le chemin d’accès au champ dans lequel la valeur sera conservée, ainsi qu’une expression, dont la valeur calculée est la valeur que vous souhaitez stocker dans l’attribut calculé.

Les expressions utilisées dans les attributs calculés sont créées à l’aide de [!DNL Profile Query Language] (PQL), langage de requête compatible avec Experience Data Model (XDM) conçu pour prendre en charge la définition et l’exécution de requêtes pour les données Real-time Customer Profile.

Les attributs calculés prennent actuellement en charge les fonctions suivantes : sum, count, min, max et boolean. Ce guide décrit certaines des expressions PQL les plus courantes que vous pouvez utiliser lors de la définition de vos propres attributs calculés pour votre organisation. Pour plus d’informations sur PQL et des liens vers des instructions de formatage supplémentaires et des exemples de requêtes prises en charge, consultez la section [Présentation de PQL](../../segmentation/pql/overview.md).

## Expressions en continu

Le tableau suivant fournit des détails sur les expressions de requête courantes prises en charge dans le mode de diffusion en continu.

| Description | Expression PQL | Type d&#39;entrée :<br/>Profil ou événement d’expérience (EE)[]) | Type de résultat |
|---|---|---|---|
| Nombre de téléchargements d’images au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot; et contentType = &quot;image&quot;].count() | Profil et EE[] | Nombre entier |
| Somme des dépenses des clients pour les produits de sport au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].sum(commerce.order.priceTotal) | Profil et EE[] | Entier ou double |
| Moyenne des dépenses des clients pour les produits sportifs au cours des 7 derniers jours.<br/><br/>**Remarque :** Nécessite la création de trois attributs calculés. | **ca1 :** xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2 :** xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].count()<br/><br/>**ca3 :** ca1 / ca2 | Profil et EE[] | Double |
| Le client a-t-il dépensé plus de 100 dollars pour les produits sportifs ces 7 derniers jours ?<br/><br/>**Remarque :** Nécessite la création de deux attributs calculés. | **ca1 :** xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2 :** ca1 > 100 | Profil et EE[] | Booléen |
| Le client a-t-il effectué un achat au cours des 7 derniers jours ? | chain(xEvent, horodatage, [A : WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 jours avant maintenant)]) | Profil et EE[] | Booléen |
| Les consommations les plus faibles sur les produits sportifs des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].min(commerce.order.priceTotal) | Profil et EE[] | Entier ou double |
| Les dépenses les plus élevées des utilisateurs pour les produits sportifs au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;transaction&quot; et catégorie = &quot;biens sportifs&quot;].max(commerce.order.priceTotal) | Profil et EE[] | Entier ou double |
| Nombre de téléchargements de chaque produit téléchargé, indexé par produit, au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Profil et EE[] | Carte[Chaîne, Entier] |
| Somme de la propriété numérique sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexée par produit. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)) | Profil et EE[] | Carte[Chaîne, Entier] ou Carte[Chaîne, double] |
| Moyenne de la propriété numérique sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexée par produit.<br/><br/>**Remarque :** Nécessite la création de trois attributs calculés. | **ca1 :** xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))<br/><br/>**ca2 :** xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3 :** ca2/ca1 | Profil et EE[] | Carte[Chaîne, double] |
| Minimum de la propriété numérique sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexé par produit. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Profil et EE[] | Carte[Chaîne, Entier] ou Carte[Chaîne, double] |
| Maximum de la propriété numérique sur les téléchargements de chaque produit téléchargé, au cours des 7 derniers jours, indexé par produit. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Profil et EE[] | Carte[Chaîne, Entier] ou Carte[Chaîne, double] |
| Expression numérique sur le profil, sans référencer d’événements. | if(person.gender = &quot;female&quot;, 60, 65) | Profile | Entier ou double |
| Expression booléenne sur le profil, ne faisant pas référence aux événements. | person.birthYear >= 2000 | Profile | Booléen |
| Expression de chaîne sur le profil, sans référencer d’événements. | if(homeAddress.countryCode dans [&quot;US&quot;, &quot;MX&quot;, &quot;CA&quot;], &quot;NA&quot;, &quot;LIGNE&quot;) | Profile | Chaîne |

## Expressions de lots

Le tableau suivant fournit des détails sur les expressions de requête disponibles uniquement en mode batch, ce qui signifie qu’elles ne sont actuellement pas disponibles en flux continu.

| Description | Expression PQL | Type d&#39;entrée :<br/>Profil ou événement d’expérience (EE)[]) | Type de résultat |
|---|---|---|---|
| Indique si la somme des expressions numériques par rapport aux téléchargements de produits au cours des 7 derniers jours dépasse 100, indexée par produit. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100) | Profil et EE[] | Carte[Chaîne, booléen] |
| Indique si la moyenne des expressions numériques par rapport aux téléchargements de produits au cours des 7 derniers jours dépasse 100, indexée par produit. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100) | Profil et EE[] | Carte[Chaîne, booléen] |
| Cumul de différentes mesures pour chaque produit téléchargé, indexé par produit au cours des 7 derniers jours. | xEvent[(l’horodatage a lieu &lt; 7 jours avant maintenant) et eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Profil et EE[] | Carte[Chaîne, objet] où Object est un type XDM personnalisé |
