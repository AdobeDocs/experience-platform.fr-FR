---
title: Afficher en plus
description: Découvrez les différentes options d’affichage des données analysées SQL. Depuis votre tableau de bord personnalisé, vous pouvez afficher les résultats tabulés de votre analyse ou télécharger les données traitées au format CSV.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 87675263b817a2026741d6bdd094010831d6ea28
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# Afficher plus {#view-more}

Après avoir créé un [insight personnalisé](./overview.md) à l’aide du [mode requête pro](./overview.md#query-pro-mode), vous pouvez afficher les données du graphique dans plusieurs formats. Vous pouvez afficher un formulaire tabulé des résultats ou exporter les données au format CSV ou par e-mail.

## Résultats tabulés {#tabulated-results}

Pour chaque graphique créé à l’aide du mode query pro via SQL, vous pouvez afficher les résultats tabulés de votre analyse dans l’interface utilisateur d’Experience Platform.

Dans votre tableau de bord personnalisé, sélectionnez les points de suspension (`...`) de n’importe quel widget pour accéder aux options [!UICONTROL Afficher plus] et [!UICONTROL Afficher SQL].

![Tableau de bord personnalisé avec un menu déroulant représentant des points de suspension insight et les options Afficher plus et Afficher le SQL mises en surbrillance.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Exporter {#export}

Dans la boîte de dialogue **[!UICONTROL Afficher plus]**, exportez les données du tableau en téléchargeant directement un fichier CSV ou en envoyant un lien vers votre e-mail pour un téléchargement sécurisé ultérieur.

>[!IMPORTANT]
>
>Pour accéder aux options d’exportation, votre administrateur doit vous accorder l’autorisation **[!UICONTROL Exporter les données du tableau de bord]**. Si le bouton [!UICONTROL Exporter] est grisé, contactez votre administrateur. Pour plus d’informations sur les autorisations relatives aux tableaux de bord[&#128279;](../../access-control/home.md) consultez la  Présentation du contrôle d’accès .

>[!NOTE]
>
>Les exportations destinées uniquement à la visualisation ne nécessitent pas l’autorisation [!UICONTROL Exporter les données du tableau de bord]. Par exemple, l’exportation de données traitées à partir de vos [informations sur le tableau de bord personnalisé au format PDF](./export-pdf.md) ou à partir de [informations sur le tableau de bord de l’interface utilisateur de Platform](../download.md).

### Télécharger le fichier CSV {#download-csv}

Dans la boîte de dialogue [!UICONTROL Afficher plus], sélectionnez **[!UICONTROL Exporter]**, puis choisissez **[!UICONTROL Télécharger CSV]** pour télécharger les données du graphique au format CSV.

>[!NOTE]
>
>Le téléchargement du fichier CSV est limité aux 500 premiers enregistrements.

![Boîte de dialogue affichant un aperçu de votre insight et les résultats tabulés de votre SQL qui a généré l’insight.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

### Envoyer en tant qu’e-mail {#send-as-email}

Pour exporter plus de 500 enregistrements, sélectionnez **[!UICONTROL Exporter]** et choisissez **[!UICONTROL Envoyer par e-mail]** dans la boîte de dialogue [!UICONTROL Exporter un fichier]. Cette option envoie en toute sécurité un lien de téléchargement à votre adresse e-mail associée à Adobe. Le nom du destinataire et son adresse e-mail Adobe enregistrée apparaissent dans la section [!UICONTROL Destinataires] de la boîte de dialogue.

![Les options Afficher plus de données de graphique avec les options Exporter et Envoyer par e-mail mises en surbrillance.](../images/sql-insights-query-pro-mode/send-as-email.png)

Après avoir sélectionné [!UICONTROL Envoyer par e-mail], Adobe génère un rapport et envoie un e-mail à l’adresse Adobe enregistrée. L’e-mail comprend un lien de téléchargement sécurisé qui nécessite une authentification via Experience Platform.

>[!NOTE]
>
>Vous devez télécharger le rapport dans les 24 heures suivant la génération du lien ; après cela, le fichier expire.

![L’interface utilisateur d’Experience Platform avec la boîte de dialogue Génération de fichier réussie s’affiche avec l’option Télécharger le rapport.](../images/sql-insights-query-pro-mode/download-report.png)

Pour protéger vos données, Adobe héberge les fichiers exportés en toute sécurité plutôt que de les envoyer en tant que pièces jointes. L’accès nécessite une authentification via l’interface utilisateur d’Experience Platform. Adobe vérifie alors que le fichier est téléchargé uniquement par le destinataire prévu.

Cette méthode vous permet d’exporter **jusqu’à 10 000 enregistrements** et garantit un accès sécurisé aux données sensibles.

## Trier par colonne {#sort-column}

Lors de l’affichage des résultats tabulés, vous pouvez utiliser la fonctionnalité de tri pour trier par colonne dans l’ordre croissant ou décroissant. Depuis votre tableau de bord personnalisé, sélectionnez les points de suspension (`...`) de n’importe quel tableau pour accéder à l’option [!UICONTROL En savoir plus].

![Tableau de bord personnalisé avec le menu déroulant des points de suspension d’un tableau et l’option Afficher plus mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Vous pouvez trier les colonnes en sélectionnant le menu déroulant en regard du nom de la colonne, puis en sélectionnant **[!UICONTROL Trier par ordre croissant]** ou **[!UICONTROL Trier par ordre décroissant]**.

>[!NOTE]
>
>Les options [!UICONTROL Tri croissant] et [!UICONTROL Tri décroissant] n’apparaissent que pour les colonnes configurées avec la fonctionnalité de [tri](./overview.md#advanced-attributes).

![Liste déroulante de colonne de tableau présentant les options de tri croissant et de tri décroissant mises en surbrillance.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Redimensionnement d’une colonne {#resize-column}

Vous pouvez redimensionner les colonnes des résultats tabulés afin d’améliorer la lisibilité des données. Dans le tableau de bord personnalisé, sélectionnez les points de suspension (`...`) du tableau pour accéder à l’option [!UICONTROL En savoir plus]. Utilisez le menu déroulant en regard du nom de la colonne pour la redimensionner, puis sélectionnez **[!UICONTROL Redimensionner la colonne]**.

![Liste déroulante de colonne du tableau présentant l’option Redimensionner la colonne mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Sélectionnez le curseur et faites glisser vers la gauche ou la droite pour ajuster la taille de la colonne selon les besoins.

![Tableau présentant la barre de redimensionnement de la colonne mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Pagination du tableau {#table-pagination}

La pagination est automatiquement appliquée à vos tables dans la fonction [!UICONTROL Afficher plus], ce qui élimine la nécessité de modifier manuellement vos requêtes SQL. Cette fonctionnalité garantit que vos données sont présentées dans un format plus gérable, ce qui facilite le processus de navigation dans les jeux de données volumineux.

Vous pouvez afficher jusqu’à 500 enregistrements par page. Pour parcourir les enregistrements, utilisez le **[!UICONTROL >]** situé au bas de la page.

![Résultats tabulés avec les résultats et la pagination mis en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment afficher les résultats tabulés de l&#39;analyse SQL de votre graphique personnalisé et comment exporter ces données en toute sécurité. Consultez le document Afficher le SQL pour savoir comment [afficher le SQL derrière vos informations personnalisées](./view-sql.md).

Vous pouvez également apprendre à générer des graphiques à partir de modèles de données existants dans l’interface utilisateur de Adobe Experience Platform à l’aide du [&#x200B; guide du mode de conception guidé &#x200B;](../standard-dashboards.md).
