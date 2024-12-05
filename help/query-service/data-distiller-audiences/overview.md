---
title: Création d’audiences à l’aide de SQL
description: Découvrez comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL. Ce guide couvre tous les aspects du cycle de vie de l’audience, notamment la création, la mise à jour et la suppression de profils, ainsi que l’utilisation de définitions d’audience pilotées par les données pour cibler des destinations basées sur des fichiers.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 7db055f598e3fa7d5a50214a0cfa86e28e5bfe47
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 1%

---

# Création d’audiences à l’aide de SQL

Utilisez l’extension d’audience SQL pour créer des audiences avec des données du lac de données, y compris toute entité de dimension existante (comme les attributs du client ou les informations sur les produits).

L’utilisation de cette extension SQL améliore votre capacité à créer des audiences, car vous n’avez pas besoin de données brutes dans vos profils lors de la définition de segments d’audience. Les audiences créées à l’aide de cette méthode sont automatiquement enregistrées dans l’espace de travail Audience, où vous pouvez les cibler davantage vers des destinations basées sur des fichiers.

![Infographie montrant le workflow d’extension de l’audience SQL. Les étapes incluent la création d’audiences avec Query Service à l’aide de commandes SQL, leur gestion dans l’interface utilisateur de Platform, afin de les activer dans des destinations basées sur des fichiers.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

Ce document explique comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL.

## Cycle de vie de la création d’audience dans Data Distiller {#audience-creation-lifecycle}

Pour créer, gérer et activer vos audiences, procédez comme suit. Les audiences créées s’intègrent de manière transparente dans le &quot;flux d’audience&quot;, de sorte que vous puissiez créer des segments à partir des audiences de base et des destinations basées sur des fichiers cibles (par exemple, les chargements CSV ou les emplacements de stockage dans le cloud) pour la sensibilisation des clients. Le &quot;flux d’audience&quot; fait référence à l’ensemble du processus de création, de gestion et d’activation d’audiences, assurant une intégration transparente entre les destinations.

Dans le cadre de votre &quot;flux d’audience&quot;, utilisez les commandes SQL suivantes pour [créer](#create-audience), [modifier](#add-profiles-to-audience) et [supprimer](#delete-audience) des audiences dans Adobe Experience Platform.

### Créer une audience {#create-audience}

Utilisez la commande `CREATE AUDIENCE AS SELECT` pour définir une nouvelle audience. L’audience créée est enregistrée dans un jeu de données et enregistrée dans l’espace de travail [!UICONTROL Audiences] sous Data Distiller.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**Paramètres**

Utilisez ces paramètres pour définir votre requête de création d&#39;audience SQL :

| Paramètre | Description |
|--------------------|------------------------------------------------------------------|
| `schema` | Facultatif. Définit le schéma XDM du jeu de données créé par la requête. |
| `table_name` | Nom de la table et de l&#39;audience. |
| `primary_identity` | Indique la colonne d’identité principale de l’audience. |
| `identity_namespace` | Espace de noms de l’identité. Vous pouvez utiliser un espace de noms existant ou en créer un nouveau. Pour afficher les espaces de noms disponibles, utilisez la commande `SHOW NAMESPACE`. Pour créer un espace de noms, utilisez `CREATE NAMESPACE`. Par exemple : `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | Une instruction SELECT définissant l’audience. La syntaxe de la requête SELECT se trouve dans la section [Requêtes SELECT](../sql/syntax.md#select-queries) . |

{style="table-layout:auto"}

>[!NOTE]
>
>Pour offrir une plus grande flexibilité pour les structures de données complexes, vous pouvez imbriquer des attributs enrichis lors de la définition d’audiences. Les attributs enrichis, tels que `orders`, `total_revenue`, `recency`, `frequency` et `monetization`, peuvent être utilisés pour filtrer les audiences selon les besoins.

**Exemple :**

L&#39;exemple suivant montre comment structurer votre requête de création d&#39;audience SQL :

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

Dans cet exemple, la colonne `userId` est identifiée en tant que colonne d’identité et un espace de noms approprié (`lumaCrmId`) est affecté. Les autres colonnes (`orders`, `total_revenue`, `recency`, `frequency` et `monetization`) sont des attributs enrichis qui fournissent un contexte supplémentaire pour l’audience.

**Limites :**

Tenez compte des limites suivantes lors de l’utilisation de SQL pour la création d’audience :

- La colonne d’identité principale **doit** se trouver au niveau le plus élevé du jeu de données, sans être imbriquée dans d’autres attributs ou catégories.
- Les audiences externes créées à l’aide de commandes SQL ont une période de conservation de 30 jours. Au bout de 30 jours, ces audiences sont automatiquement supprimées, ce qui est un élément important de la planification des stratégies de gestion de l’audience.

### Ajout de profils à une audience existante {#add-profiles-to-audience}

Utilisez la commande `INSERT INTO` pour ajouter des profils (ou des audiences entières) à une audience existante.

```sql
INSERT INTO table_name
SELECT select_query
```

**Paramètres**

Le tableau ci-dessous explique les paramètres requis pour la commande `INSERT INTO` :

| Paramètre | Description |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | Nom de la table qui a été créée dans le cadre de la commande de création d’audience. |
| `select_query` | Instruction SELECT. La syntaxe de la requête SELECT se trouve dans la section Requêtes SELECT . |

{style="table-layout:auto"}

**Exemple :**

L’exemple suivant montre comment ajouter des profils à une audience existante avec la commande `INSERT INTO` :

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### Exemple d’audience de modèle RFM {#rfm-model-audience-example}

L’exemple suivant montre comment créer une audience à l’aide du modèle Récence, Fréquence et Monétisation (RFM) . Cet exemple segmente les clients en fonction de leur taux de récence, de fréquence et de monétisation afin d’identifier les groupes clés, tels que les clients fidèles, les nouveaux clients et les clients à forte valeur ajoutée.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

La requête suivante crée un schéma pour l’audience RFM. L’instruction configure des champs pour contenir les informations sur les clients telles que `userId`, `days_since_last_purchase`, `orders`, `total_revenue`, etc.

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

Après avoir créé l’audience, renseignez-la avec les données client et segmentez les profils en fonction de leurs scores RFM. L’instruction SQL ci-dessous utilise la fonction `NTILE(4)` pour classer les clients en quartiles en fonction de leurs scores RFM (récence, fréquence, monétisation). Ces scores classent les clients en six segments, tels que &quot;Core&quot;, &quot;Loyal&quot; et &quot;Whales&quot;. Les données client segmentées sont alors insérées dans la table `adls_rfm_profile` de l&#39;audience.&quot;

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
```

### Suppression d’une audience (DROP AUDIENCE) {#delete-audience}

Utilisez la commande `DROP AUDIENCE` pour supprimer une audience existante. Si l’audience n’existe pas, une exception se produit, sauf si `IF EXISTS` est spécifié.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Paramètres**

La table contient les paramètres requis pour la commande `DROP AUDIENCE` :

| Paramètre | Description |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Facultatif. Si spécifié, dans le cas où la table est introuvable, aucune exception n’est générée. |
| `db_name` | Indique le groupe de données utilisé pour qualifier le jeu de données d’audience. |
| `table_name` | Nom de la table qui a été créée dans le cadre de la commande de création d’audience. |

{style="table-layout:auto"}

**Exemple :**

L’exemple suivant montre comment supprimer une audience à l’aide de la commande DROP AUDIENCE :

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Enregistrement et disponibilité automatiques des audiences {#registration-and-availability}

Les audiences créées à l’aide de l’extension SQL sont automatiquement enregistrées sous Data Distiller [!UICONTROL Origin] dans l’espace de travail Audience. Une fois enregistrées, ces audiences sont disponibles pour le ciblage dans des destinations basées sur des fichiers, ce qui améliore la segmentation et les stratégies de ciblage. Ce processus ne nécessite aucune configuration supplémentaire, ce qui rationalise la gestion de l’audience. Pour plus d’informations sur la manière d’afficher, de gérer et de créer des audiences dans l’interface utilisateur de Platform, consultez la [présentation d’Audience Portal](../../segmentation/ui/audience-portal.md).

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![L’espace de travail Audience dans Adobe Experience Platform, présentant les audiences Distiller de données automatiquement publiées et prêtes à l’emploi.](../images/data-distiller/sql-audiences/audiences.png)

## Activer des audiences vers les destinations {#activate-audiences}

Activez vos audiences en les ciblant sur n’importe quelle destination basée sur des fichiers, telle que [!DNL Amazon S3], [!DNL SFTP] ou [!DNL Azure Blob]. Les attributs d’audience enrichis peuvent être affinés et filtrés selon les besoins.

![ Diagramme de flux des types de destinations Adobe Experience Platform, présentant les destinations publiques et privées/personnalisées, y compris les options de lot et de diffusion en continu.](../images/data-distiller/sql-audiences/destination-types.png)

## Clarifications des fonctionnalités {#faqs}

Cette section traite des questions fréquentes sur la création et la gestion d’audiences externes à l’aide de SQL dans Data Distiller.

**Questions** :

- La création d’audience est-elle prise en charge uniquement pour les jeux de données plats ?

+++Réponse

Actuellement, la création de l’audience est limitée aux attributs plats (au niveau racine) lors de la définition de l’audience.

+++

- La création d’audience génère-t-elle un ou plusieurs jeux de données uniques ou varie-t-elle en fonction de la configuration ?

+++Réponse

Il existe un mappage un-à-un entre une audience et un jeu de données.

+++

- Le jeu de données créé lors de la création de l’audience est-il marqué pour Profile ?

+++Réponse

Non, le jeu de données créé lors de la création de l’audience n’est pas marqué pour Profile.

+++

- Le jeu de données est-il créé sur le lac de données ?

+++Réponse

Oui, le jeu de données associé à l’audience est créé sur le lac de données. Les attributs de ce jeu de données sont disponibles dans le compositeur d’audience et le flux de destination sous forme d’attributs enrichis.

+++

- Les attributs de l’audience sont-ils limités aux destinations basées sur des fichiers de lot d’entreprise ? (Oui ou Non)

+++Réponse

Non. Les attributs enrichis dans l’audience peuvent être utilisés dans des destinations par lots d’entreprise et des destinations basées sur des fichiers. Si vous rencontrez une erreur du type &quot;Les identifiants de segment suivants ont des espaces de noms non autorisés pour cette destination : e917f626-a038-42f7-944c-xyxyx&quot;, créez un segment dans Data Distiller et utilisez-le avec n’importe quelle destination disponible.

+++

- Puis-je créer une audience d’audiences qui utilise une audience Distiller de données ?

+++Réponse

Oui, vous pouvez créer une audience qui utilise une audience Distiller de données.

+++

- Ces audiences s’affichent-elles dans Adobe Journey Optimizer ? Dans le cas contraire, que se passe-t-il lorsque je crée une audience dans le créateur de règles qui inclut tous les membres de cette audience ?

+++Réponse

Les audiences Distiller de données sont également disponibles dans Adobe Journey Optimizer. Vous pouvez utiliser les audiences Distiller de données dans Adobe Journey Optimizer et filtrer les résultats en fonction des attributs enrichis.

+++

- Les audiences Data Distiller sont-elles supprimées tous les 30 jours puisqu’elles sont des audiences externes ?

+++Réponse

Oui, les audiences Distiller de données sont supprimées tous les 30 jours puisqu’il s’agit d’audiences externes.

+++

## Étapes suivantes

Après avoir lu ce document, vous avez appris à utiliser l’extension d’audience SQL dans Data Distiller pour créer, gérer et publier efficacement des audiences à l’aide de commandes SQL. Vous pouvez désormais personnaliser les définitions d’audience en fonction de vos besoins commerciaux uniques et les activer dans différentes destinations, afin d’optimiser vos stratégies marketing et vos décisions basées sur les données.

Vous pouvez ensuite lire la documentation suivante pour développer et optimiser vos stratégies de gestion de l’audience Platform :

- **Explorer l’évaluation de l’audience** : découvrez les [méthodes d’évaluation de l’audience dans Adobe Experience Platform](../../segmentation/home.md#evaluate-segments) : segmentation par flux pour les mises à jour en temps réel, segmentation par lots pour le traitement planifié ou à la demande et segmentation de périphérie pour l’évaluation instantanée sur l’Edge Network.
- **Intégration avec les destinations** : lisez le guide sur l’[exportation de fichiers à la demande vers des destinations par lot](../../destinations/ui/export-file-now.md) à l’aide de l’interface utilisateur Destinations de plateforme.
- **Réviser les performances de l’audience** : analysez les performances de vos audiences définies par SQL sur différents canaux. Utilisez les informations sur les données pour ajuster et améliorer vos définitions d’audience et vos stratégies de ciblage. Lisez le document sur [Audience insights](../../dashboards/insights/audiences.md) pour savoir comment accéder aux requêtes SQL et les adapter aux informations sur les audiences dans Adobe Real-Time CDP. Vous pouvez ensuite créer vos propres insights et transformer les données brutes en informations exploitables en personnalisant le tableau de bord Audiences afin de visualiser et d’utiliser efficacement ces informations pour une meilleure prise de décision.

