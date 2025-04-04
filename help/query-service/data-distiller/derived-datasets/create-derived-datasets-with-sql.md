---
title: Créer des jeux de données dérivés avec SQL
description: Découvrez comment utiliser SQL pour créer un jeu de données dérivé activé pour le profil et comment utiliser le jeu de données pour le profil client en temps réel et le service de segmentation.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 2%

---

# Créer des jeux de données dérivés avec SQL

Découvrez comment utiliser des requêtes SQL pour manipuler et transformer des données à partir de jeux de données existants afin de créer un jeu de données dérivé activé pour Profile. Ce workflow fournit une méthode alternative efficace pour créer des jeux de données dérivés pour vos cas d’utilisation professionnels de profil client en temps réel.

Ce document décrit diverses extensions SQL pratiques qui génèrent un jeu de données dérivé à utiliser avec le profil client en temps réel. Le workflow simplifie le processus que vous auriez autrement dû effectuer par le biais de divers appels API ou d’interactions avec l’interface utilisateur d’Experience Platform.

En règle générale, la génération et la publication d’un jeu de données dérivé pour le profil client en temps réel impliquent les étapes suivantes :

* Créez un espace de noms d’identité, s’il n’existe pas déjà.
* Créez le type de données pour stocker le jeu de données dérivé, si nécessaire.
* Créez un groupe de champs avec ce type de données pour stocker les informations du jeu de données dérivé.
* Créez ou affectez une colonne d’identité principale avec l’espace de noms créé précédemment.
* Créez un schéma à l’aide du groupe de champs et du type de données créés précédemment.
* Créez un jeu de données à l’aide de votre schéma et activez-le pour le profil, si nécessaire.
* Vous pouvez éventuellement marquer un jeu de données comme activé pour le profil.

Après avoir suivi les étapes mentionnées ci-dessus, vous êtes prêt à renseigner le jeu de données. Si vous avez activé le jeu de données pour le profil, vous pouvez également créer des segments qui font référence au nouveau jeu de données et commencer à produire des informations.

Query Service vous permet d’effectuer toutes les actions répertoriées ci-dessus à l’aide de requêtes SQL. Cela inclut d’apporter des modifications à vos jeux de données et groupes de champs si nécessaire.

## Création d’une table avec une option permettant de l’activer pour le profil {#enable-dataset-for-profile}

>[!NOTE]
>
>La requête SQL fournie ci-dessous suppose l’utilisation d’un espace de noms préexistant.

Utilisez une requête CTAS (Create Table as Select) pour créer un jeu de données, attribuer des types de données, définir une identité principale, créer un schéma et le marquer comme activé pour les profils. L’exemple d’instruction SQL ci-dessous crée un jeu de données et le rend disponible pour Real-Time Customer Data Platform (Real-Time CDP). Votre requête SQL suit le format illustré dans l’exemple ci-dessous :

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Les types de données pris en charge sont les suivants : booléen, date, datetime, texte, flottant, bigint, entier, mappage, tableau et struct/row.

Le bloc de code SQL ci-dessous fournit des exemples pour définir les types de données struct/row, map et array. La ligne 1 illustre la syntaxe des lignes. La ligne 2 illustre la syntaxe de mappage et la ligne 3, la syntaxe de tableau.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Les jeux de données peuvent également être activés pour le profil via l’interface utilisateur d’Experience Platform. Pour plus d’informations sur le marquage d’un jeu de données comme étant activé pour le profil, consultez la documentation [activer un jeu de données pour le profil client en temps réel](../../../catalog/datasets/user-guide.md#enable-profile).

Dans l’exemple de requête ci-dessous, le jeu de données `decile_table` est créé avec `id` comme colonne d’identité principale et l’espace de noms est `IDFA`. Il comporte également un champ nommé `decile1Month` de type de données map. La table créée (`decile_table`) est activée pour le profil.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Une fois la requête exécutée, l’identifiant du jeu de données est renvoyé à la console, comme illustré dans l’exemple ci-dessous.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Utilisez `label='PROFILE'` sur une commande `CREATE TABLE` pour créer un jeu de données activé pour le profil. La fonctionnalité `upsert` est activée par défaut. La fonctionnalité `upsert` peut être remplacée à l’aide de la commande `ALTER`, comme illustré dans l’exemple ci-dessous.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Consultez la documentation sur la syntaxe SQl pour plus d’informations sur l’utilisation de la commande [ALTER TABLE](../../sql/syntax.md#alter-table) et de [label dans le cadre d’une requête CTAS](../../sql/syntax.md#create-table-as-select).

## Construit pour faciliter la gestion des jeux de données dérivés via SQL

Les fonctionnalités décrites ci-dessous sont très utiles lors de la gestion de jeux de données dérivés via SQL.

### Modifier les jeux de données existants à activer pour le profil {#enable-existing-dataset-for-profile}

La structure SQL ALTER TABLE peut être utilisée pour rendre les jeux de données existants activés pour le profil. Pour ce faire, une balise activée pour le profil doit être ajoutée au schéma et au jeu de données correspondant.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Une fois la commande `ALTER TABLE` exécutée, la console renvoie `ALTER SUCCESS`.

### Ajouter une identité principale à un jeu de données existant {#add-primary-identity}

Marquez une colonne existante dans un jeu de données comme jeu d’identités principal. Dans le cas contraire, une erreur se produit. Pour définir une identité principale à l’aide de SQL, utilisez le format de requête affiché ci-dessous.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Par exemple :

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

Dans l’exemple fourni, `id2` est une colonne existante dans `test1_dataset`.

### Désactivation d’un jeu de données pour le profil {#disable-dataset-for-profile}

Si vous souhaitez désactiver le tableau pour les utilisateurs de profil, vous devez utiliser la commande DROP. Vous trouverez ci-dessous un exemple d’instruction SQL USE `DROP`.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Par exemple :

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Cette instruction SQL fournit une méthode alternative efficace à l’utilisation d’un appel API. Pour plus d’informations, consultez la documentation sur la [désactivation d’un jeu de données en vue de son utilisation avec Real-Time CDP à l’aide de l’API des jeux de données](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Autoriser la mise à jour et l’insertion de fonctionnalités pour votre jeu de données {#enable-upsert-functionality-for-dataset}

La commande UPSERT permet d&#39;insérer un nouvel enregistrement ou de mettre à jour les données existantes dans une table. Plus précisément, il vous permet de mettre à jour une ligne existante si une valeur spécifiée existe déjà dans un tableau, ou d&#39;insérer une nouvelle ligne si la valeur spécifiée n&#39;existe pas déjà.

Vous trouverez ci-dessous un exemple d’instruction utilisant le bon format.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Par exemple :

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Cette instruction SQL fournit une méthode alternative efficace à l’utilisation d’un appel API. Pour plus d’informations, consultez la documentation sur la [activation d’un jeu de données en vue de son utilisation avec Real-Time CDP et UPSERT à l’aide de l’API des jeux de données](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Désactiver la fonctionnalité de mise à jour et d’insertion pour votre jeu de données {#disable-upsert-functionality-for-dataset}

Cette commande désactive la possibilité de mettre à jour et d’insérer des lignes dans votre jeu de données.

Vous trouverez ci-dessous un exemple d’instruction utilisant le bon format.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Par exemple :

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Afficher les informations supplémentaires associées à chaque table {#show-labels-for-tables}

Des métadonnées supplémentaires sont conservées pour les jeux de données activés pour le profil. Utilisez la commande `SHOW TABLES` pour afficher une colonne `labels` supplémentaire qui fournit des informations sur les libellés associés aux tableaux.

Vous trouverez ci-dessous un exemple de sortie de cette commande :

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Dans l’exemple, vous pouvez constater que le `table_with_a_decile` a été activé pour le profil et appliqué avec des libellés tels que [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) comme décrit précédemment.

### Créer un groupe de champs avec SQL

Les groupes de champs peuvent désormais être créés à l’aide de SQL. Vous aurez ainsi la possibilité d’utiliser l’éditeur de schémas dans l’interface utilisateur d’Experience Platform ou d’effectuer un appel API vers le registre des schémas.

Vous trouverez ci-dessous un exemple d’instruction permettant de créer un groupe de champs.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>La création d’un groupe de champs via SQL échoue si l’indicateur `label` n’est pas fourni dans l’instruction ou si le groupe de champs existe déjà.
>Assurez-vous que la requête inclut une clause `IF NOT EXISTS` pour éviter l’échec de la requête, car le groupe de champs existe déjà.

Un exemple concret peut ressembler à celui illustré ci-dessous.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

L’exécution réussie de cette instruction renvoie l’identifiant du groupe de champs créé. Par exemple `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Pour plus d’informations sur les autres méthodes](../../../xdm/ui/resources/field-groups.md#create) consultez la documentation sur la [création d’un groupe de champs dans l’éditeur de schémas ou sur l’utilisation de l’API [schema Registry](../../../xdm/api/field-groups.md#create).

### Déposer un groupe de champs

Il peut parfois être nécessaire de supprimer un groupe de champs du registre des schémas. Pour ce faire, exécutez la commande `DROP FIELDGROUP` avec l’identifiant du groupe de champs .

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Par exemple :

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>La suppression d’un groupe de champs via SQL échoue si le groupe de champs n’existe pas. Assurez-vous que l’instruction inclut une clause `IF EXISTS` pour éviter l’échec de la requête.

### Afficher tous les noms et identifiants de groupes de champs pour vos tables

La commande `SHOW FIELDGROUPS` renvoie une table qui contient le nom, fieldgroupId et le propriétaire des tables.

Vous trouverez ci-dessous un exemple de sortie de cette commande :

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous comprenez mieux comment utiliser SQL pour créer un profil et un jeu de données activé pour l’upsert basé sur des jeux de données dérivés. Vous êtes maintenant prêt à utiliser ce jeu de données avec les workflows d’ingestion par lots pour mettre à jour vos données de profil. Pour en savoir plus sur l’ingestion de données dans Adobe Experience Platform, commencez par lire la [présentation de l’ingestion des données](../../../ingestion/home.md).
