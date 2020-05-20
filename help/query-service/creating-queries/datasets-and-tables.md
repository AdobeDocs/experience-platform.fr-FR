---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Jeu de données vs tables et schémas
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# Jeu de données vs tables et schémas

Vérifiez la liste des jeux de données disponibles dans l’interface utilisateur [d’](https://platform.adobe.com/datasets)Adobe Experience Platform, en veillant à respecter les noms des jeux de données.
>[!NOTE] Certains noms de jeux de données comportent des espaces et pourraient autrement ne pas être sûrs pour SQL.

![](../images/queries/datasets-and-tables/dataset-names.png)


Examinez la structure hiérarchique du schéma de jeux de données dans l’interface utilisateur en cliquant sur le nom d’un schéma dans la table de jeux de données.

![](../images/queries/datasets-and-tables/schema-information.png)

Ouvrez la ligne de commande PSQL et utilisez les détails de la connexion à partir d’ici : [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Pour vue des tables disponibles sur la plateforme avec SQL, vous pouvez utiliser soit `\d` , soit `SHOW TABLES;`.


`\d` affiche la vue PostgreSQL standard

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` est une commande personnalisée qui fournit une vue plus détaillée et présente le tableau, ainsi que le nom du jeu de données figurant dans l’interface utilisateur de la plate-forme.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Pour vue au schéma racine d&#39;une table, utilisez la `\d table_name` commande.

>[!NOTE] Le schéma présenté montre les champs racine, dont la plupart sont complexes, référencés par un type d’objet dans l’interface utilisateur du schéma de dataset.

`\d luma_midvalues`

```
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Pour aller plus loin dans le schéma, utilisez des traits de soulignement (`_`) pour déclarer la colonne dans le tableau à décrire. Par exemple : `\d table_name_column`.

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
