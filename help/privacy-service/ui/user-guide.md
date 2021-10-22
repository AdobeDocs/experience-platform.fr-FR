---
keywords: Experience Platform ; accueil ; rubriques populaires ; exportation ; Exportation
solution: Experience Platform
title: Gestion des tâches de confidentialité dans l’interface utilisateur du Privacy Service
topic-legacy: UI guide
description: Découvrez comment utiliser l’interface utilisateur du Privacy Service pour coordonner et surveiller les demandes de confidentialité entre les différentes applications Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 61%

---

# Gestion des tâches de confidentialité dans l’interface utilisateur du Privacy Service

Ce document fournit les étapes permettant de créer et de gérer les demandes de confidentialité à l’aide de la [!DNL Privacy Service] interface utilisateur.

## Parcourez les [!DNL Privacy Service] Tableau de bord de l’interface utilisateur

Le tableau de bord pour le [!DNL Privacy Service] L’interface utilisateur fournit deux widgets qui vous permettent d’afficher l’état de vos travaux de confidentialité : &quot;[!UICONTROL Rapport d&#39;état]&quot; et &quot;[!UICONTROL Demandes de travaux]&quot;. Le tableau de bord affiche également la réglementation actuellement sélectionnée pour les tâches affichées.

![Tableau de bord de l’interface utilisateur](../images/user-guide/dashboard.png)

### Type de réglementation

[!DNL Privacy Service] prend en charge les demandes d&#39;emploi pour plusieurs règlements relatifs à la protection des renseignements personnels :

* Le [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* L&#39;Union européenne [!DNL General Data Protection Regulation] ([!UICONTROL RGPD])
* Thaïlande [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Le Brésil [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Nouvelle-Zélande [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Les tâches pour chaque type de réglementation sont suivies séparément. Pour basculer entre les types de régulation, sélectionnez l’option **[!UICONTROL Type de règlement]** et sélectionnez le règlement souhaité dans la liste.

![Liste déroulante de type de réglementation](../images/user-guide/regulation.png)

Lorsque vous modifiez le type de réglementation, le tableau de bord se met à jour pour afficher tous les filtres, widgets, ainsi que toutes les opérations et les boîtes de dialogue de création de tâche qui s’appliquent au règlement sélectionné.

![Tableau de bord mis à jour](../images/user-guide/dashboard-update.png)

### Rapport d’état

Le graphique dans la partie gauche du widget Rapport d’état effectue le suivi des tâches envoyées par rapport à toute tâche pouvant avoir été signalée avec des erreurs. Le graphique dans la partie droite effectue le suivi des tâches proches de la fin du délai de conformité de 30 jours.

Sélectionnez l’un des deux boutons bascule au-dessus du graphique pour afficher ou masquer leurs mesures respectives.

![](../images/user-guide/hide-errors.png)

Vous pouvez voir le nombre exact de tâches associées à un point de données d’un des graphiques en survolant le point de données en question avec la souris.

![Survol des points de données](../images/user-guide/mouse-over.png)

Pour afficher des détails supplémentaires sur un point de données donné, sélectionnez le point de données en question pour afficher les tâches associées dans le widget Demandes de travaux. Prêtez attention au filtre appliqué juste au-dessus de la liste de tâches.

![Filtre appliqué à partir du widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Lorsqu’un filtre a été appliqué au widget Demandes de travaux, vous pouvez supprimer le filtre en sélectionnant l’option **X** sur la pilule de filtre. Les requêtes de tâche reviennent alors à la liste de suivi par défaut.

### Requêtes de tâche

Le widget Requêtes de tâche liste toutes les requêtes de tâche disponibles dans votre organisation et inclut des détails tels que le type de requête, l’état actuel, la date d’échéance et le courrier électronique du demandeur.

>[!NOTE]
>
>Les données relatives aux tâches créées précédemment sont uniquement accessibles pendant 30 jours à compter de la date d’achèvement.

Vous pouvez filtrer la liste en saisissant des mots-clés dans la barre de recherche sous le titre de Requêtes de tâche. La liste est automatiquement filtrée au fur et à mesure de votre saisie, et affiche les requêtes qui contiennent des valeurs correspondant aux termes recherchés. Vous pouvez également utiliser le menu déroulant **[!UICONTROL Demandé le]** afin de sélectionner une période pour les tâches répertoriées.

![Options de recherche de Requête de tâche](../images/user-guide/job-search.png)

Pour afficher les détails d&#39;une demande d&#39;emploi particulière, sélectionnez l&#39;ID de tâche de la demande dans la liste pour ouvrir le fichier **[!UICONTROL Détails de la tâche]** .

![Interface utilisateur des Détails de la tâche pour le RGPD](../images/user-guide/job-details.png)

Cette boîte de dialogue contient des informations d’état sur chaque [!DNL Experience Cloud] et son état actuel par rapport au travail global. Chaque tâche de confidentialité étant asynchrone, la page affiche la date et l’heure de communication (GMT) les plus récentes de chaque solution, car certaines d’entre elles nécessitent plus de temps que les autres pour traiter la requête.

Si une solution a fourni des données supplémentaires, elles peuvent être consultées dans cette boîte de dialogue. Vous pouvez afficher ces données en sélectionnant des lignes de produit individuelles.

Pour télécharger l’ensemble des données de travail en tant que fichier CSV, sélectionnez **[!UICONTROL Exporter au format CSV]** en haut à droite de la boîte de dialogue.

## Création d’une nouvelle requête de tâche de confidentialité

>[!NOTE]
>
>Pour créer une requête de tâche de confidentialité, vous devez fournir des informations d’identité aux clients spécifiques qui souhaitent accéder à leurs données ou les supprimer. Avant de poursuivre la lecture de cette section, consultez le document concernant les [informations d’identité pour les demandes d’accès à des informations personnelles](../identity-data.md).

Le [!DNL Privacy Service] L’interface utilisateur propose deux méthodes pour créer des demandes de travaux :

* [Utilisation du créateur de requêtes](#request-builder)
* [Chargement d’un fichier JSON](#json)

Les étapes d’utilisation de chacune de ces méthodes sont décrites dans les sections suivantes.

### Utilisation du créateur de requêtes {#request-builder}

À l’aide du créateur de requêtes, vous pouvez créer manuellement une nouvelle requête de tâche de confidentialité dans l’interface utilisateur. Il est préférable d’utiliser le créateur de requêtes pour les jeux de requêtes les plus simples et les plus petits, car les requêtes y sont limitées à un seul type d’identifiant par utilisateur. Pour les requêtes plus complexes, il serait plus pertinent de [charger un fichier JSON](#json) à la place.

Pour commencer à utiliser le générateur de requêtes, sélectionnez **[!UICONTROL Créer une demande]** sous le widget Rapport d’état sur le côté droit de l’écran.

![Sélectionner Créer une demande](../images/user-guide/create-request.png)

La boîte de dialogue **[!UICONTROL Créer une requête]** s’ouvre et affiche les options disponibles pour envoyer une requête de tâche de confidentialité pour le type de réglementation actuellement sélectionné.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Sélectionnez l’option **[!UICONTROL Type de tâche]** de la demande (&quot;Supprimer&quot; ou &quot;Accès&quot;) et un ou plusieurs produits disponibles dans la liste.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Sous **[!UICONTROL Type d’espace de nom]**, sélectionnez le type d’espace de nom approprié pour les identifiants de client envoyés à [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Lors de l’utilisation du type d’espace de nom standard, sélectionnez un espace de nom dans le menu déroulant (adresse e-mail, ECID ou AAID), puis saisissez les valeurs d’identifiant dans la zone de texte à droite, en appuyant sur **\&lt;enter>** pour chaque identifiant afin de l’ajouter à la liste.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Lors de l’utilisation du type d’espace de noms personnalisé, vous devez saisir manuellement l’espace de nom avant de fournir les valeurs d’identifiant plus bas.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Chargement d’un fichier JSON {#json}

Lorsque vous créez des requêtes plus complexes, comme celles qui utilisent plusieurs types d’identifiants pour chaque sujet de données traité, vous pouvez créer une requête en chargeant un fichier JSON.

Sélectionnez la flèche en regard de **[!UICONTROL Créer une demande]**, sous le widget Rapport d’état sur le côté droit de l’écran. Dans la liste des options qui s’affiche, sélectionnez **[!UICONTROL Charger JSON]**.

![Options de création de requête](../images/user-guide/create-options.png)

La boîte de dialogue **[!UICONTROL Charger JSON]** s’affiche, vous permettant ainsi de faire glisser votre fichier JSON dans la fenêtre.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Si vous n’avez pas de fichier JSON à télécharger, sélectionnez **[!UICONTROL Télécharger Adobe-GDPR-Request.json]** pour télécharger un modèle que vous pouvez remplir en fonction des valeurs que vous avez collectées auprès de vos personnes de données.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Trouvez le fichier JSON sur votre ordinateur et faites-le glisser dans la fenêtre de dialogue. Si le chargement est réussi, le nom du fichier s’affiche dans la boîte de dialogue. Vous pouvez continuer à ajouter d’autres fichiers JSON si nécessaire en les faisant glisser dans la boîte de dialogue.

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**. La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Étapes suivantes

En lisant ce document, vous avez appris à utiliser le fichier [!DNL Privacy Service] Interface utilisateur pour créer une tâche de confidentialité, afficher les détails d&#39;une tâche et contrôler son état de traitement, et télécharger les résultats une fois qu&#39;elle a terminé.

Pour savoir comment effectuer ces opérations par programme à l’aide de la [!DNL Privacy Service] API, reportez-vous à la section [Guide d’API](../api/overview.md).
