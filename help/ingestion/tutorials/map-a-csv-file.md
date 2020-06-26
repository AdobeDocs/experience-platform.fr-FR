---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappage d’un fichier CSV à un schéma XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 7876e6d52815968802bd73bb5e340c99ea3387a8
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 2%

---


# Mappage d’un fichier CSV à un schéma XDM

Pour importer des données CSV dans [!DNL Adobe Experience Platform]un schéma, les données doivent être mises en correspondance avec un [!DNL Experience Data Model] (XDM). Ce didacticiel explique comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface [!DNL Platform] utilisateur.

En outre, l&#39;annexe du présent didacticiel fournit de plus amples informations sur l&#39;utilisation des fonctions [de](#mapping-functions)cartographie.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de [!DNL Platform]:

- [!DNL Experience Data Model (XDM System)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.
- [!DNL Batch ingestion](../batch-ingestion/overview.md): Méthode par laquelle [!DNL Platform] ingère les données des fichiers de données fournis par l’utilisateur.

Ce didacticiel nécessite également que vous ayez déjà créé un jeu de données dans lequel intégrer vos données CSV. Pour connaître les étapes de création d’un jeu de données dans l’interface utilisateur, consultez le didacticiel [sur l’assimilation des](./ingest-batch-data.md)données.

## Choisir une destination

Connectez-vous à [!DNL Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Workflows]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Workflows]* .

Dans l’écran **[!UICONTROL Workflows]** , sélectionnez **[!UICONTROL Mapper le fichier CSV au schéma]** XDM sous la section d’assimilation **[!UICONTROL des]** données, puis sélectionnez **[!UICONTROL Lancement.]**

![](../images/tutorials/map-a-csv-file/workflows.png)

Le flux de travail *[!UICONTROL Faire correspondre le fichier CSV au schéma]* XDM s’affiche, en commençant par l’étape *[!UICONTROL Destination]* . Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez soit utiliser un jeu de données existant, soit en créer un nouveau.

**Utiliser un jeu de données existant**

Pour importer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Utiliser un jeu de données]** existant. Vous pouvez récupérer un jeu de données existant à l&#39;aide de la fonction de recherche ou en faisant défiler la liste des jeux de données existants dans le panneau.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Pour intégrer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Créer un nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Sélectionnez un schéma en utilisant la fonction de recherche ou en faisant défiler la liste des schémas fournis. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Ajouter des données

L’étape *[!UICONTROL Ajouter les données]* s’affiche. Faites glisser votre fichier CSV dans l’espace prévu à cet effet ou sélectionnez **[!UICONTROL Choisir les fichiers]** pour entrer manuellement votre fichier CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

La section *[!UICONTROL Exemple de données]* s’affiche une fois le fichier téléchargé et affiche les dix premières lignes de données. Une fois que vous avez confirmé que les données ont été téléchargées comme prévu, sélectionnez **[!UICONTROL Suivant]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappage des champs CSV aux champs de schéma XDM

The *[!UICONTROL Mapping]* step appears. Les colonnes du fichier CSV sont répertoriées sous Champ ** source, et leurs champs de schéma XDM correspondants sont répertoriés sous Champ *[!UICONTROL de]* Cible. Les champs de cible non sélectionnés sont indiqués en rouge. Vous pouvez utiliser l’option de filtre de champs pour restreindre la liste des champs source disponibles.

Pour mapper une colonne CSV à un champ XDM, sélectionnez l’icône de schéma en regard du champ de cible correspondant à la colonne.

![](../images/tutorials/map-a-csv-file/mapping.png)

La fenêtre *[!UICONTROL Sélectionner un champ]* de schéma s&#39;affiche. Ici, vous pouvez parcourir la structure du schéma XDM et localiser le champ vers lequel vous souhaitez mapper la colonne CSV. Cliquez sur un champ XDM pour le sélectionner, puis sur **[!UICONTROL Sélectionner]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

L’écran *[!UICONTROL Mappage]* réapparaît, le champ XDM sélectionné s’affichant désormais sous Champ *[!UICONTROL de]* Cible.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Si vous ne souhaitez pas mapper une colonne CSV particulière, vous pouvez supprimer le mappage en cliquant sur l’icône **Supprimer** située en regard du champ de cible. Vous pouvez également supprimer tous les mappages en cliquant sur le bouton **** Effacer tous les mappages.

![](../images/tutorials/map-a-csv-file/remove-mapping.png)

Si vous souhaitez ajouter un nouveau mappage, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** en haut de la liste de champ ** source.

![](../images/tutorials/map-a-csv-file/add-mapping.png)

Lors du mappage de champs, vous pouvez également inclure des fonctions pour calculer les valeurs en fonction des champs de source d’entrée. Pour plus d’informations, voir la section relative aux fonctions [de](#mapping-functions) mappage dans l’annexe.

### Ajouter le champ calculé

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être attribuées à des attributs dans le schéma de cible et recevoir un nom et une description pour faciliter la référence.

Sélectionnez le bouton **[!UICONTROL Ajouter le champ]** calculé pour continuer.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Le panneau **[!UICONTROL Créer un champ]** calculé s’affiche. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez l’un des onglets à début pour ajouter des fonctions, des champs ou des opérateurs à l’éditeur d’expressions.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulation | Description |
| --------- | ----------- |
| Champs | L’onglet Champs liste les champs et les attributs disponibles dans le schéma source. |
| Fonctions | L&#39;onglet Fonctions liste les fonctions disponibles pour transformer les données. |
| Opérateurs   | L’onglet opérateurs liste les opérateurs disponibles pour transformer les données. |

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à l’aide de l’éditeur d’expressions situé au centre. Sélectionnez l’éditeur à début de la création d’une expression.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

L’écran de mappage s’affiche à nouveau avec votre nouveau champ source. Appliquez le champ de cible approprié et sélectionnez **[!UICONTROL Terminer]** pour terminer le mappage.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Surveiller votre flux de données

Une fois votre fichier CSV mappé et créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d’informations sur la surveillance des flux de données, voir le didacticiel sur la [surveillance des flux](../../ingestion/quality/monitor-data-flows.md)de données en flux continu.

## Étapes suivantes

En suivant ce didacticiel, vous avez mappé un fichier CSV aplati à un schéma XDM et l’avez assimilé à [!DNL Platform]un fichier. Ces données peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile]. Consultez la présentation pour [!DNL Real-time Customer Profile](../../profile/home.md) plus d’informations.

## Annexe

La section suivante fournit des informations supplémentaires sur le mappage des colonnes CSV aux champs XDM.

### Fonctions de mappage

Certaines fonctions de mappage peuvent être utilisées pour calculer et calculer des valeurs en fonction de ce qui est entré dans les champs source. Pour utiliser une fonction, tapez-la sous Champ ** source avec la syntaxe et les entrées appropriées.

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