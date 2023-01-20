---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;déduplication des données;déduplication ;
solution: Experience Platform
title: Déduplication des données dans Query Service
type: Tutorial
description: 'Ce document présente des exemples de requêtes de sous-sélection et d’échantillon complet pour dédupliquer trois cas d’utilisation courants : Événements d’expérience, achats et mesures.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 15%

---

# Déduplication des données dans [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] prend en charge la déduplication des données. La déduplication des données peut être effectuée lorsqu’il est nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble spécifique de champs, car seule une partie des données de la ligne est une duplication des informations.

La déduplication consiste généralement à utiliser la variable `ROW_NUMBER()` d’une fenêtre pour un identifiant (ou une paire d’identifiants) au fil du temps ordonné, ce qui renvoie un nouveau champ qui représente le nombre de fois où un doublon a été détecté. L’heure est souvent représentée à l’aide de la variable [!DNL Experience Data Model] (XDM) `timestamp` champ .

Lorsque la valeur de la variable `ROW_NUMBER()` is `1`, il fait référence à l’instance d’origine. En règle générale, il s’agit de l’instance que vous souhaitez utiliser. Cela se fait le plus souvent au sein d’une sous-sélection, dans laquelle le dédoublonnage est effectué avec une requête `SELECT` de niveau supérieur, comme le compte d’agrégats.

Les cas d’utilisation de déduplication peuvent être globaux ou limités à un seul utilisateur ou un identifiant d’utilisateur final dans la variable `identityMap`.

Ce document décrit la procédure de déduplication pour trois cas d’utilisation courants : Événements d’expérience, achats et mesures.

Chaque exemple inclut le périmètre, la clé de fenêtre, une composition de la méthode de déduplication, ainsi que la requête SQL complète.

## Événements Experience {#experience-events}

Dans le cas d’événements d’expérience en double, vous souhaiterez probablement ignorer la ligne entière.

>[!CAUTION]
>
>De nombreux jeux de données dans [!DNL Experience Platform], y compris ceux produits par le connecteur de données Adobe Analytics, applique déjà le dédoublonnage au niveau de l’événement d’expérience. Par conséquent, la réapplication de ce niveau de dédoublonnage est inutile et ralentira votre requête.
>
>Il est important de comprendre la source de vos jeux de données et de savoir si le dédoublonnage au niveau de l’événement d’expérience a déjà été appliqué. Pour tous les jeux de données diffusés en continu (par exemple, ceux d’Adobe Target), vous **will** Vous devez appliquer un dédoublonnage au niveau de l’événement d’expérience, car ces sources de données ont une sémantique &quot;au moins une fois&quot;.

**Portée :** globale

**Clé de la fenêtre :** `id`

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

Si vous avez des achats en double, vous souhaiterez probablement conserver la plupart des [!DNL Experience Event] , mais ignorez les champs liés à l’achat (tels que la variable `commerce.orders` ). Les achats contiennent un champ spécial pour l’identifiant d’achat, qui est `commerce.order.purchaseID`.

Il est recommandé d’utiliser `purchaseID` dans la portée du visiteur, car il s’agit du champ sémantique standard pour les identifiants d’achat dans XDM. La portée du visiteur est recommandée pour supprimer les données d’achat en double, car la requête est plus rapide que l’utilisation de la portée globale et il est peu probable qu’un identifiant d’achat soit dupliqué sur plusieurs identifiants de visiteur.

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
>Dans certains cas où les données Analytics d’origine comportent des identifiants d’achat en double pour les identifiants visiteur, vous **may** Vous devez effectuer le comptage en double des identifiants d’achat pour tous les visiteurs. Lorsque l’identifiant d’achat n’est pas présent, cette méthode nécessite d’inclure une condition qui, au lieu de cela, utilise l’identifiant d’événement pour que la requête soit aussi rapide que possible.

### Exemple complet

L’exemple ci-dessous utilise une clause de condition pour utiliser l’identifiant d’événement dans le cas où l’identifiant d’achat n’est pas présent.

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

Si une mesure utilise l’identifiant unique facultatif et qu’un doublon de cet identifiant apparaît, vous voudrez probablement ignorer cette valeur de mesure et conserver le reste de l’événement d’expérience.

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

Ce document fournit des exemples de déduplication des données et décrit comment effectuer la déduplication des données dans Query Service. Pour plus d’informations sur les bonnes pratiques relatives à l’écriture de requêtes à l’aide de Query Service, veuillez lire la section [guide d’écriture de requêtes](../best-practices/writing-queries.md).
