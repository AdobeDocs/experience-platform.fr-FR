---
keywords: Experience Platform;accueil;rubriques populaires;exportation;Exporter
solution: Experience Platform
title: Gestion des tâches de confidentialité dans l’interface utilisateur de Privacy Service
description: Découvrez comment utiliser l’interface utilisateur de Privacy Service pour coordonner et surveiller les demandes d’accès à des informations personnelles dans diverses applications Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 45%

---

# Gérer les tâches de confidentialité dans l’interface utilisateur de Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Respecter les demandes d’accès à des informations personnelles des titulaires de données"
>abstract="<h2>Description</h2><p>Adobe Experience Platform Privacy Service vous permet de créer et de gérer les demandes d’accès à des informations personnelles pour le compte de clients et de clientes qui souhaitent accéder à leurs données personnelles ou les supprimer, conformément aux réglementations légales en matière de confidentialité.</p>"

Ce document décrit les étapes à suivre pour créer et gérer des demandes d’accès à des informations personnelles dans l’interface utilisateur [!DNL Privacy Service].

>[!IMPORTANT]
>
>Privacy Service est destiné uniquement aux requêtes relatives aux titulaires de données et aux droits des clientes et clients. Toute autre utilisation de Privacy Service pour le nettoyage ou la maintenance des données n’est ni prise en charge ni autorisée. Adobe a l’obligation légale d’y répondre dans les délais impartis. Par conséquent, le test de chargement sur Privacy Service n’est pas autorisé, car il s’agit d’un environnement de production uniquement qui crée une liste d’attente inutile de requêtes d’accès à des informations personnelles valides.
>
>Une limite de chargement quotidienne stricte est maintenant en place pour prévenir les abus du service. Les utilisateurs et utilisatrices qui abusent du système verront leur accès au service désactivé. Une réunion ultérieure sera ensuite organisée avec ces utilisateurs et utilisatrices afin d’aborder leurs actions et de discuter de l’utilisation acceptable de Privacy Service.

## Parcourir le tableau de bord de l’interface utilisateur de [!DNL Privacy Service]

Le tableau de bord de l’interface utilisateur de [!DNL Privacy Service] fournit deux widgets qui vous permettent d’afficher le statut de vos tâches de confidentialité : « [!UICONTROL Rapport de statut] » et « [!UICONTROL Requêtes de tâche] ». Le tableau de bord affiche également la réglementation actuellement sélectionnée pour les tâches affichées.

![Tableau de bord de l’interface utilisateur](../images/user-guide/dashboard.png)

### Type de réglementation

[!DNL Privacy Service] prend en charge les demandes de traitement pour plusieurs réglementations de confidentialité. Le tableau suivant répertorie les réglementations prises en charge et leur libellé correspondant, tel qu’il est représenté dans l’interface utilisateur :

| Libellé de l’interface utilisateur | Réglementation |
|-------------------------------------|------------------------|
| [!UICONTROL APA_AUS (Australie)] | Le [!DNL Australia Privacy Act] |
| [!UICONTROL CCPA (Californie)] | Le [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPA_USA (Colorado)] | Le [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_USA (Californie)] | Le [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA_USA (Connecticut)] | Le [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DPDPA_USA (Delaware)] | Le [!DNL Delaware Personal Data Privacy Act] |
| [!UICONTROL FDBR_USA (Floride)] | Le [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL RGPD (Union européenne)] | La [!DNL General Data Protection Regulation] de l&#39;Union européenne |
| [!UICONTROL HIPPA_USA (États-Unis)] | Le [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPA_USA] (Iowa) | Le [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA (Brésil) &#x200B;] | La [!DNL Lei Geral de Proteção de Dados] « [!DNL General Data Protection Law] » du Brésil |
| [!UICONTROL MHMDA_USA (Washington)] | Le [!DNL Washington My Health My Data Act] |
| [!UICONTROL MCDPA_USA (Montana)] | Le [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL NDPA_USA (Nebraska)] | Le [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NZPA_NZL (Nouvelle-Zélande)] | [!DNL Privacy Act] de la Nouvelle-Zélande |
| [!UICONTROL NHPA_USA (New Hampshire)] | Le [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_USA (New Jersey)] | Le [!DNL New Jersey Data Protection Act] |
| [!UICONTROL OCPA USA (Oregon)] | Le [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA (Thaïlande)] | [!DNL Personal Data Protection Act] de Thaïlande |
| [!UICONTROL QL25_CAN (Québec)] | [!DNL Quebec Law 25] |
| [!UICONTROL TDPSA USA (Texas)] | Le [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL UCPA_USA (Utah)] | Le [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA (Virginie)] | Le [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!-- 
Waiting:
| **[!UICONTROL PIPA_KOR]**  ?        | South Korea [!DNL Personal Information Privacy Act] |
 -->

>[!NOTE]
>
>Consultez la présentation des [réglementations de confidentialité prises en charge](../regulations/overview.md) pour plus d’informations sur le contexte juridique de chaque réglementation.

Les tâches pour chaque type de réglementation sont suivies séparément. Pour basculer entre les types de régulation, sélectionnez le menu déroulant **[!UICONTROL Type de régulation]** et sélectionnez la régulation souhaitée dans la liste.

![Console Privacy Service avec le menu déroulant Type de réglementation.](../images/user-guide/regulation.png)

Lorsque vous modifiez le type de réglementation, le tableau de bord se met à jour pour afficher tous les filtres, widgets, ainsi que toutes les opérations et les boîtes de dialogue de création de tâche qui s’appliquent au règlement sélectionné.

![Tableau de bord mis à jour](../images/user-guide/dashboard-update.png)

### Rapport d’état

Le graphique dans la partie gauche du widget Rapport d’état effectue le suivi des tâches envoyées par rapport à toute tâche pouvant avoir été signalée avec des erreurs. Le graphique dans la partie droite effectue le suivi des tâches proches de la fin du délai de conformité de 30 jours.

Sélectionnez l’un des deux boutons (bascule) situés au-dessus du graphique pour afficher ou masquer leurs mesures respectives.

![](../images/user-guide/hide-errors.png)

Vous pouvez voir le nombre exact de tâches associées à un point de données d’un des graphiques en survolant le point de données en question avec la souris.

![Survol des points de données](../images/user-guide/mouse-over.png)

Pour afficher plus de détails sur un point de données donné, sélectionnez le point de données en question pour afficher les tâches associées dans le widget Requêtes de tâche. Prêtez attention au filtre appliqué juste au-dessus de la liste de tâches.

![Filtre appliqué à partir du widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Lorsqu’un filtre a été appliqué au widget Requêtes de tâche, vous pouvez supprimer le filtre en sélectionnant la **X** sur la pilule du filtre. Les requêtes de tâche reviennent alors à la liste de suivi par défaut.

### Requêtes de tâche {#job-requests}

L’espace de travail [!UICONTROL Requêtes de tâche] répertorie les détails des requêtes de tâche récentes dans votre organisation. Les détails incluent le type de demande, le statut actuel, la date d’échéance, l’adresse électronique du demandeur, etc. Des ensembles de 100 enregistrements sont chargés à la fois. Par défaut, les tâches les plus récemment créées s’affichent en haut avec plus d’ensembles d’enregistrements chargés lorsque vous faites défiler l’écran vers le bas.

>[!NOTE]
>
>Les données des tâches créées précédemment ne sont accessibles que pendant 30 jours après la date d’achèvement.

Vous pouvez filtrer la liste en saisissant des mots-clés dans la barre de recherche située sous le titre [!UICONTROL Requêtes de tâche]. La liste est automatiquement filtrée au fur et à mesure de votre saisie, et affiche les requêtes qui contiennent des valeurs correspondant aux termes recherchés. Le champ de recherche effectue une recherche « rapide » qui fait correspondre les ID de tâche de confidentialité aux tâches actuellement générées/chargées dans l’interface utilisateur. Il ne s’agit pas d’une recherche complète de toutes les tâches envoyées. Il s’agit plutôt d’un filtre appliqué aux résultats chargés. Utilisez l’API Privacy Service pour [renvoyer des tâches en fonction d’une réglementation spécifique, de périodes ou d’une seule tâche](../api/privacy-jobs.md#list).

>[!TIP]
>
>Pour charger des enregistrements dans l’interface utilisateur des 30 derniers jours, vous devez faire défiler le tableau vers le bas et charger d’autres lots d’enregistrements.

![La section Requête de tâche de la console de confidentialité avec le champ de recherche en surbrillance.](../images/user-guide/job-search.png)

Vous pouvez également utiliser le bouton de recherche pour effectuer une requête de traitement des informations personnelles qui couvre une période spécifique. Cette action renvoie toutes les tâches de confidentialité envoyées par votre organisation pendant la période donnée. Sélectionnez le menu déroulant **[!UICONTROL Demandé le]** pour choisir les dates de début et de fin de la requête. Les options disponibles sont les suivantes : [!UICONTROL Aujourd’hui], [!UICONTROL 7 derniers jours], [!UICONTROL 2 dernières semaines], [!UICONTROL 30 derniers jours] ou [!UICONTROL Personnalisé]. Utilisée avec l’option [!UICONTROL Demandé le], la fonction de recherche affiche uniquement les demandes de traitement envoyées entre les périodes sélectionnées.

![La section Requête de tâche avec le champ de recherche, Demandé dans le menu déroulant et le bouton Rechercher en surbrillance.](../images/user-guide/requested-on-dropdown-menu.png)

Pour afficher les détails d’une demande de traitement spécifique, sélectionnez l’ID de traitement de la demande dans la liste afin d’ouvrir la page **[!UICONTROL Détails du traitement]**.

![Interface utilisateur des Détails de la tâche pour le RGPD](../images/user-guide/job-details.png)

Cette boîte de dialogue contient des informations d’état sur chaque solution [!DNL Experience Cloud] et son état actuel par rapport à la tâche globale. Chaque tâche de confidentialité étant asynchrone, la page affiche la date et l’heure de communication (GMT) les plus récentes de chaque solution, car certaines d’entre elles nécessitent plus de temps que les autres pour traiter la requête.

Si une solution a fourni des données supplémentaires, elles peuvent être consultées dans cette boîte de dialogue. Vous pouvez afficher ces données en sélectionnant des lignes de produits individuelles.

Pour télécharger l’ensemble des données de tâche au format CSV, sélectionnez **[!UICONTROL Exporter au format CSV]** dans le coin supérieur droit de la boîte de dialogue.

## Création d’une nouvelle requête de tâche de confidentialité {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Instructions"
>abstract="<ul><li>Sélectionnez <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=fr#logging-in-from-experience-platform">Demandes</a> dans le volet de navigation de gauche pour ouvrir l’URL de confidentialité, puis sélectionnez <b>Créer une demande</b>.</li><li>Vous pouvez ensuite utiliser le créateur de requêtes ou charger un fichier JSON des titulaires des données.</li><li>Si vous utilisez le créateur de requêtes, sélectionnez le type de tâche (accès et/ou suppression), puis choisissez le type d’identité que vous fournissez (adresse e-mail, ECID ou AAID) ou saisissez un espace de noms d’identité personnalisé. Saisissez les valeurs d’identité appropriées pour les clients et clientes et sélectionnez <b>Créer</b> lorsque vous avez terminé.</li><li>Si vous chargez un fichier JSON, sélectionnez la flèche en regard de l’option Créer une demande. Dans la liste des options, sélectionnez <b>Télécharger un fichier JSON</b> et chargez votre fichier. Si vous ne disposez pas d’un fichier JSON à charger, sélectionnez <b>Télécharger Adobe-GDPR-Request.json</b> pour télécharger un modèle que vous pouvez remplir. Chargez le fichier JSON et sélectionnez <b>Créer</b> lorsque vous avez terminé.</li><li>Pour plus d’informations sur cette fonctionnalité, reportez-vous à la section <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=fr">Guide d’utilisation de Privacy Service</a> sur Experience League.</li></ul>"

>[!NOTE]
>
>Pour créer une demande de traitement d’accès à des informations personnelles, vous devez fournir des informations d’identité pour les clients spécifiques dont les données doivent être consultées ou supprimées. Avant de poursuivre la lecture de cette section, consultez le document concernant les [informations d’identité pour les demandes d’accès à des informations personnelles](../identity-data.md).

L’interface utilisateur de [!DNL Privacy Service] propose deux méthodes pour créer de nouvelles requêtes de tâche :

* [Utiliser le créateur de requêtes](#request-builder)
* [Charger un fichier JSON](#json)

Les étapes d’utilisation de chacune de ces méthodes sont décrites dans les sections suivantes.

### Utiliser le créateur de requêtes {#request-builder}

À l’aide du créateur de requêtes, vous pouvez créer manuellement une nouvelle requête de tâche de confidentialité dans l’interface utilisateur. Il est préférable d’utiliser le créateur de requêtes pour les jeux de requêtes les plus simples et les plus petits, car les requêtes y sont limitées à un seul type d’identifiant par utilisateur. Pour les requêtes plus complexes, il serait plus pertinent de [charger un fichier JSON](#json) à la place.

Pour commencer à utiliser le créateur de requêtes, sélectionnez **[!UICONTROL Créer une requête]** sous le widget Rapport de statut sur la droite de l’écran.

![Sélectionnez Créer une demande](../images/user-guide/create-request.png)

La boîte de dialogue **[!UICONTROL Créer une requête]** s’ouvre et affiche les options disponibles pour envoyer une requête de tâche de confidentialité pour le type de réglementation actuellement sélectionné.

![](../images/user-guide/request-builder.png){width=500}

Sélectionnez le **[!UICONTROL Type de tâche]** de la demande (« Supprimer » ou « Accéder ») et un ou plusieurs produits disponibles dans la liste.

Privacy Service prend en charge deux types de demandes de traitement des données personnelles : [!UICONTROL Accès] (lecture) et/ou [!UICONTROL Suppression]. Vous pouvez envoyer une demande pour recevoir toutes les informations contenues dans le produit qui se rapportent à l&#39;objet de la demande ou demander la suppression de toutes les informations qui se rapportent à l&#39;objet de la demande.

![](../images/user-guide/type-and-products.png){width=500}

Sous **[!UICONTROL Type d’espace de noms]**, sélectionnez le type d’espace de noms approprié pour les ID client envoyés à [!DNL Privacy Service].

![](../images/user-guide/namespace-type.png){width=500}

Lors de l’utilisation du type d’espace de noms standard , sélectionnez un espace de noms dans le menu déroulant (adresse e-mail, ECID ou AAID), puis saisissez les valeurs d’identifiant dans la zone de texte à droite, en appuyant sur **\&lt;enter>** pour chaque identifiant afin de l’ajouter à la liste.

![](../images/user-guide/standard-namespace.png){width=500}

Lors de l’utilisation du type d’espace de noms personnalisé , vous devez saisir manuellement l’espace de noms avant de fournir les valeurs d’identifiant ci-dessous.

![](../images/user-guide/custom-namespace.png){width=500}

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![](../images/user-guide/request-builder-create.png){width=500}

La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Charger un fichier JSON {#json}

Lorsque vous créez des requêtes plus complexes, comme celles qui utilisent plusieurs types d’identifiants pour chaque titulaire de données traité, vous pouvez créer une requête en chargeant un fichier JSON.

Sélectionnez la flèche en regard de **[!UICONTROL Créer une requête]**, sous le widget Rapport de statut sur le côté droit de l’écran. Dans la liste des options qui s’affiche, sélectionnez **[!UICONTROL Charger JSON]**.

![Options de création de requête](../images/user-guide/create-options.png)

La boîte de dialogue **[!UICONTROL Charger JSON]** s’affiche, vous permettant ainsi de faire glisser votre fichier JSON dans la fenêtre.

![](../images/user-guide/upload-json.png){width=500}

Si vous ne disposez pas d’un fichier JSON à charger, sélectionnez **[!UICONTROL Télécharger Adobe-GDPR-Request.json]** pour télécharger un modèle que vous pouvez remplir en fonction des valeurs que vous avez collectées auprès de vos titulaires de données.


![](../images/user-guide/privacy-template.png){width=500}


Trouvez le fichier JSON sur votre ordinateur et faites-le glisser dans la fenêtre de dialogue. Si le chargement est réussi, le nom du fichier s’affiche dans la boîte de dialogue. Vous pouvez continuer à ajouter d’autres fichiers JSON si nécessaire en les faisant glisser dans la boîte de dialogue.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer]**. La boîte de dialogue disparaît et la ou les nouvelles tâches sont répertoriées dans le widget Requêtes de tâche, où s’affiche également leur état de traitement actuel.

### Étapes suivantes

En lisant ce document, vous avez appris à utiliser l’interface utilisateur de [!DNL Privacy Service] pour créer une tâche de confidentialité, afficher les détails d’une tâche et surveiller son statut de traitement, puis télécharger les résultats une fois celle-ci terminée.

Pour savoir comment effectuer ces opérations par programmation à l’aide de l’API [!DNL Privacy Service], reportez-vous au guide [API](../api/overview.md).
