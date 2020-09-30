---
keywords: Experience Platform;home;popular topics;query service;Query service;datasets;tables;schemas;
solution: Experience Platform
title: Jeux de données par rapport aux tableaux et schémas
topic: queries
type: Tutorial
description: Ce document contient des informations sur l'affichage de vos jeux de données dans la structure du schéma de jeux de données et l'utilisation des commandes PostgreSQL.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 84%

---


# Jeux de données par rapport aux tableaux et schémas

Consultez la liste des jeux de données disponibles dans l’[interface utilisateur d’Adobe Experience Platform](https://platform.adobe.com/datasets), en vous assurant d’observer les noms des jeux de données.
>[!NOTE]
>
>Certains noms de jeux de données possèdent des espaces et peuvent ne pas être compatibles avec SQL dans le cas contraire.

![](../images/queries/datasets-and-tables/dataset-names.png)


Vérifiez la structure hiérarchique du schéma du jeu de données dans l’interface utilisateur en cliquant sur un nom de schéma dans le tableau des jeux de données.

![](../images/queries/datasets-and-tables/schema-information.png)

Ouvrez la ligne de commande PSQL et utilisez les détails de la connexion que vous trouverez ici : [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

To view the available tables on [!DNL Platform] with SQL, you can use either `\d` or `SHOW TABLES;`.


`\d` affiche la vue PostgreSQL standard

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;`[!DNL Platform] est une commande personnalisée qui apporte une vue plus détaillée et présente le tableau ainsi que le nom du jeu de données qui apparaît dans l’interface utilisateur de 

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Pour afficher le schéma racine d’un tableau, utilisez la commande `\d table_name`.

>[!NOTE]
>
>Le schéma présenté présente les champs racine, dont la plupart sont complexes, référencés par un type d’objet dans l’interface utilisateur du schéma de jeux de données.

`\d luma_midvalues`

```sql
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

Pour aller plus loin dans le schéma, utilisez des traits de soulignement (`_`) pour déclarer la colonne dans le tableau que vous souhaitez décrire. Par exemple : `\d table_name_column`.

`\d luma_midvalues_web`

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
