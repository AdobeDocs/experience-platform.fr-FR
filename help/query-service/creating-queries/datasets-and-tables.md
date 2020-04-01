---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Datasets vs tables et '
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Datasets vs tables et 

Passez en revue les  des jeux de données disponibles dans l’interface utilisateur [d’](https://platform.adobe.com/datasets)Adobe Experience Platform, en veillant à respecter les noms des jeux de données.
>[!NOTE] Certains noms de jeux de données ont des espaces et pourraient ne pas être sûrs pour SQL.

![](../images/queries/datasets-and-tables/dataset-names.png)


Vérifiez la structure hiérarchique du de jeux de données dans l’interface utilisateur en cliquant sur un nom de dans la table de jeux de données.

![](../images/queries/datasets-and-tables/schema-information.png)

Ouvrez la ligne de commande PSQL et utilisez les détails de la connexion à partir d’ici : [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Pour  les tables disponibles sur Platform avec SQL, vous pouvez utiliser `\d` ou `SHOW TABLES;`.


`\d` affiche le PostgreSQL standard 

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` est une commande personnalisée qui donne un  plus détaillé et présente le tableau, ainsi que le nom du jeu de données figurant dans l’interface utilisateur de la plateforme.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Pour  le racine d’un tableau, utilisez la `\d table_name` commande.

>[!NOTE] Le  présenté présente les champs racine, dont la plupart sont complexes, référencés par un type d’objet dans l’interface utilisateur du de jeux de données.

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

Pour aller plus loin dans le , utilisez des traits de soulignement (`_`) pour déclarer la colonne dans le tableau à décrire. Par exemple : `\d table_name_column`.

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
