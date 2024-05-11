---
title: Création d’un filtre de date
description: Découvrez comment filtrer vos insights personnalisés par date.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Création d’un filtre de date {#create-date-filter}

Pour filtrer vos informations par date, vous devez ajouter des paramètres à vos requêtes SQL qui peuvent accepter des contraintes de date. Cela s’inscrit dans le cadre du workflow de création d’informations sur le mode professionnel des requêtes. Voir [documentation sur le mode query pro](#query-pro-mode) pour savoir comment saisir des informations SQL.

Les paramètres de requête vous permettent d’utiliser des données dynamiques qui agissent comme espaces réservés aux valeurs que vous ajoutez au moment de l’exécution. Ces valeurs d’espace réservé peuvent être mises à jour via l’interface utilisateur et permettent aux utilisateurs moins techniques de mettre à jour les informations en fonction des périodes.

Si vous ne connaissez pas les paramètres de requête, reportez-vous à la documentation de [conseils sur la mise en oeuvre de requêtes paramétrées](../../../../query-service/ui/parameterized-queries.md).

## Appliquer un filtre de date à votre tableau de bord {#apply-date-filter}

Pour appliquer un filtre de date, sélectionnez **[!UICONTROL Ajouter un filtre]**, puis **[!UICONTROL Filtre de date]** dans le menu déroulant de la vue de votre tableau de bord.

![Un tableau de bord personnalisé avec le filtre Ajouter et son menu déroulant est mis en surbrillance.](../../../images/customizable-insights/add-filter.png)

## Modifier votre code SQL pour inclure les paramètres de requête de date {#include-date-parameters}

Ensuite, assurez-vous que votre SQL inclut des paramètres de requête pour permettre une période. Si vous n’avez pas encore incorporé de paramètres de requête dans votre SQL, modifiez vos insights pour inclure ces paramètres. Consultez la documentation pour obtenir des instructions sur la manière de [modification d’un aperçu](../query-pro-mode.md#edit).

>[!TIP]
>
>Il est recommandé d’ajouter `$START_DATE` et `$END_DATE` des paramètres de votre instruction SQL dans chacun des graphiques pour lesquels vous souhaitez activer des filtres de dates.

>[!NOTE]
>
>Les filtres de date ne prennent pas en charge les contraintes de temps. Le filtre s’applique uniquement aux périodes. En d’autres termes, si vous disposez de plusieurs rapports sur une période de 24 heures, vous ne pouvez pas faire la distinction entre différentes heures au cours d’une même journée. C’est pourquoi il est recommandé de définir le composant de temps comme une date.

Si le ou les tableaux de données que vous analysez comportent un composant d’heure, vous pouvez regrouper vos données par date, puis appliquer ces filtres de date.

L’exemple d’instruction SQL ci-dessous montre comment incorporer des `$START_DATE` et `$END_DATE` paramètres et utilisation `cast` pour définir le composant d’heure comme une date.

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

La capture d’écran ci-dessous met en évidence les contraintes de date intégrées à l’instruction SQL et les paires clé-valeur du paramètre de requête.

>[!NOTE]
>
>Lors de la composition de votre instruction en mode query pro, vous devez fournir des exemples de valeurs pour chaque paramètre afin d’exécuter l’instruction SQL et de créer le graphique. Les exemples de valeurs que vous fournissez lors de la composition de votre instruction sont remplacés par les valeurs réelles que vous sélectionnez pour le filtre de date (ou global) au moment de l’exécution.

![La variable [!UICONTROL Saisir SQL] avec les paramètres de date en surbrillance dans le SQL.](../../../images/customizable-insights/sql-date-parameters.png)

## Activation des paramètres de date dans chaque insight {#enable-date-parameters}

Une fois que vous avez intégré les paramètres appropriés au SQL de vos insights, la variable `Start_date` et `End_date` sont désormais disponibles en tant que bascules dans le compositeur de widgets. Voir [section population du widget de mode professionnel des requêtes](#populate-widget) pour plus d’informations sur la modification d’un insight.

Dans le compositeur de widgets, sélectionnez les bascules pour activer la fonction `Start_date` et `End_date` paramètres.

![Le compositeur de widget avec les bascules Start_date et End_date mis en surbrillance.](../../../images/customizable-insights/widget-composer-date-filter-toggles.png)

Sélectionnez ensuite les paramètres de requête appropriés dans les menus déroulants.

![Le compositeur de widgets avec le menu déroulant Start_date en surbrillance.](../../../images/customizable-insights/widget-composer-date-filter-dropdown.png)

Enfin, sélectionnez **[!UICONTROL Enregistrer et fermer]** pour revenir à votre tableau de bord. Les filtres de date sont désormais activés pour toutes les informations qui comportent des paramètres de date de début et de fin.

## Utiliser le filtre de date

Pour utiliser un filtre de date personnalisé, sélectionnez l&#39;icône du calendrier et choisissez un début et une fin dans la vue Calendrier.

>[!IMPORTANT]
>
>L’ajout simple d’un filtre de date ne modifie pas les graphiques. Vous devez modifier chacune de vos informations afin d’inclure les dates de début et de fin de votre choix.

![Un tableau de bord personnalisé avec le calendrier du filtre de date mis en surbrillance.](../../../images/customizable-insights/date-filter.png)

Une fois que vous avez sélectionné une plage de dates dans votre tableau de bord, les insights dont le code SQL contient des paramètres de date affichent les options de filtre de dates dans le compositeur de widget.

>[!NOTE]
>
>La sélection d’une période sur votre tableau de bord affiche les bascules des filtres de date dans le cadre du processus de création des informations.

## Suppression d’un filtre de date {#delete-date-filter}

Pour supprimer votre filtre de date, sélectionnez l’icône Supprimer le filtre (![Icône Supprimer le filtre .](../../../images/customizable-insights/delete-filter-icon.png)).

![Un tableau de bord personnalisé avec l’icône de suppression de filtre mise en surbrillance.](../../../images/customizable-insights/delete-date-filter.png)
