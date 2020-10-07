---
keywords: Experience Platform;home;popular topics;export;Export
solution: Experience Platform
title: Guide d’utilisation de Privacy Service
topic: UI guide
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 84%

---


# [!DNL Privacy Service] guide de l&#39;utilisateur

This document provides steps for creating and managing privacy requests using the [!DNL Privacy Service] user interface.

## Browse the [!DNL Privacy Service] UI dashboard

The dashboard for the [!DNL Privacy Service] UI provides two widgets that allow you to view the status of your privacy jobs: &quot;[!UICONTROL Status Report]&quot; and &quot;[!UICONTROL Job Requests]&quot;. Le tableau de bord affiche également la réglementation actuellement sélectionnée pour les tâches affichées.

![Tableau de bord de l’interface utilisateur](../images/user-guide/dashboard.png)

### Type de réglementation

[!DNL Privacy Service] prend en charge les demandes d&#39;emploi pour quatre types de réglementation :

* L&#39;Union européenne [!DNL General Data Protection Regulation] ([!UICONTROL RGPD])
* Le [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* Brésil [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Thaïlande [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])

Les tâches pour chaque type de réglementation sont suivies séparément. Pour passer d’un type de réglementation à l’autre, cliquez sur le menu déroulant **[!UICONTROL Type de réglementation]** et sélectionnez la réglementation souhaitée dans la liste.

![Liste déroulante de type de réglementation](../images/user-guide/regulation.png)

Lorsque vous modifiez le type de réglementation, le tableau de bord se met à jour pour afficher tous les filtres, widgets, ainsi que toutes les opérations et les boîtes de dialogue de création de tâche qui s’appliquent au règlement sélectionné.

![Tableau de bord mis à jour](../images/user-guide/dashboard-update.png)

### Rapport d’état

Le graphique dans la partie gauche du widget Rapport d’état effectue le suivi des tâches envoyées par rapport à toute tâche pouvant avoir été signalée avec des erreurs. Le graphique dans la partie droite effectue le suivi des tâches proches de la fin du délai de conformité de 30 jours.

Cliquez sur l’un des deux boutons situés au-dessus du graphique pour afficher ou masquer leurs mesures respectives.

![](../images/user-guide/hide-errors.png)

Vous pouvez voir le nombre exact de tâches associées à un point de données d’un des graphiques en survolant le point de données en question avec la souris.

![Survol des points de données](../images/user-guide/mouse-over.png)

Pour afficher plus d’informations sur un point de données précis, cliquez sur celui-ci pour afficher les tâches associées dans le widget Requêtes de tâche. Prêtez attention au filtre appliqué juste au-dessus de la liste de tâches.

![Filtre appliqué à partir du widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Lorsqu’un filtre a été appliqué au widget Requêtes de tâche, vous pouvez le supprimer en cliquant sur le **X** dans le cadre de filtre. Les requêtes de tâche reviennent alors à la liste de suivi par défaut.

### Requêtes de tâche

Le widget Requêtes de tâche liste toutes les requêtes de tâche disponibles dans votre organisation et inclut des détails tels que le type de requête, l’état actuel, la date d’échéance et le courrier électronique du demandeur.

>[!NOTE]
>
>Les données relatives aux tâches créées précédemment sont uniquement accessibles pendant 30 jours à compter de la date d’achèvement.

Vous pouvez filtrer la liste en saisissant des mots-clés dans la barre de recherche sous le titre de Requêtes de tâche. La liste est automatiquement filtrée au fur et à mesure de votre saisie, et affiche les requêtes qui contiennent des valeurs correspondant aux termes recherchés. Vous pouvez également utiliser le menu déroulant **[!UICONTROL Demandé le]** afin de sélectionner une période pour les tâches répertoriées.

![Options de recherche de Requête de tâche](../images/user-guide/job-search.png)

Pour consulter les détails d’une requête de tâche spécifique, cliquez sur l’identifiant de celle-ci dans la liste pour ouvrir la page **[!UICONTROL Détails de la tâche]**.

![Interface utilisateur des Détails de la tâche pour le RGPD](../images/user-guide/job-details.png)

This dialog contains status information about each [!DNL Experience Cloud] solution and its current state in relation to the overall job. Chaque tâche de confidentialité étant asynchrone, la page affiche la date et l’heure de communication (GMT) les plus récentes de chaque solution, car certaines d’entre elles nécessitent plus de temps que les autres pour traiter la requête.

Si une solution a fourni des données supplémentaires, elles peuvent être consultées dans cette boîte de dialogue. Vous pouvez consulter ces données en cliquant sur les lignes individuelles de produit.

Pour télécharger l’intégralité des données de tâche sous la forme d’un fichier CSV, cliquez sur **[!UICONTROL Exporter au format CSV]** dans le coin supérieur droit de la boîte de dialogue.

## Création d’une nouvelle requête de tâche de confidentialité

>[!NOTE]
>
>Pour créer une requête de tâche de confidentialité, vous devez fournir des informations d’identité aux clients spécifiques qui souhaitent accéder à leurs données ou les supprimer. Avant de poursuivre la lecture de cette section, consultez le document concernant les [informations d’identité pour les demandes d’accès à des informations personnelles](../identity-data.md).

The [!DNL Privacy Service] UI provides two methods to create new job requests:

* [Utilisation du créateur de requêtes](#request-builder)
* [Chargement d’un fichier JSON](#json)

Les étapes d’utilisation de chacune de ces méthodes sont décrites dans les sections suivantes.

### Utilisation du créateur de requêtes {#request-builder}

À l’aide du créateur de requêtes, vous pouvez créer manuellement une nouvelle requête de tâche de confidentialité dans l’interface utilisateur. Il est préférable d’utiliser le créateur de requêtes pour les jeux de requêtes les plus simples et les plus petits, car les requêtes y sont limitées à un seul type d’identifiant par utilisateur. Pour les requêtes plus complexes, il serait plus pertinent de [charger un fichier JSON](#json) à la place.

Pour commencer à utiliser le créateur de requêtes, cliquez sur **[!UICONTROL Créer une requête]** sous le widget Rapport d’état sur le côté droit de l’écran.

![Cliquez sur Créer une requête](../images/user-guide/create-request.png)

La boîte de dialogue **[!UICONTROL Créer une requête]** s’ouvre et affiche les options disponibles pour envoyer une requête de tâche de confidentialité pour le type de réglementation actuellement sélectionné.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Select the **[!UICONTROL Job Type]** of the request (&quot;Delete&quot; or &quot;Access&quot;) and one or more available products from the list.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Sous **[!UICONTROL Type d’espace de nom]**, sélectionnez le type d’espace de nom approprié pour les identifiants de client envoyés à [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Lors de l’utilisation du type d’espace de nom standard, sélectionnez un espace de nom dans le menu déroulant (adresse électronique, ECID ou AAID), puis saisissez les valeurs d’identifiant dans la zone de texte à droite, en appuyant sur **\&lt;enter>** pour chaque identifiant afin de l’ajouter à la liste.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Lors de l’utilisation du type d’espace de noms personnalisé, vous devez saisir manuellement l’espace de nom avant de fournir les valeurs d’identifiant plus bas.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Chargement d’un fichier JSON {#json}

Lorsque vous créez des requêtes plus complexes, comme celles qui utilisent plusieurs types d’identifiants pour chaque sujet de données traité, vous pouvez créer une requête en chargeant un fichier JSON.

Cliquez sur la flèche près de **[!UICONTROL Créer une requête]**, sous le widget Rapport d’état dans la partie droite de l’écran. Dans la liste des options qui s’affiche, sélectionnez **[!UICONTROL Charger JSON]**.

![Options de création de requête](../images/user-guide/create-options.png)

La boîte de dialogue **[!UICONTROL Charger JSON]** s’affiche, vous permettant ainsi de faire glisser votre fichier JSON dans la fenêtre.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Si vous ne disposez d’aucun fichier JSON à charger, cliquez sur **[!UICONTROL Télécharger Adobe-GDPR-Request.json]** pour télécharger un modèle que vous pouvez compléter en fonction des valeurs collectées auprès de vos sujets des données.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Trouvez le fichier JSON sur votre ordinateur et faites-le glisser dans la fenêtre de dialogue. Si le chargement est réussi, le nom du fichier s’affiche dans la boîte de dialogue. Vous pouvez continuer à ajouter d’autres fichiers JSON si nécessaire en les faisant glisser dans la boîte de dialogue.

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**. La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Étapes suivantes

By reading this document, you have learned how to use the [!DNL Privacy Service] UI to create a privacy job, view a job&#39;s details and monitor its processing status, and download the results once it has completed.

For steps on how to perform these operations programmatically using the [!DNL Privacy Service] API, please refer to the [developer guide](../api/getting-started.md).