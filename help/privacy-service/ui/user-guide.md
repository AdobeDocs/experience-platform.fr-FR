---
keywords: Experience Platform ; accueil ; rubriques populaires ; exportation ; Exporter
solution: Experience Platform
title: Gérer les tâches liées à la confidentialité dans l’interface utilisateur du Privacy Service
topic: UI guide
description: Découvrez comment utiliser l’interface utilisateur du Privacy Service pour coordonner et surveiller les demandes de confidentialité dans diverses applications Experience Cloud.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 61%

---


# Gérer les tâches de confidentialité dans l’interface utilisateur du Privacy Service

Ce document fournit des étapes pour la création et la gestion des demandes de confidentialité à l&#39;aide de l&#39;interface utilisateur [!DNL Privacy Service].

## Parcourir le tableau de bord d&#39;interface utilisateur [!DNL Privacy Service]

Le tableau de bord de l&#39;interface utilisateur [!DNL Privacy Service] fournit deux widgets qui vous permettent de vue de l&#39;état de vos tâches de confidentialité : &quot;[!UICONTROL Rapport d&#39;état]&quot; et &quot;[!UICONTROL Demandes d&#39;emploi]&quot;. Le tableau de bord affiche également la réglementation actuellement sélectionnée pour les tâches affichées.

![Tableau de bord de l’interface utilisateur](../images/user-guide/dashboard.png)

### Type de réglementation

[!DNL Privacy Service] prend en charge les demandes d’emploi pour plusieurs règlements de confidentialité :

* Le [!DNL California Consumer Privacy Act] ([!UICONTROL ACCP])
* L&#39;Union européenne [!DNL General Data Protection Regulation] ([!UICONTROL RGPD])
* Thaïlande : [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brésil : [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Nouvelle-Zélande [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Les tâches pour chaque type de réglementation sont suivies séparément. Pour passer d&#39;un type de régulation à l&#39;autre, sélectionnez le menu déroulant **[!UICONTROL Type de régulation]** et sélectionnez la régulation désirée dans la liste.

![Liste déroulante de type de réglementation](../images/user-guide/regulation.png)

Lorsque vous modifiez le type de réglementation, le tableau de bord se met à jour pour afficher tous les filtres, widgets, ainsi que toutes les opérations et les boîtes de dialogue de création de tâche qui s’appliquent au règlement sélectionné.

![Tableau de bord mis à jour](../images/user-guide/dashboard-update.png)

### Rapport d’état

Le graphique dans la partie gauche du widget Rapport d’état effectue le suivi des tâches envoyées par rapport à toute tâche pouvant avoir été signalée avec des erreurs. Le graphique dans la partie droite effectue le suivi des tâches proches de la fin du délai de conformité de 30 jours.

Sélectionnez l’un des deux boutons de bascule situés au-dessus du graphique pour afficher ou masquer leurs mesures respectives.

![](../images/user-guide/hide-errors.png)

Vous pouvez voir le nombre exact de tâches associées à un point de données d’un des graphiques en survolant le point de données en question avec la souris.

![Survol des points de données](../images/user-guide/mouse-over.png)

Pour vue d’autres détails sur un point de données donné, sélectionnez le point de données en question pour afficher les tâches associées dans le widget Demandes de tâche. Prêtez attention au filtre appliqué juste au-dessus de la liste de tâches.

![Filtre appliqué à partir du widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Lorsqu’un filtre a été appliqué au widget Demandes de travaux, vous pouvez supprimer le filtre en sélectionnant **X** sur la pilule de filtre. Les requêtes de tâche reviennent alors à la liste de suivi par défaut.

### Requêtes de tâche

Le widget Requêtes de tâche liste toutes les requêtes de tâche disponibles dans votre organisation et inclut des détails tels que le type de requête, l’état actuel, la date d’échéance et le courrier électronique du demandeur.

>[!NOTE]
>
>Les données relatives aux tâches créées précédemment sont uniquement accessibles pendant 30 jours à compter de la date d’achèvement.

Vous pouvez filtrer la liste en saisissant des mots-clés dans la barre de recherche sous le titre de Requêtes de tâche. La liste est automatiquement filtrée au fur et à mesure de votre saisie, et affiche les requêtes qui contiennent des valeurs correspondant aux termes recherchés. Vous pouvez également utiliser le menu déroulant **[!UICONTROL Demandé le]** afin de sélectionner une période pour les tâches répertoriées.

![Options de recherche de Requête de tâche](../images/user-guide/job-search.png)

Pour vue les détails d’une demande de travail spécifique, sélectionnez l’ID de travail de la demande dans la liste afin d’ouvrir la page **[!UICONTROL Détails de la tâche]**.

![Interface utilisateur des Détails de la tâche pour le RGPD](../images/user-guide/job-details.png)

Cette boîte de dialogue contient des informations d&#39;état sur chaque solution [!DNL Experience Cloud] et son état actuel par rapport à la tâche globale. Chaque tâche de confidentialité étant asynchrone, la page affiche la date et l’heure de communication (GMT) les plus récentes de chaque solution, car certaines d’entre elles nécessitent plus de temps que les autres pour traiter la requête.

Si une solution a fourni des données supplémentaires, elles peuvent être consultées dans cette boîte de dialogue. Vous pouvez vue ces données en sélectionnant des lignes de produit individuelles.

Pour télécharger l’ensemble des données de travail au format CSV, sélectionnez **[!UICONTROL Exporter au format CSV]** dans l’angle supérieur droit de la boîte de dialogue.

## Création d’une nouvelle requête de tâche de confidentialité

>[!NOTE]
>
>Pour créer une requête de tâche de confidentialité, vous devez fournir des informations d’identité aux clients spécifiques qui souhaitent accéder à leurs données ou les supprimer. Avant de poursuivre la lecture de cette section, consultez le document concernant les [informations d’identité pour les demandes d’accès à des informations personnelles](../identity-data.md).

L&#39;interface utilisateur [!DNL Privacy Service] fournit deux méthodes pour créer de nouvelles demandes de travaux :

* [Utilisation du créateur de requêtes](#request-builder)
* [Chargement d’un fichier JSON](#json)

Les étapes d’utilisation de chacune de ces méthodes sont décrites dans les sections suivantes.

### Utilisation du créateur de requêtes {#request-builder}

À l’aide du créateur de requêtes, vous pouvez créer manuellement une nouvelle requête de tâche de confidentialité dans l’interface utilisateur. Il est préférable d’utiliser le créateur de requêtes pour les jeux de requêtes les plus simples et les plus petits, car les requêtes y sont limitées à un seul type d’identifiant par utilisateur. Pour les requêtes plus complexes, il serait plus pertinent de [charger un fichier JSON](#json) à la place.

Pour début à l’aide du créateur de requêtes, sélectionnez **[!UICONTROL Créer une requête]** sous le widget Rapport d’état sur la droite de l’écran.

![Sélectionner une demande de création](../images/user-guide/create-request.png)

La boîte de dialogue **[!UICONTROL Créer une requête]** s’ouvre et affiche les options disponibles pour envoyer une requête de tâche de confidentialité pour le type de réglementation actuellement sélectionné.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Sélectionnez le **[!UICONTROL type de tâche]** de la demande (&quot;Supprimer&quot; ou &quot;Accès&quot;) et un ou plusieurs produits disponibles à partir de la liste.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Sous **[!UICONTROL Type d’espace de nom]**, sélectionnez le type d’espace de nom approprié pour les identifiants de client envoyés à [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Lors de l’utilisation du type d’espace de nom standard, sélectionnez un espace de nom dans le menu déroulant (adresse électronique, ECID ou AAID), puis saisissez les valeurs d’identifiant dans la zone de texte à droite, en appuyant sur **\&lt;enter>** pour chaque identifiant afin de l’ajouter à la liste.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Lors de l’utilisation du type d’espace de noms personnalisé, vous devez saisir manuellement l’espace de nom avant de fournir les valeurs d’identifiant plus bas.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Chargement d’un fichier JSON {#json}

Lorsque vous créez des requêtes plus complexes, comme celles qui utilisent plusieurs types d’identifiants pour chaque sujet de données traité, vous pouvez créer une requête en chargeant un fichier JSON.

Sélectionnez la flèche en regard de **[!UICONTROL Créer une requête]**, sous le widget Rapport d&#39;état sur la droite de l&#39;écran. Dans la liste des options qui s’affiche, sélectionnez **[!UICONTROL Charger JSON]**.

![Options de création de requête](../images/user-guide/create-options.png)

La boîte de dialogue **[!UICONTROL Charger JSON]** s’affiche, vous permettant ainsi de faire glisser votre fichier JSON dans la fenêtre.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Si vous n’avez pas de fichier JSON à télécharger, sélectionnez **[!UICONTROL Télécharger Adobe-GDPR-Request.json]** pour télécharger un modèle que vous pouvez renseigner en fonction des valeurs que vous avez collectées auprès de vos sujets de données.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Trouvez le fichier JSON sur votre ordinateur et faites-le glisser dans la fenêtre de dialogue. Si le chargement est réussi, le nom du fichier s’affiche dans la boîte de dialogue. Vous pouvez continuer à ajouter d’autres fichiers JSON si nécessaire en les faisant glisser dans la boîte de dialogue.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer]**. La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Étapes suivantes

En lisant ce document, vous avez appris à utiliser l&#39;interface utilisateur [!DNL Privacy Service] pour créer une tâche de confidentialité, vue les détails d&#39;une tâche et contrôler son état de traitement, et télécharger les résultats une fois qu&#39;elle est terminée.

Pour savoir comment exécuter ces opérations par programmation à l&#39;aide de l&#39;API [!DNL Privacy Service], consultez le [guide du développeur](../api/getting-started.md).