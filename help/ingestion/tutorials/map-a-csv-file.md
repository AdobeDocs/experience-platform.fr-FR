---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappage d’un fichier CSV à un schéma XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 2%

---


# Mappage d’un fichier CSV à un schéma XDM

Pour importer des données CSV dans Adobe Experience Platform, les données doivent être mises en correspondance avec un schéma de modèle de données d’expérience (XDM). Ce didacticiel explique comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface utilisateur de la plateforme d’expérience.

En outre, l&#39;annexe du présent didacticiel fournit de plus amples informations sur l&#39;utilisation des fonctions [de](#mapping-functions)cartographie.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Modèle de données d’expérience (système XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
- [Importation](../batch-ingestion/overview.md)par lot : Méthode par laquelle la plate-forme ingère des données à partir de fichiers de données fournis par l’utilisateur.

Ce didacticiel nécessite également que vous ayez déjà créé un jeu de données dans lequel intégrer vos données CSV. Pour connaître les étapes de création d’un jeu de données dans l’interface utilisateur, consultez le didacticiel [sur l’assimilation des](./ingest-batch-data.md)données.

## Données Ajouter

Dans l’interface utilisateur de la plateforme d’expérience, cliquez sur **Workflows** dans le volet de navigation de gauche, puis cliquez sur **Mapper le fichier CSV au schéma** XDM. Dans le rail de droite qui s’affiche, cliquez sur **Lancer**.

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

Le flux de travail _Faire correspondre le fichier CSV au schéma_ XDM s’affiche, en commençant par l’étape des données __ Ajouter.

![](../images/tutorials/map-a-csv-file/add-data.png)

Faites glisser votre fichier CSV dans l’espace prévu à cet effet ou cliquez sur **Parcourir** pour sélectionner directement un fichier. Une section _Exemple de données_ s’affiche une fois le fichier téléchargé et affiche les dix premières lignes de données. Une fois que vous avez confirmé que les données ont été téléchargées comme prévu, cliquez sur **Suivant**.

![](../images/tutorials/map-a-csv-file/csv-added.png)

## Choisir une destination

The _Destination_ step appears. Dans la liste fournie, sélectionnez le jeu de données dans lequel les données CSV seront assimilées, puis cliquez sur **Suivant**.

![](../images/tutorials/map-a-csv-file/select-destination.png)

## Mappage des champs CSV aux champs de schéma XDM

The _Mapping_ step appears. Les colonnes du fichier CSV sont répertoriées sous Champ __ source, et leurs champs de schéma XDM correspondants sont répertoriés sous Champ _de_ Cible. Les champs de cible non sélectionnés sont indiqués en rouge.

Pour mapper une colonne CSV à un champ XDM, cliquez sur l’icône de schéma en regard du champ de cible correspondant à la colonne.

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

La fenêtre _Sélectionner un champ_ de schéma s&#39;affiche. Ici, vous pouvez parcourir la structure du schéma XDM et localiser le champ vers lequel vous souhaitez mapper la colonne CSV. Cliquez sur un champ XDM pour le sélectionner, puis sur **Sélectionner**.

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

L’écran _Mappage_ réapparaît, le champ XDM sélectionné s’affichant désormais sous Champ _de_ Cible.

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

Si vous ne souhaitez pas mapper une colonne CSV particulière, vous pouvez supprimer le mappage en cliquant sur l’icône **Supprimer** située en regard du champ de cible. Si vous souhaitez ajouter un nouveau mappage, cliquez sur **Ajouter nouveau mappage** au bas de la liste.

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

Lors du mappage de champs, vous pouvez également inclure des fonctions pour calculer les valeurs en fonction des champs de source d’entrée. Pour plus d’informations, voir la section relative aux fonctions [de](#mapping-functions) mappage dans l’annexe.

Répétez les étapes ci-dessus pour continuer à mapper les colonnes CSV aux champs XDM. Une fois que vous avez terminé, cliquez sur **Suivant**.

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## Données d’entrée

L’étape _d’envoi_ s’affiche, vous permettant de vérifier les détails de votre fichier source et de votre jeu de données de cible. Cliquez sur **Inviter** au début d’assimilation des données CSV. Selon la taille du fichier CSV, ce processus peut prendre plusieurs minutes. L’écran se met à jour une fois l’assimilation terminée, ce qui indique la réussite ou l’échec. Click **Finish** to complete the workflow.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez mappé avec succès un fichier CSV aplati à un schéma XDM et l’avez ingéré dans Platform. Ces données peuvent désormais être utilisées par les services de plateforme en aval tels que le Profil client en temps réel. Pour plus d’informations, consultez la présentation [du Profil client en temps](../../profile/home.md) réel.

## Annexe

La section suivante fournit des informations supplémentaires sur le mappage des colonnes CSV aux champs XDM.

### Fonctions de mappage

Certaines fonctions de mappage peuvent être utilisées pour calculer et calculer des valeurs en fonction de ce qui est entré dans les champs source. Pour utiliser une fonction, tapez-la sous Champ __ source avec la syntaxe et les entrées appropriées.

Par exemple, pour concaténer des champs CSV de **ville** et de **pays** et les affecter au champ XDM de **ville** , définissez le champ source comme `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Le tableau ci-dessous liste toutes les fonctions de mappage prises en charge, y compris les exemples d’expressions et leurs résultats.

| Fonction | Description | Exemple d’expression | Exemple de sortie |
| -------- | ----------- | ----------------- | ------------- |
| concat | Concatène les chaînes données. | concat(&quot;Bonjour, &quot;, &quot;là&quot;, &quot;!&quot;) | `"Hi, there!"` |
| exploser | Scinde la chaîne en fonction d’un regex et renvoie un tableau de parties. | explode(&quot;Salut, voilà !&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| order | Renvoie l’emplacement/l’index d’une sous-chaîne. | (&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| remplacer | Remplace la chaîne de recherche si elle est présente dans la chaîne d’origine. | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Test de remplacement de chaîne&quot; |
| substr | Renvoie une sous-chaîne d’une longueur donnée. | translate(&quot;Ceci est un test de sous-chaîne&quot;, 7, 8) | &quot;a subst&quot; |
| lower /<br>lcase | Convertit une chaîne en minuscules. | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Convertit une chaîne en majuscules. | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;BONJOUR&quot; |
| scinder | Scinde une chaîne d’entrée sur un séparateur. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Rejoint une liste d’objets à l’aide du séparateur. | `join(" ", ["Hello", "world"]`) | &quot;Bonjour le monde&quot; |
| coalesce | Renvoie le premier objet non nul dans une liste donnée. | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| décoder | Compte tenu d&#39;une clé et d&#39;une liste de paires clé-valeur aplaties en tant que tableau, la fonction renvoie la valeur si clé est trouvée ou renvoie une valeur par défaut si elle est présente dans le tableau. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | Evalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | Renvoie le minimum d&#39;arguments donnés. Utilise l’ordre naturel. | min(3, 1, 4) | 1 |
| max | Renvoie le maximum des arguments donnés. Utilise l’ordre naturel. | max(3, 1, 4) | 4 |
| first | Récupère le premier argument donné. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Récupère le dernier argument donné. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | Génère un ID pseudo-aléatoire. | uuid()<br>guid() | {UNIQUE_ID} |
| now | Récupère l’heure actuelle. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Récupère l&#39;heure Unix actuelle. | timestamp() | 1571850624571 |
| format | Formate la date d’entrée selon un format spécifié. | format({DATE}, &quot;aaaa-MM-jj HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Convertit un horodatage en chaîne de date selon un format spécifié. | dformat(1571829875, &quot;jj-MMM-aaaa hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | date(&quot;23-Oct-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Récupère les parties de la date. Les valeurs de composant suivantes sont prises en charge : <br><br>&quot;année&quot;<br>&quot;aaaa&quot;<br>&quot;yy&quot;<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;&quot;m&quot;&quot;dayof year&quot;&quot;le&quot;jour&quot;y&quot;&quot;jour&quot;de&quot;&quot;de&quot;&quot;semaine&quot;&quot;w&quot;&quot;jour de la semaine&quot;&quot;w&quot;jour de la semaine&quot;&quot;w&quot;w&quot;h&quot;h&quot;h&quot;wj&quot;wj&quot;h&quot;h&quot;h&quot;&quot;h&quot;h&quot;semaine&quot;h&quot;h&quot;semaine&quot;&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot; h&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minute&quot;mi&quot;&quot;n&quot;second&quot;&quot;s&quot;&quot;milliseconde&quot;&quot;ms&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br> | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Remplace un composant à une date donnée. Les composants suivants sont acceptés : <br><br>&quot;année&quot;<br>&quot;aaaa&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>day&quot;<br>&quot;dd&quot;&quot;&quot;hour&quot;&quot;hh&quot;&quot;minute&quot;mi&quot;&quot;n&quot;&quot;second&quot;&quot;s&quot;&quot;&quot;<br><br><br><br><br><br><br><br><br><br><br><br> | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Crée une date à partir de pièces. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Renvoie l’horodatage actuel. | current_timestamp() | 1571850624571 |
| current_date | Renvoie la date actuelle sans composant d’heure. | current_date() | &quot;18-nov.-2019&quot; |