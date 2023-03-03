---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;déduplication de données;déduplication;
solution: Experience Platform
title: Déduplication des données dans Query Service
type: Tutorial
description: 'Ce document présente des exemples de requêtes d’échantillon complets et sous-sélectionnés pour dédupliquer trois cas d’utilisation courants : événements d’expérience, achats et mesures.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: ht
source-wordcount: '623'
ht-degree: 100%

---

# Déduplication des données dans [!DNL Query Service]

[!DNL Query Service] d’Adobe Experience Platform prend en charge la déduplication des données. La déduplication des données peut être effectuée lorsqu’il est nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble spécifique de champs, car seule une partie des données de la ligne est une information dupliquée.

La déduplication consiste généralement à utiliser la fonction `ROW_NUMBER()` sur une fenêtre pour un identifiant (ou une paire d’identifiants) au cours d’un délai indiqué, ce qui renvoie un nouveau champ qui représente le nombre de fois où un doublon a été détecté. La date est souvent représentée à l’aide du champ `timestamp` [!DNL Experience Data Model] (XDM).

Lorsque la valeur de `ROW_NUMBER()` est `1`, cela fait référence à l’instance d’origine. En règle générale, il s’agit de l’instance que vous souhaitez utiliser. Cela se fait le plus souvent au sein d’une sous-sélection, dans laquelle la déduplication est effectuée avec une requête `SELECT` de niveau supérieur, comme le compte d’agrégats.

Les cas d’utilisation de déduplication peuvent être globaux ou limités à un seul identifiant utilisateur ou utilisateur final dans `identityMap`.

Ce document décrit la procédure de déduplication pour trois cas d’utilisation courants : événements d’expérience, achats et mesures.

Chaque exemple inclut la portée, la clé de fenêtre, une description de la méthode de déduplication, ainsi que la requête SQL complète.

## Événements d’expérience {#experience-events}

Dans le cas de doublons d&#39;événements d&#39;expérience, vous souhaiterez probablement ignorer la ligne entière.

>[!CAUTION]
>
>Pour de nombreux jeux de données dans [!DNL Experience Platform], y compris ceux produits par le connecteur de données Adobe Analytics, la déduplication au niveau des événements d&#39;experience est déjà appliquée. Par conséquent, la réapplication de ce niveau de déduplication est inutile et ralentira votre requête.
>
>Il est important de comprendre la source de vos jeux de données, et de savoir si la déduplication au niveau des événements d&#39;expérience a déjà été appliquée. Pour les jeux de données diffusés en continu (par exemple, ceux d’Adobe Target), vous **devez** appliquer une déduplication au niveau des événements d&#39;expérience car ces sources de données ont des sémantiques « au moins une fois ».

**Portée :** globale

**Clé de la fenêtre :** `id`

### Exemple de déduplication

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Exemple complet

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## Achats {#purchases}

Dans le cas de doublons d’achats, vous souhaiterez probablement conserver la majeure partie de la ligne [!DNL Experience Event], mais ignorer les champs liés à l’achat (comme la mesure `commerce.orders`). Les achats contiennent un champ spécial pour l’identifiant d’achat, qui est `commerce.order.purchaseID`.

Il est recommandé d’utiliser `purchaseID` dans la portée du visiteur ou de la visiteuse, car il s’agit du champ sémantique standard pour les identifiants d’achat dans XDM. La portée du visiteur ou de la visiteuse est recommandée pour supprimer les données d’achat en double, car la requête est plus rapide que l’utilisation de la portée globale et il est peu probable qu’un identifiant d’achat soit dupliqué sur plusieurs identifiants de visiteur ou visiteuse.

**Portée :** visiteur

**Clé de la fenêtre :** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Exemple de déduplication

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

>[!NOTE]
>
>Dans certains cas où les données Analytics d’origine comportent des identifiants d’achat en double sur les identifiants de visiteur ou visiteuse, vous pouvez **peut-être** avoir besoin d’effectuer le comptage d’identifiants d’achat en double pour tous les visiteurs et visiteuses. Lorsque l’identifiant d’achat n’est pas présent, cette méthode nécessite d’inclure une condition qui utilise à la place l’identifiant d’événement pour que la requête soit aussi rapide que possible.

### Exemple complet

L’exemple ci-dessous a recours à une clause de condition pour utiliser l’identifiant d’événement dans le cas où l’identifiant d’achat n’est pas présent.

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## Mesures {#metrics}

Si une mesure utilise l’ID unique facultatif et qu’un doublon de cet ID s’affiche, vous voudrez probablement ignorer cette valeur de mesure et conserver le reste de l’évènement d&#39;expérience.

Dans XDM, la plupart des mesures utilisent le `Measure`type de données qui inclut un champ facultatif`id` que vous pouvez utiliser pour le dédoublonnage.

**Portée :** visiteur

**Clé de la fenêtre :** identityMap[$NAMESPACE].id &amp; id of Measure object

### Exemple de déduplication

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### Exemple complet

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## Étapes suivantes

Ce document fournit des exemples de déduplication des données et décrit comment l’effectuer dans Query Service. Pour obtenir plus de bonnes pratiques relatives à l’écriture de requêtes à l’aide de Query Service, lisez le [guide d’écriture de requêtes](../best-practices/writing-queries.md).
