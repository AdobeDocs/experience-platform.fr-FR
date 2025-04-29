---
title: Créer des audiences à l’aide de SQL
description: Découvrez comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL. Ce guide couvre tous les aspects du cycle de vie des audiences, notamment la création, la mise à jour et la suppression de profils, ainsi que l’utilisation de définitions d’audience pilotées par les données pour cibler les destinations basées sur des fichiers.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 9e16282f9f10733fac9f66022c521684f8267167
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 3%

---

# Créer des audiences à l’aide de SQL

Utilisez l’extension d’audience SQL pour créer des audiences avec des données du lac de données, y compris toutes les entités de dimension existantes (telles que les attributs du client ou les informations sur le produit).

L’utilisation de cette extension SQL améliore votre capacité à créer des audiences, car vous n’avez pas besoin de données brutes dans vos profils lors de la définition des segments d’audience. Les audiences créées à l’aide de cette méthode sont automatiquement enregistrées dans l’espace de travail Audience , où vous pouvez les cibler davantage vers des destinations basées sur des fichiers.

![Infographie présentant le workflow d’extension d’audience SQL. Les étapes incluent la création d’audiences avec Query Service à l’aide de commandes SQL, leur gestion dans l’interface utilisateur d’Experience Platform et leur activation dans des destinations basées sur des fichiers.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

Ce document explique comment utiliser l’extension d’audience SQL dans Adobe Experience Platform Data Distiller pour créer, gérer et publier des audiences à l’aide de commandes SQL.

## Cycle de vie de la création d’audiences dans Data Distiller {#audience-creation-lifecycle}

Pour créer, gérer et activer vos audiences, procédez comme suit. Les audiences créées s’intègrent de manière transparente dans le « flux d’audience ». Vous pouvez ainsi créer des segments à partir d’audiences de base et cibler des destinations basées sur des fichiers (par exemple, des chargements CSV ou des emplacements d’espace de stockage) pour la sensibilisation des clients. « Flux d’audience » fait référence à l’ensemble du processus de création, de gestion et d’activation des audiences, assurant ainsi une intégration transparente entre les destinations.

Dans le cadre de votre « flux d’audience », utilisez les commandes SQL suivantes pour [créer](#create-audience), [modifier](#add-profiles-to-audience) et [supprimer](#delete-audience) des audiences dans Adobe Experience Platform.

### Créer une audience {#create-audience}

Utilisez la commande `CREATE AUDIENCE AS SELECT` pour définir une nouvelle audience. L’audience créée est enregistrée dans un jeu de données et enregistrée dans l’espace de travail [!UICONTROL Audiences] sous Distiller de données.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**Paramètres**

Utilisez les paramètres suivants pour définir votre requête de création d&#39;audience SQL :

| Paramètre | Description |
|--------------------|------------------------------------------------------------------|
| `schema` | Facultatif. Définit le schéma XDM du jeu de données créé par la requête. |
| `table_name` | Nom de la table et de l&#39;audience. |
| `primary_identity` | Indique la colonne d’identité principale pour l’audience. |
| `identity_namespace` | Espace de noms de l’identité. Vous pouvez utiliser un espace de noms existant ou en créer un nouveau. Pour afficher les espaces de noms disponibles, utilisez la commande `SHOW NAMESPACES` . Pour créer un espace de noms, utilisez `CREATE NAMESPACE`. Par exemple : `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | Instruction SELECT définissant l’audience. La syntaxe de la requête SELECT se trouve dans la section [Requêtes SELECT](../sql/syntax.md#select-queries). |

{style="table-layout:auto"}

>[!NOTE]
>
>Pour offrir une plus grande flexibilité pour les structures de données complexes, vous pouvez imbriquer des attributs enrichis lors de la définition des audiences. Les attributs enrichis, tels que `orders`, `total_revenue`, `recency`, `frequency` et `monetization`, peuvent être utilisés pour filtrer les audiences selon les besoins.

**Exemple :**

L&#39;exemple suivant montre comment structurer votre requête de création d&#39;audience SQL :

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

Dans cet exemple, la colonne `userId` est identifiée comme colonne d’identité et un espace de noms approprié (`lumaCrmId`) est attribué. Les colonnes restantes (`orders`, `total_revenue`, `recency`, `frequency` et `monetization`) sont des attributs enrichis qui fournissent un contexte supplémentaire pour l’audience.

**Limites :**

Gardez à l’esprit les limites suivantes lorsque vous utilisez SQL pour la création d’audiences :

- La colonne d’identité principale **doit** se trouve au niveau le plus élevé du jeu de données, sans être imbriquée dans d’autres attributs ou catégories.
- Les audiences externes créées à l’aide de commandes SQL ont une période de conservation de 30 jours. Au bout de 30 jours, ces audiences sont automatiquement supprimées, ce qui est un élément important à prendre en compte pour la planification des stratégies de gestion des audiences.

### Ajouter des profils à une audience existante {#add-profiles-to-audience}

Utilisez la commande `INSERT INTO` pour ajouter des profils (ou des audiences entières) à une audience existante.

```sql
INSERT INTO table_name
SELECT select_query
```

**Paramètres**

Le tableau ci-dessous décrit les paramètres requis pour la commande `INSERT INTO` :

| Paramètre | Description |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | Nom de la table créée dans le cadre de la commande de création d’audience. |
| `select_query` | Instruction SELECT. La syntaxe de la requête SELECT se trouve dans la section Requêtes SELECT. |

{style="table-layout:auto"}

**Exemple :**

L’exemple suivant montre comment ajouter des profils à une audience existante avec la commande `INSERT INTO` :

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### Remplacer les données d&#39;audience (INSERT OVERWRITE) {#replace-audience}

Utilisez la commande `INSERT OVERWRITE INTO` pour remplacer tous les profils existants d’une audience par les résultats d’une nouvelle requête SQL. Cette commande est utile pour gérer les segments d’audience dynamiques en vous permettant d’actualiser entièrement le contenu d’une audience en une seule étape.

>[!AVAILABILITY]
>
>La commande `INSERT OVERWRITE INTO` n’est disponible que pour les clientes et clients de Data Distiller. Pour en savoir plus sur le module complémentaire Distiller de données, contactez votre représentant Adobe.

Contrairement à [`INSERT INTO`](#add-profiles-to-audience), qui s’ajoute à l’audience actuelle, `INSERT OVERWRITE INTO` supprime tous les membres existants de l’audience et insère uniquement ceux renvoyés par la requête. Vous bénéficiez ainsi d’un meilleur contrôle et d’une plus grande flexibilité lors de la gestion des audiences nécessitant des mises à jour fréquentes ou complètes.

Utilisez le modèle de syntaxe suivant pour remplacer une audience par un nouvel ensemble de profils :

```sql
INSERT OVERWRITE INTO audience_name
SELECT select_query
```

**Paramètres**

Le tableau ci-dessous décrit les paramètres requis pour la commande `INSERT OVERWRITE INTO` :

| Paramètre | Description |
|-----------|-------------|
| `audience_name` | Nom de l’audience créée à l’aide de la commande `CREATE AUDIENCE`. |
| `select_query` | Instruction `SELECT` qui définit les profils à inclure dans l’audience. |

**Exemple :**

Dans cet exemple, l’audience `audience_monthly_refresh` est complètement remplacée par les résultats de la requête. Tous les profils non renvoyés par la requête sont supprimés de l’audience.

>[!NOTE]
>
>Un seul chargement par lots doit être associé à l’audience pour que les opérations de remplacement fonctionnent correctement.

```sql
INSERT OVERWRITE INTO audience_monthly_refresh
SELECT user_id FROM latest_transaction_summary WHERE total_spend > 100;
```

#### Comportement de remplacement de l’audience dans le profil client en temps réel

Lorsque vous remplacez une audience, le profil client en temps réel applique la logique suivante pour mettre à jour l’appartenance à un profil :

- Les profils qui apparaissent uniquement dans le nouveau lot sont marqués comme saisis.
- Les profils qui n’existaient que dans le lot précédent sont marqués comme étant sortis.
- Les profils présents dans les deux lots restent inchangés (aucune opération n’est effectuée).

Cela permet de s’assurer que les mises à jour des audiences sont reflétées avec précision dans les systèmes et workflows en aval.

**Exemple de scénario**

Si un `A1` d’audience contient à l’origine :

| Identifiant | NOM |
|----|------|
| A | Vérin |
| B | John |
| C | Martha |

Et la requête de remplacement renvoie :

| Identifiant | NOM |
|----|------|
| A | Stewart |
| C | Martha |

L’audience mise à jour contiendra alors :

| Identifiant | NOM |
|----|------|
| A | Stewart |
| C | Martha |

Le profil B est supprimé, le profil A est mis à jour et le profil C reste inchangé.

Si la requête de remplacement inclut un nouveau profil :

| Identifiant | NOM |
|----|------|
| A | Stewart |
| C | Martha |
| D | Chris |

L’audience finale sera alors :

| Identifiant | NOM |
|----|------|
| A | Stewart |
| C | Martha |
| D | Chris |

### Exemple d’audience de modèle RFM {#rfm-model-audience-example}

L’exemple suivant montre comment créer une audience à l’aide du modèle Récence, fréquence et monétisation (RFM). Cet exemple segmente les clients en fonction de leurs scores de récence, de fréquence et de monétisation pour identifier des groupes clés, tels que les clients fidèles, les nouveaux clients et les clients à forte valeur ajoutée.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

La requête suivante crée un schéma pour l’audience RFM. Le relevé configure des champs pour contenir des informations sur le client telles que `userId`, `days_since_last_purchase`, `orders`, `total_revenue`, etc.

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

Après avoir créé l’audience, renseignez-la avec des données client et segmentez les profils en fonction de leurs scores RFM. L’instruction SQL ci-dessous utilise la fonction `NTILE(4)` pour classer les clients en quartiles en fonction de leurs scores RFM (Récence, Fréquence, Monétisation). Ces scores classent les clients en six segments, tels que « Principal », « Fidèle » et « Baleines ». Les données client segmentées sont ensuite insérées dans le tableau des `adls_rfm_profile` d’audience. »

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

### Supprimer une audience {#delete-audience}

Utilisez la commande `DROP AUDIENCE` pour supprimer une audience existante. Si l’audience n’existe pas, une exception se produit, sauf si `IF EXISTS` est spécifié.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Paramètres**

Le tableau contient les paramètres nécessaires à la commande `DROP AUDIENCE` :

| Paramètre | Description |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Facultatif. Si spécifié, dans le cas où la table est introuvable, aucune exception n&#39;est générée. |
| `db_name` | Indique le groupe de données utilisé pour qualifier le jeu de données d’audience. |
| `table_name` | Nom de la table créée dans le cadre de la commande de création d’audience. |

{style="table-layout:auto"}

**Exemple :**

L’exemple suivant montre comment supprimer une audience à l’aide de la commande DROP AUDIENCE :

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Enregistrement et disponibilité automatiques des audiences {#registration-and-availability}

Les audiences créées à l’aide de l’extension SQL sont automatiquement enregistrées sous la Distiller de données [!UICONTROL Origine] dans l’espace de travail Audience . Une fois enregistrées, ces audiences sont disponibles pour le ciblage dans les destinations basées sur des fichiers, ce qui améliore la segmentation et les stratégies de ciblage. Ce processus ne nécessite aucune configuration supplémentaire, ce qui simplifie la gestion des audiences. Pour plus d’informations sur l’affichage, la gestion et la création d’audiences dans l’interface utilisateur d’Experience Platform, consultez la présentation d’[Audience Portal](../../segmentation/ui/audience-portal.md).

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![L’espace de travail Audience dans Adobe Experience Platform, qui affiche les audiences Data Distiller automatiquement publiées et prêtes à l’emploi.](../images/data-distiller/sql-audiences/audiences.png)

## Activer des audiences vers les destinations {#activate-audiences}

Activez vos audiences en les ciblant vers une destination basée sur des fichiers, telle que [!DNL Amazon S3], [!DNL SFTP] ou [!DNL Azure Blob]. Les attributs d’audience enrichis sont disponibles pour un affinement et un filtrage supplémentaires, si nécessaire.

![Organigramme des types de destination Adobe Experience Platform, présentant les destinations publiques et privées/personnalisées, y compris les options de lot et de diffusion en continu.](../images/data-distiller/sql-audiences/destination-types.png)

## Clarifications des fonctionnalités {#faqs}

Cette section répond aux questions fréquentes sur la création et la gestion des audiences externes à l’aide de SQL dans Data Distiller.

**Questions** :

- La création d’audiences est-elle prise en charge uniquement pour les jeux de données plats ?

+++Réponse

Actuellement, la création de l’audience est limitée aux attributs plats (au niveau racine) lors de la définition de l’audience.

+++

- La création de l’audience entraîne-t-elle la création d’un ou de plusieurs jeux de données ou varie-t-elle selon la configuration ?

+++Réponse

Il existe un mappage direct entre une audience et un jeu de données.

+++

- Le jeu de données créé lors de la création de l’audience est-il marqué pour Profil ?

+++Réponse

Non, le jeu de données créé lors de la création de l’audience n’est pas marqué pour le profil.

+++

- Le jeu de données est-il créé sur le lac de données ?

+++Réponse

Oui, le jeu de données associé à l’audience est créé sur le lac de données. Les attributs de ce jeu de données sont disponibles dans le compositeur d’audience et le flux de destination en tant qu’attributs enrichis.

+++

- Les attributs de l’audience sont-ils limités aux destinations basées sur des fichiers par lots d’entreprise ? (Oui ou Non)

+++Réponse

Non. Les attributs enrichis de l’audience peuvent être utilisés dans les destinations d’entreprise par lots et basées sur des fichiers. Si vous rencontrez une erreur du type « Les identifiants de segment suivants comportent des espaces de noms qui ne sont pas autorisés pour cette destination : e917f626-a038-42f7-944c-xyxyxyx », créez un segment dans Data Distiller et utilisez-le avec toute destination disponible.

+++

- Puis-je créer une audience d’audiences qui utilise une audience de Distiller de données ?

+++Réponse

Oui, vous pouvez créer une audience d’audiences qui utilise une audience de Distiller de données.

+++

- Ces audiences apparaissent-elles dans Adobe Journey Optimizer ? Dans le cas contraire, que se passe-t-il lorsque je crée une audience dans le créateur de règles qui inclut tous les membres de cette audience ?

+++Réponse

Les audiences de Distiller de données sont également disponibles dans Adobe Journey Optimizer. Vous pouvez utiliser les audiences de Distiller de données dans Adobe Journey Optimizer et filtrer les résultats en fonction des attributs enrichis.

+++

- Les audiences du Distiller de données sont-elles supprimées tous les 30 jours, puisqu’il s’agit d’audiences externes ?

+++Réponse

Oui, les audiences du Distiller de données sont supprimées tous les 30 jours, car il s’agit d’audiences externes.

+++

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment utiliser l’extension d’audience SQL dans Data Distiller pour créer, gérer et publier efficacement des audiences à l’aide de commandes SQL. Vous pouvez désormais personnaliser les définitions d’audience en fonction des besoins uniques de votre entreprise et les activer dans différentes destinations, optimisant ainsi vos stratégies marketing et vos décisions axées sur les données.

Vous pouvez ensuite lire la documentation suivante pour développer et optimiser davantage vos stratégies de gestion des audiences Experience Platform :

- **Explorer l’évaluation de l’audience** : découvrez les [méthodes d’évaluation de l’audience dans Adobe Experience Platform](../../segmentation/home.md#evaluate-segments) : segmentation par flux pour les mises à jour en temps réel, segmentation par lots pour le traitement planifié ou à la demande et segmentation Edge pour l’évaluation instantanée sur Edge Network.
- **Intégration aux destinations** : lisez le guide sur la manière d’[exporter des fichiers à la demande vers des destinations par lots](../../destinations/ui/export-file-now.md) à l’aide de l’interface utilisateur des destinations Experience Platform.
- **Revoir les performances des audiences** : analysez les performances de vos audiences définies par SQL sur différents canaux. Utilisez les informations sur les données pour ajuster et améliorer vos définitions d’audience et vos stratégies de ciblage. Lisez le document sur [les informations sur l’audience](../../dashboards/insights/audiences.md) pour savoir comment accéder aux requêtes SQL pour les informations sur l’audience dans Adobe Real-Time CDP et les adapter. Vous pouvez ensuite créer vos propres informations et transformer les données brutes en informations exploitables en personnalisant le tableau de bord des audiences afin de visualiser et d’utiliser efficacement ces informations pour une meilleure prise de décision.

