---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;guide de dépannage;faq;dépannage;
solution: Experience Platform
title: Guide de dépannage de Query Service
topic-legacy: troubleshooting
description: Ce document contient des informations sur les codes d’erreur courants que vous rencontrez et les causes possibles.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 38d0c34e7af2466fa005c8adaf3bd9e1d9fd78e1
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 5%

---

# Guide de dépannage du [!DNL Query Service]

Ce document fournit des réponses aux questions fréquentes sur Query Service et fournit une liste des codes d’erreur courants lors de l’utilisation de Query Service. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

La liste suivante de réponses aux questions fréquentes est divisée en plusieurs catégories :

- [General (Général)](#general)
- [Exportation de données](#exporting-data)
- [Outils tiers](#third-party-tools)

## Questions générales sur Query Service {#general}

Cette section contient des informations sur les performances, les limites et les processus.

### Puis-je désactiver la fonction de saisie automatique dans l’éditeur de Query Service ?

+++Réponse Non. La désactivation de la fonction de saisie semi-automatique n’est actuellement pas prise en charge par l’éditeur.
+++

### Pourquoi l’éditeur de requêtes devient-il parfois lent lorsque je tape une requête ?

+++Réponse La fonction de saisie automatique est une cause potentielle. La fonction traite certaines commandes de métadonnées qui peuvent parfois ralentir l’éditeur lors de la modification des requêtes.
+++

### Puis-je utiliser Postman pour l’API Query Service ?

+++Répondez Oui, vous pouvez visualiser et interagir avec tous les services d’API Adobe à l’aide de Postman (une application tierce gratuite). Regardez la [Guide de configuration Postman](https://video.tv.adobe.com/v/28832) pour obtenir des instructions détaillées sur la configuration d’un projet dans Adobe Developer Console et l’acquisition de toutes les informations d’identification nécessaires pour l’utilisation avec Postman. Consultez la documentation officielle pour [conseils sur le démarrage, l’exécution et le partage de collections Postman](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Existe-t-il une limite au nombre maximum de lignes renvoyées par une requête via l’interface utilisateur ?

+++Réponse Oui, Query Service applique en interne une limite de 50 000 lignes, sauf si une limite explicite est spécifiée en externe. Reportez-vous aux conseils relatifs à [exécution de requête interactive](./best-practices/writing-queries.md#interactive-query-execution) pour plus d’informations.
+++

### Existe-t-il une limite de taille des données pour le résultat obtenu à partir d’une requête ?

+++Réponse Non. La taille des données n’est pas limitée, mais le délai d’expiration de la requête est limité à 10 minutes à partir d’une session interactive. Si la requête est exécutée en tant que CTAS par lot, un délai d’expiration de 10 minutes n’est pas applicable. Reportez-vous aux conseils relatifs à [exécution de requête interactive](./best-practices/writing-queries.md#interactive-query-execution) pour plus d’informations.
+++

### Comment contourner la limite du nombre de lignes de sortie d’une requête SELECT ?

+++Réponse Pour contourner la limite de ligne de sortie, appliquez &quot;LIMIT 0&quot; dans la requête. Par exemple :

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Comment empêcher mes requêtes d’expirer en 10 minutes ?

+++Réponse Une ou plusieurs des solutions suivantes sont recommandées en cas d’expiration des requêtes.

- [Convertir la requête en requête CTAS](./sql/syntax.md#create-table-as-select) et planifiez l’exécution. La planification d’une exécution peut être effectuée : [via l’interface utilisateur](./ui/user-guide.md#scheduled-queries) ou le [API](./api/scheduled-queries.md#create).
- Exécutez la requête sur un bloc de données plus petit en appliquant des [conditions de filtrage](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Exécutez la commande EXPLAIN](./sql/syntax.md#explain) pour en savoir plus.
- Examinez les statistiques des données du jeu de données.
- Convertir la requête en formulaire simplifié et la relancer à l’aide de [instructions préparées](./sql/prepared-statements.md).
+++

### Y a-t-il un problème ou un impact sur les performances de Query Service si plusieurs requêtes s’exécutent simultanément ?

+++Réponse Non. Query Service dispose d’une fonctionnalité de mise à l’échelle automatique qui garantit que les requêtes simultanées n’ont aucun impact perceptible sur les performances du service.
+++

### Comment puis-je trouver un nom de colonne à partir d’un jeu de données hiérarchique ?

+++Réponse Les étapes suivantes décrivent comment afficher une vue tabulaire d’un jeu de données via l’interface utilisateur, y compris tous les champs et colonnes imbriqués dans un formulaire aplati.

- Après vous être connecté à Experience Platform, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche de l’interface utilisateur à laquelle accéder [!UICONTROL Jeux de données] tableau de bord.
- Jeux de données [!UICONTROL Parcourir] s’ouvre. Vous pouvez utiliser la barre de recherche pour affiner les options disponibles. Sélectionnez un jeu de données dans la liste affichée.

![Jeu de données surligné dans l’interface utilisateur de Platform.](./images/troubleshooting/dataset-selection.png)

- Le [!UICONTROL Activité Jeux de données] s’affiche. Sélectionner [!UICONTROL Prévisualisation d’un jeu de données] pour ouvrir une boîte de dialogue du schéma XDM et une vue tabulaire des données aplaties du jeu de données sélectionné. Vous trouverez plus de détails dans la section [prévisualisation de la documentation d’un jeu de données](../catalog/datasets/user-guide.md#preview-a-dataset)

![Schéma XDM et vue tabulaire des données aplaties.](./images/troubleshooting/dataset-preview.png)

- Sélectionnez un champ du schéma pour afficher son contenu dans une colonne aplatie. Le nom de la colonne s’affiche au-dessus de son contenu sur le côté droit de la page. Vous devez copier ce nom pour interroger ce jeu de données.

![Nom de colonne d’un jeu de données imbriqué mis en surbrillance dans l’interface utilisateur.](./images/troubleshooting/column-name.png)

Consultez la documentation pour obtenir des conseils complets sur [Comment travailler avec des structures de données imbriquées](./best-practices/nested-data-structures.md) à l’aide de Query Editor ou d’un client tiers.
+++

### Comment accélérer une requête sur un jeu de données contenant des tableaux ?

+++Réponse Pour améliorer les performances des requêtes sur les jeux de données contenant des tableaux, vous devez [faire exploser le tableau](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [Requête CTAS](./sql/syntax.md#create-table-as-select) au moment de l’exécution, puis explorez-le pour en savoir plus sur les opportunités d’amélioration de son temps de traitement.
+++

### Pourquoi ma requête CTAS est-elle toujours en cours de traitement après de nombreuses heures pour un petit nombre de lignes seulement ?

+++Réponse Si la requête a pris beaucoup de temps sur un très petit jeu de données, contactez le service clientèle.

Il peut y avoir plusieurs raisons pour qu’une requête soit bloquée pendant le traitement. Pour déterminer la cause exacte, une analyse approfondie au cas par cas est nécessaire. [Contacter l’assistance clientèle d’Adobe](#customer-support) à ce processus.
+++

### Comment contacter le service clientèle d’Adobe ? {#customer-support}

+++Réponse
[Liste complète des numéros de téléphone de l’assistance clientèle d’Adobe](https://helpx.adobe.com/ca/contact/phone.html) est disponible sur la page d’aide d’Adobe. Vous pouvez également trouver de l’aide en ligne en procédant comme suit :

- Accédez à [https://www.adobe.com/](https://www.adobe.com/) dans votre navigateur web.
- Sur le côté droit de la barre de navigation supérieure, sélectionnez **[!UICONTROL Se connecter]**.

![Le site web d’Adobe avec connexion est mis en surbrillance.](./images/troubleshooting/adobe-sign-in.png)

- Utilisez votre Adobe ID et votre mot de passe enregistrés avec votre licence d’Adobe.
- Sélectionner **[!UICONTROL Aide et assistance]** dans la barre de navigation supérieure.

![Menu déroulant de la barre de navigation supérieure avec l’aide et la prise en charge surlignée.](./images/troubleshooting/help-and-support.png)

Une bannière déroulante s’affiche avec une [!UICONTROL Aide et support] . Sélectionner **[!UICONTROL Contactez-nous]** pour ouvrir l’assistant virtuel de l’assistance clientèle Adobe ou sélectionnez **[!UICONTROL Support aux entreprises]** pour obtenir une aide dédiée aux grandes entreprises.
+++

### Comment mettre en oeuvre une série de tâches séquentielles sans exécuter les tâches suivantes si la tâche précédente ne se termine pas correctement ?

+++Réponse La fonction de bloc anonyme vous permet de chaîner une ou plusieurs instructions SQL exécutées en séquence. Ils permettent également de gérer les exceptions.

Voir [documentation bloquée anonyme](./best-practices/anonymous-block.md) pour plus d’informations.
+++

### Comment mettre en oeuvre l’attribution personnalisée dans Query Service ?

+++Réponse Il existe deux façons de mettre en oeuvre l’attribution personnalisée :

1. Utilisez une combinaison de [Fonctions définies par l’Adobe](./sql/adobe-defined-functions.md) pour déterminer si les besoins du cas d’utilisation sont satisfaits.
1. Si la suggestion précédente ne répond pas à votre cas d’utilisation, vous devez utiliser une combinaison de [fonctions de fenêtre](./sql/adobe-defined-functions.md#window-functions). Les fonctions de fenêtre examinent tous les événements d’une séquence. Elles vous permettent également de consulter les données historiques et peuvent être utilisées dans n’importe quelle combinaison.
+++

### Puis-je modéliser mes requêtes afin de pouvoir les réutiliser facilement ?

+++Répondez Oui, vous pouvez modéliser des requêtes à l’aide d’instructions préparées. Les instructions préparées peuvent optimiser les performances et éviter de réanalyser rapidement une requête. Voir [documentation sur les instructions préparées](./sql/prepared-statements.md) pour plus d’informations.
+++

### Comment récupérer les logs d’erreur d’une requête ? {#error-logs}

+++Réponse Pour récupérer les logs d’erreur d’une requête spécifique, vous devez d’abord utiliser l’API Query Service pour récupérer les détails du log de requête. La réponse HTTP contient les ID de requête requis pour rechercher une erreur de requête.

Utilisez la commande GET pour récupérer plusieurs requêtes. Vous trouverez des informations sur la manière d’effectuer un appel à l’API dans la section [exemple de documentation sur les appels API](./api/queries.md#sample-api-calls).

À partir de la réponse, identifiez la requête sur laquelle vous souhaitez enquêter et effectuez une autre requête de GET à l’aide de `id` . Vous trouverez des instructions complètes dans la section [récupération d’une requête par documentation d’identification](./api/queries.md#retrieve-a-query-by-id).

Une réponse réussie renvoie un état HTTP 200 et contient le paramètre `errors` tableau. La réponse a été raccourcie pour plus de concision.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

Le [Documentation de référence de l’API Query Service](https://www.adobe.io/experience-platform-apis/references/query-service/) fournit plus d’informations sur tous les points de terminaison disponibles.
+++

### Que signifie &quot;Erreur de validation du schéma&quot; ?

+++Réponse Le message &quot;Erreur lors de la validation du schéma&quot; signifie que le système ne peut pas localiser un champ dans le schéma. Vous devez lire le document des bonnes pratiques pour [organisation des ressources de données dans Query Service](./best-practices/organize-data-assets.md) suivie de la fonction [Créer un tableau comme sélection de documentation](./sql/syntax.md#create-table-as-select).

L’exemple suivant illustre l’utilisation d’une syntaxe CTAS et d’un type de données struct :

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### Comment traiter rapidement les nouvelles données qui entrent dans le système tous les jours ?

+++Répondez Au [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) peut être utilisée pour lire de manière incrémentielle les données d’une table en fonction d’un ID d’instantané. Idéal pour l’utilisation avec la variable [charge incrémentale](./best-practices/incremental-load.md) modèle qui traite uniquement les informations du jeu de données qui a été créé ou modifié depuis la dernière exécution du chargement. Par conséquent, il augmente l’efficacité du traitement et peut être utilisé avec le traitement par flux et par lot des données.
+++

### Pourquoi y a-t-il une différence entre les nombres affichés dans l’interface utilisateur de Profile et les nombres calculés à partir du jeu de données d’exportation de profil ?

+++Réponse Les nombres affichés dans le tableau de bord du profil sont précis à partir du dernier instantané. Les chiffres générés dans la table d&#39;export de profil dépendent entièrement de la requête d&#39;export. Par conséquent, l’interrogation du nombre de profils admissibles pour un segment particulier est une cause courante de cette incohérence.

>[!NOTE]
>
>La requête inclut des données historiques, tandis que l’interface utilisateur affiche uniquement les données de profil actuelles.

+++

### Pourquoi ma requête a-t-elle renvoyé un sous-ensemble vide et que dois-je faire ?

+++Réponse La cause la plus probable est que la portée de votre requête est trop limitée. Vous devez supprimer systématiquement une section de la variable `WHERE` jusqu’à ce que vous commenciez à voir certaines données.

Vous pouvez également confirmer que votre jeu de données contient des données à l’aide d’une petite requête telle que :

```sql
SELECT count(1) FROM myTableName
```

+++

### Puis-je échantillonner mes données ?

+++Réponse Cette fonctionnalité est actuellement en cours de réalisation. Des informations détaillées seront disponibles dans [notes de mise à jour](../release-notes/latest/latest.md) et par le biais des boîtes de dialogue de l’interface utilisateur de Platform une fois que la fonctionnalité est prête à être publiée.
+++

### Quelles fonctions d’assistance sont prises en charge par Query Service ?

+++Réponse Query Service fournit plusieurs fonctions d’assistance SQL intégrées pour étendre les fonctionnalités SQL. Consultez le document pour obtenir la liste complète des [Fonctions SQL prises en charge par Query Service](./sql/spark-sql-functions.md).
+++

### Que dois-je faire si ma requête planifiée échoue ?

+++Répondez d’abord, consultez les journaux pour connaître les détails de l’erreur. La section FAQ sur [recherche d’erreurs dans les logs](#error-logs) fournit des informations supplémentaires sur la manière de procéder.

Vous devez également consulter la documentation pour obtenir des conseils sur la manière d’effectuer [requêtes planifiées dans l’interface utilisateur](./ui/user-guide.md#scheduled-queries) et [l’API](./api/scheduled-queries.md).
+++

### Que signifie l’erreur &quot;Limite de session atteinte&quot; ?

+++La réponse &quot;Limite de session atteinte&quot; signifie que le nombre maximal de sessions Query Service autorisées pour votre organisation a été atteint. Connectez-vous à l’administrateur Adobe Experience Platform de votre entreprise.
+++

### Comment le journal de requête gère-t-il les requêtes relatives à un jeu de données supprimé ?

+++Réponse Query Service ne supprime jamais l’historique des requêtes. Cela signifie que toute requête référençant un jeu de données supprimé renvoie &quot;Aucun jeu de données valide&quot;.
+++

### Comment puis-je obtenir uniquement les métadonnées d’une requête ?

+++Réponse Vous pouvez exécuter une requête qui renvoie zéro ligne pour obtenir uniquement les métadonnées en réponse. Cet exemple de requête renvoie uniquement les métadonnées de la table spécifiée.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Comment puis-je itérer rapidement sur une requête CTAS (Create Table As Select) sans la matérialiser ?

+++Réponse Vous pouvez créer des tableaux temporaires pour itérer rapidement une requête et l’expérimenter avant de la matérialiser pour l’utiliser. Vous pouvez également utiliser des tableaux temporaires pour vérifier si une requête est fonctionnelle.

Vous pouvez par exemple créer un tableau temporaire :

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Vous pouvez ensuite utiliser le tableau temporaire comme suit :

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### Comment modifier le fuseau horaire en horodatage UTC ?

+++Réponse Adobe Experience Platform conserve les données au format d’horodatage UTC (temps universel coordonné). Exemple de format UTC : `2021-12-22T19:52:05Z`

Query Service prend en charge les fonctions SQL intégrées pour convertir un horodatage donné au format UTC et à partir de ce format. Les deux `to_utc_timestamp()` et le `from_utc_timestamp()` Les méthodes prennent deux paramètres : horodatage et fuseau horaire.

| Paramètre | Description |
|-----------|---------------|
| Horodatage | L’horodatage peut être écrit au format UTC ou simple. `{year-month-day}` format. Si aucune heure n’est fournie, la valeur par défaut est minuit le matin du jour donné. |
| Fuseau horaire | Le fuseau horaire est écrit dans une `{continent/city})` format. Il doit s’agir de l’un des codes de fuseau horaire reconnus, comme indiqué dans la variable [base de données TZ du domaine public](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Convertir en horodatage UTC

Le `to_utc_timestamp()` interprète les paramètres donnés et les convertit **à l’horodatage de votre fuseau horaire local.** au format UTC. Par exemple, le fuseau horaire à Séoul, en Corée du Sud, est UTC/GMT +9 heures. En fournissant un horodatage date seule, la méthode utilise une valeur par défaut de minuit le matin. L’horodatage et le fuseau horaire sont convertis au format UTC de l’heure de cette région en horodatage UTC de votre région locale.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La requête renvoie un horodatage à l’heure locale de l’utilisateur. Dans ce cas, la veille à 15h00 comme à Séoul, il y a neuf heures d&#39;avance.

```
2021-08-30 15:00:00
```

Autre exemple : si l’horodatage donné a été `2021-07-14 12:40:00.0` pour le `Asia/Seoul` fuseau horaire, l’horodatage UTC renvoyé serait `2021-07-14 03:40:00.0`

La sortie de console fournie dans l’interface utilisateur de Query Service est plus lisible :

```
8/30/2021, 3:00 PM
```

#### Convertir à partir de l’horodatage UTC

Le `from_utc_timestamp()` interprète les paramètres donnés. **à partir de l’horodatage de votre fuseau horaire local** et fournit l’horodatage équivalent de la région souhaitée au format UTC. Dans l’exemple ci-dessous, l’heure est 14 h 40 dans le fuseau horaire local de l’utilisateur. Le fuseau horaire de Séoul passé en tant que variable est neuf heures avant le fuseau horaire local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La requête renvoie un horodatage au format UTC pour le fuseau horaire transmis en tant que paramètre. Le résultat est neuf heures avant le fuseau horaire qui a exécuté la requête.

```
8/31/2021, 11:40 PM
```

### Comment dois-je filtrer mes données de série temporelle ?

+++Réponse Lors de l’interrogation des données de série temporelle, vous devez utiliser le filtre d’horodatage chaque fois que possible pour une analyse plus précise.

>[!NOTE]
>
> Chaîne de date **must** être au format `yyyy-mm-ddTHH24:MM:SS`.

Vous trouverez ci-dessous un exemple d’utilisation du filtre d’horodatage :

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### Comment utiliser correctement la variable `CAST` pour convertir mes horodatages dans les requêtes SQL ?

+++Réponse lors de l’utilisation de la variable `CAST` pour convertir un horodatage, vous devez inclure la date **et** temps.

Par exemple, l’absence du composant temporel, comme illustré ci-dessous, entraînera une erreur :

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

L’utilisation correcte de la variable `CAST` est illustré ci-dessous :

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Dois-je utiliser des caractères génériques, tels que * pour obtenir toutes les lignes de mes jeux de données ?

+++Réponse Vous ne pouvez pas utiliser de caractères génériques pour obtenir toutes les données de vos lignes, car Query Service doit être traité comme un **columnar-store** plutôt qu’un système de magasin traditionnel basé sur les lignes.
+++

### Dois-je utiliser `NOT IN` dans ma requête SQL ?

+++Répondez Au `NOT IN` est souvent utilisé pour récupérer les lignes qui ne figurent pas dans une autre table ou instruction SQL. Cet opérateur peut ralentir les performances et renvoyer des résultats inattendus si les colonnes comparées acceptent `NOT NULL`, ou vous avez un grand nombre d’enregistrements.

Au lieu d’utiliser `NOT IN`, vous pouvez utiliser `NOT EXISTS` ou `LEFT OUTER JOIN`.

Par exemple, si les tables suivantes sont créées :

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Si vous utilisez la variable `NOT EXISTS` , vous pouvez répliquer à l’aide de l’opérateur `NOT IN` en utilisant la requête suivante :

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Si vous utilisez la méthode `LEFT OUTER JOIN` , vous pouvez répliquer à l’aide de l’opérateur `NOT IN` en utilisant la requête suivante :

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

## Erreurs de l’API REST

| Code d’état HTTP | Description | Causes possibles |
|------------------|-----------------------|----------------------------|
| 400 | Mauvaise requête | Requête malformée ou illégale |
| 401 | Échec de l’authentification | Jeton d’authentification non valide |
| 500 | Erreur interne du serveur | Échec du système interne |

## Erreurs de l’API PostgreSQL

| Code erreur | État de la connexion | Description | Cause possible |
|------------|---------------------------|-------------|----------------|
| **08P01** | S/O | Type de message non pris en charge | Type de message non pris en charge |
| **28P01** | Démarrage - authentification | Mot de passe non valide | Jeton d’authentification non valide |
| **28000** | Démarrage - authentification | Type d’autorisation non valide | Type d’autorisation non valide. Doit être `AuthenticationCleartextPassword`. |
| **42P12** | Démarrage - authentification | Aucune table trouvée | Aucune table n’a été trouvée pour utilisation |
| **42601** | Requête | Erreur de syntaxe | Erreur de syntaxe ou de commande non valide |
| **42P01** | Requête | Table introuvable | La table spécifiée dans la requête est introuvable |
| **42P07** | Requête | La table existe | Il existe déjà une table portant le même nom (CREATE TABLE) |
| **53400** | Requête | LIMIT dépasse la valeur maximale | L’utilisateur a spécifié une clause LIMIT supérieure à 100 000 |
| **53400** | Requête | Délai d’expiration de la déclaration | La déclaration soumise en direct a duré plus de 10 minutes au maximum |
| **58000** | Requête | Erreur système | Échec du système interne |
| **0A000** | Requête/Commande | Non pris en charge | La fonctionnalité de la requête/commande n’est pas prise en charge |
| **42501** | Requête DROP TABLE | Table de dépôt non créée par Query Service | La table en cours de suppression n’a pas été créée par Query Service à l’aide de l’événement `CREATE TABLE` statement |
| **42501** | Requête DROP TABLE | Tableau non créé par l’utilisateur authentifié | La table en cours de suppression n’a pas été créée par l’utilisateur actuellement connecté. |
| **42P01** | Requête DROP TABLE | Table introuvable | La table spécifiée dans la requête est introuvable. |
| **42P12** | Requête DROP TABLE | Aucune table trouvée pour `dbName`: veuillez consulter la section `dbName` | Aucune table n’a été trouvée dans la base de données actuelle |

## Exportation de données {#exporting-data}

Cette section fournit des informations sur l&#39;export des données et des limites.


### Existe-t-il un moyen d’extraire des données de Query Service après le traitement des requêtes et d’enregistrer les résultats dans un fichier CSV ?

+++Répondez Oui. Les données peuvent être extraites de Query Service et il existe également la possibilité de stocker les résultats au format CSV via une commande SQL.

Il existe deux manières d’enregistrer les résultats d’une requête lors de l’utilisation d’un client PSQL. Vous pouvez utiliser la variable `COPY TO` ou créez une instruction au format suivant :

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Conseils sur l’utilisation de la variable `COPY TO` command](./sql/syntax.md#copy) se trouve dans la documentation de référence sur la syntaxe SQL.
+++

### Puis-je extraire le contenu du jeu de données final qui a été ingéré par le biais de requêtes CTAS (en supposant qu’il s’agisse de grandes quantités de données telles que Terabytes) ?

+++Réponse Non. Actuellement, aucune fonctionnalité n’est disponible pour l’extraction des données ingérées.
+++

## Outils tiers {#third-party-tools}

Cette section contient des informations sur l’utilisation d’outils tiers tels que PSQL et Power BI.

### Puis-je connecter Query Service à un outil tiers ?

+++Réponse Oui, vous pouvez connecter plusieurs clients de bureau tiers à Query Service. Consultez la documentation pour [détails complets sur les clients disponibles et comment les connecter à Query Service](./clients/overview.md).
+++

### Existe-t-il un moyen de connecter Query Service une fois pour une utilisation continue avec un outil tiers ?

+++Réponse Oui, les clients de bureau tiers peuvent être connectés à Query Service par le biais d’une configuration unique d’informations d’identification qui n’expirent pas. Les informations d’identification non arrivant à expiration peuvent être générées par un utilisateur autorisé et les recevront dans un fichier JSON téléchargé sur son ordinateur local. Complet [conseils sur la création et le téléchargement d’informations d’identification non expirantes](./ui/credentials.md#non-expiring-credentials) se trouve dans la documentation .
+++

### Quel type d’éditeurs SQL tiers puis-je me connecter à Query Service Editor ?

+++Répondre Tout éditeur SQL tiers qui est PSQL ou [!DNL Postgres] Il est possible de se connecter à l’éditeur de Query Service en conformité avec le client. Consultez la documentation pour [connexion des clients à Query Service](./clients/overview.md) pour obtenir une liste des instructions disponibles.
+++

### Puis-je connecter l’outil de Power BI à Query Service ?

+++Répondez Oui, vous pouvez vous connecter à Query Service. Consultez la documentation pour [instructions sur la connexion de l’appli de bureau Power BI à Query Service](./clients/power-bi.md).
+++

### Pourquoi le chargement des tableaux de bord est-il long lorsqu’ils sont connectés à Query Service ?

+++Réponse Lorsque le système est connecté à Query Service, il est connecté à un moteur de traitement interactif ou par lots. Cela peut entraîner des temps de chargement plus longs pour refléter les données traitées.

Si vous souhaitez améliorer les temps de réponse de vos tableaux de bord, vous devez mettre en oeuvre un serveur Business Intelligence (BI) en tant que couche de mise en cache entre Query Service et les outils de BI. En règle générale, la plupart des outils de BI disposent d’une offre supplémentaire pour un serveur.

L’ajout de la couche de serveur de cache a pour but de mettre en cache les données de Query Service et d’en utiliser de même pour les tableaux de bord afin d’accélérer la réponse. Cela est possible, car les résultats des requêtes exécutées seraient mis en cache dans le serveur BI chaque jour. Le serveur de mise en cache diffuse ensuite ces résultats à tout utilisateur disposant de la même requête afin de réduire la latence. Reportez-vous à la documentation de l’utilitaire ou de l’outil tiers que vous utilisez pour clarifier cette configuration.
+++

### Est-il possible d’accéder à Query Service à l’aide de l’outil de connexion pgAdmin ?

+++Réponse Non, la connectivité pgAdmin n’est pas prise en charge. A [liste des clients tiers disponibles et instructions sur la manière de les connecter à Query Service](./clients/overview.md) se trouve dans la documentation .
+++
