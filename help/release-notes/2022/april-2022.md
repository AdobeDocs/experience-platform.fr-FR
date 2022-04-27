---
title: Notes de mise à jour de Adobe Experience Platform - Avril 2022
description: Notes de mise à jour d’avril 2022 pour Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: b3655b70a44f878a29c6a401e5957660edebeba6
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 26%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 avril 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Dashboards]](#dashboards)
- [Flux de données](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Édition B2B de Real-time Customer Data Platform](#B2B)
- [Sources](#sources)

## [!DNL Intelligent Services] {#intelligent-services}

Intelligent Services permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données.

Attribution AI et Customer AI permettent aux clients de configurer des modèles AI/ML avancés pour l’attribution marketing et la propension des clients. La fonction Jeux de données multiples permet aux clients d’importer plusieurs jeux de données au moment de la configuration du modèle sans avoir à assembler et à préparer les données à l’avance.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de jeux de données multiples | La fonction Jeux de données multiples prend désormais en charge tous les jeux de données Experience Event ainsi que la sélection de la carte des identités comme identité. Les clients peuvent sélectionner la carte des identités et les identifiants associés, à condition qu’il existe un espace de noms d’identité commun entre les jeux de données. Attribution AI prend en charge les schémas suivants : Adobe Analytics, Événement d’expérience, Événement d’expérience client. Customer AI prend en charge tous ces schémas ainsi que le schéma Adobe Audience Manager. Pour plus d’informations sur la prise en charge de jeux de données multiples dans Attribution AI et Customer AI, reportez-vous à la section [Guide d’utilisation d’Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) et [Guide d’utilisation de Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nouvelles mesures d’évaluation de modèle dans Customer AI | Les nouveaux graphiques Gains de Customer AI permettent aux marketeurs de déterminer la taille du groupe à cibler en fonction de leur budget et de leurs objectifs de retour sur investissement. Les nouveaux graphiques de l’effet élévateur mesurent la qualité du modèle, offrant ainsi une meilleure visibilité sur l’effet élévateur qu’ils obtiendraient par rapport au ciblage aléatoire. Pour plus d’informations, voir [découvrir des informations avec Customer AI ;](../../intelligent-services/customer-ai/user-guide/discover-insights.md) document. |

Pour plus d’informations sur les [!DNL Intelligent Services], consultez la [[!DNL Intelligent Services] présentation](../../intelligent-services/home.md).

## [!DNL Dashboards] {#dashboards}

 Platform propose de nombreux tableaux de bord qui vous permettent d’afficher des informations importantes concernant les données de votre entreprise. Celles-ci sont présentées telles qu’elles sont capturées lors d’aperçus quotidiens.

Les tableaux de bord fournissent des options de création de rapports préconfigurées pour les données de votre entreprise et sont directement intégrés au workflow du marketeur dans Platform. La mise à disposition de ces tableaux de bord ne nécessite pas d’assistance informatique supplémentaire. En outre, ils offrent un gain de temps et d’effort en évitant de recourir à l’exportation et au traitement des données avec une conception et une implémentation d’entreposage de données supplémentaires.

Les widgets suivants sont disponibles via la bibliothèque de widgets sur leurs tableaux de bord respectifs. Consultez la documentation pour plus d’informations sur [comment ajouter des widgets par le biais de la bibliothèque de widgets](../../dashboards/customize/widget-library.md).

| Fonctionnalité | Tableau de bord | Description |
| --------------------------------------------------------- | ------------- | ----------- |
| [!UICONTROL Profils de tendance ajoutée] | Profils | Ce widget utilise un graphique linéaire pour illustrer le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30 derniers jours, 90 jours ou 12 mois. |
| [!UICONTROL Audiences mappées à l’état de destination] | Profils | Ce widget affiche le nombre total d’audiences mappées et non mappées dans une seule mesure et utilise un graphique en anneau pour illustrer la différence proportionnelle entre leurs totaux. |
| [!UICONTROL Taille des audiences] | Profils | Ce widget fournit un tableau à deux colonnes qui répertorie jusqu’à 20 segments et le nombre total d’audiences contenues dans chaque segment. La liste dépend de la stratégie de fusion appliquée et classée de haut en bas en fonction du nombre total d’audiences. |
| [!UICONTROL Tendance du nombre de profils] | Profils | Ce widget utilise un graphique linéaire pour illustrer la tendance du nombre total de profils contenus dans le système au fil du temps. Les données peuvent être visualisées sur des périodes de 30 jours, 90 jours et 12 mois. |
| [!UICONTROL Profils d’identité uniques par identité] | Profils | Ce widget utilise un graphique à barres pour illustrer le nombre total de profils qui sont identifiés avec un seul identifiant unique. Le widget prend en charge jusqu’à cinq des identités les plus courantes. |
| [!UICONTROL État de la destination] | Destinations | Ce widget affiche le nombre total de destinations activées sous la forme d’une mesure unique et utilise un graphique en anneau pour illustrer la différence proportionnelle entre les destinations activées et désactivées. |
| [!UICONTROL Destinations principales par plateforme de destination] | Destinations | Ce widget utilise un tableau à deux colonnes pour afficher la liste des plateformes de destination principales et le nombre total de destinations principales pour chaque plateforme de destination. |
| [!UICONTROL Audiences activées sur toutes les destinations] | Destinations | Ce widget fournit le nombre total d’audiences activées sur toutes les destinations dans une seule mesure. |
| [!UICONTROL Ordre d’activation de l’audience] | Segments | Ce widget fournit un tableau à trois colonnes qui répertorie le nom de destination, la plateforme et la date d’activation de l’audience. |
| [!UICONTROL Tendance de la taille de l’audience] | Segments | Ce widget fournit une représentation graphique linéaire pour le nombre total de profils qui répondent aux critères d’une définition de segment sur des périodes de 30 jours, 90 jours et 12 mois. |
| [!UICONTROL Tendance de changement de la taille de l’audience] | Segments | Ce widget fournit un graphique linéaire qui illustre la différence entre le nombre total de profils qualifiés pour un segment donné et les instantanés quotidiens les plus récents. La période d’analyse des tendances peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. |
| [!UICONTROL Tendance de la taille de l’audience par identité] | Segments | Ce widget illustre la tendance de la taille de l’audience d’un segment particulier en fonction d’un type d’identité sélectionné. La période d’analyse des tendances peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. |

Consultez la documentation pour plus d’informations sur [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md), et [[!DNL Segments]](../../dashboards/guides/segments.md) tableaux de bord.

## Flux de données {#dataflows}

Dans Platform, les données sont ingérées à partir de nombreuses sources différentes, analysées dans le système et activées pour un large éventail de destinations. En offrant de la transparence au niveau des flux de données, Platform facilite le processus de suivi de ce flux de données potentiellement non linéaire.

Les flux de données sont une représentation des tâches qui déplacent des données dans Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers les jeux de données cibles, où elles sont ensuite utilisées par le service d’identités et le profil client en temps réel avant d’être finalement activées vers les destinations.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Tableau de bord Segments | Vous pouvez désormais utiliser le tableau de bord de surveillance pour surveiller les flux de données des segments. Pour en savoir plus, veuillez lire le guide sur [surveillance des segments dans l’interface utilisateur](../../dataflows/ui/monitor-segments.md) |

Pour des informations plus générales sur les flux de données, reportez-vous à la [présentation des flux de données](../../dataflows/home.md). Pour en savoir plus sur la segmentation, reportez-vous à la section [présentation de la segmentation](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la source Adobe Analytics | La source Adobe Analytics prend désormais en charge les fonctionnalités de préparation de données, ce qui vous permet de mapper vos données de suite de rapports Analytics à un schéma XDM cible lors de la création d’un flux de données. Voir le tutoriel sur [création d’une connexion source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) pour plus d’informations. |
| Prise en charge de l’importation de règles de mappage existantes | Vous pouvez désormais importer des règles de mappage à partir d’un flux de données existant afin d’accélérer vos configurations de flux de données et de limiter les erreurs. Voir le tutoriel sur [importation de règles de mappage existantes](../../data-prep/ui/mapping.md) pour plus d’informations. |

Pour plus d’informations sur les [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| [Alertes contextuelles pour les flux de données de destination](../../destinations/ui/alerts.md) | Vous pouvez désormais vous abonner à des alertes lors de la création d’un flux de données de destination, afin de recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux de données. Vous pouvez choisir de recevoir des alertes dans l’interface utilisateur de l’Experience Platform ou par courrier électronique. |

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) | Connectez et activez des données à la plateforme publicitaire Criteo. |
| [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) | Connectez et activez les données à la plateforme Sendgrid pour les emails transactionnels et marketing. |

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification open source qui fournit des structures et des définitions courantes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Ajout ou suppression de champs standard individuels pour un schéma | L’interface utilisateur de l’éditeur de schémas vous permet désormais d’ajouter des parties de groupes de champs standard à vos schémas, offrant ainsi plus de flexibilité aux champs que vous choisissez d’inclure sans avoir à créer de ressources personnalisées à partir de zéro.<br><br>Vous pouvez désormais également définir des champs personnalisés ad hoc directement dans la structure du schéma et les affecter à un nouveau groupe de champs personnalisés ou existant sans avoir à créer ni à modifier au préalable le groupe de champs.<br><br>Consultez le guide sur la [création et modification de schémas dans l’interface utilisateur](../../xdm/ui/resources/schemas.md) pour plus d’informations sur ces nouveaux workflows. |

{style=&quot;table-layout:auto&quot;}

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Schéma global | [[!UICONTROL Demande d’opération d’hygiène des données]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Capture les détails d’une demande de nettoyage des données pour supprimer ou modifier des enregistrements dans un jeu de données ou un environnement de test spécifié. |
| Descripteur | [[!UICONTROL Descripteur de granularité de série temporelle]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indique la granularité des données de série temporelle et de résumé. Lorsqu’il est appliqué à un schéma, le `timestamp` est le premier horodatage d’une période de cette granularité. |
| Classe | [[!UICONTROL Mesures récapitulatives XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fournit des mesures prérésumées avec des dimensions de regroupement, telles que les résultats d’un SQL SELECT avec un GROUP BY. |
| Groupe de champs | [[!UICONTROL Mappage des résultats d’évaluation des stratégies de consentement]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Capture le résultat de l’évaluation de la stratégie de consentement pour une personne. |
| Groupe de champs | [[!UICONTROL Recherche de site]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Capture les informations relatives à la recherche de site, telles que la requête, le filtrage et l’ordre de recherche. |
| Groupe de champs | [[!UICONTROL Fusionner les pistes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Capture les détails d’un événement où plusieurs pistes sont fusionnées. |
| Groupe de champs | [[!UICONTROL E-mails envoyés]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Capture les détails d’un événement où un email est envoyé à un destinataire. |
| Groupe de champs | [[!UICONTROL Assemblage de champs]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Capture les valeurs calculées via le processus de combinaison d’identités pour un événement. |
| Groupe de champs | [[!UICONTROL Détails Du Destinataire Secondaire Pour Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Groupe de champs Adobe Journey Optimizer qui capture les détails d’un destinataire secondaire pour un audit. |
| Groupe de champs | [[!UICONTROL Informations détaillées sur la relation client du compte d’entreprise XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Capture les détails liés à une relation compte-personne. |
| Groupe de champs | [[!UICONTROL Détails de la personne du compte]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Capture les détails liés à une relation compte-personne. |
| Type de données | [[!UICONTROL Panier]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Capture des informations sur un panier de commerce électronique. |
| Type de données | [[!UICONTROL Expédition]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Capture les informations d’expédition pour un ou plusieurs produits. |
| Type de données | [[!UICONTROL Recherche de site]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Capture des informations sur l’activité de recherche de site. |
| Extension (Workfront) | [[!UICONTROL Attributs de tâche opérationnelle]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Capture les détails relatifs à une tâche opérationnelle. |
| Extension (Workfront) | [[!UICONTROL Attributs du Portfolio de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Capture les détails liés à un portfolio de travail. |
| Extension (Workfront) | [[!UICONTROL Attributs du programme de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Capture les détails liés à un programme de travail. |
| Extension (Workfront) | [[!UICONTROL Attributs de projet de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Capture les détails liés à un projet de travail. |

{style=&quot;table-layout:auto&quot;}

**Composants XDM mis à jour**

| Type de composant | Nom | Description de la mise à jour |
| --- | --- | --- |
| Schéma global | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nouvelles valeurs d’énumération pour `destinationCategory`. |
| Descripteur | [[!UICONTROL Descripteur de nom convivial]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Ajout de la prise en charge de la suppression des valeurs suggérées (`meta:enum`) qui ne sont pas nécessaires dans les champs standard. |
| Groupe de champs | [[!UICONTROL Processus de connexion de l’utilisateur]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` champ ajouté. |
| Type de données | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Plusieurs champs liés au panier ont été ajoutés. |
| Type de données | [[!UICONTROL Élément de liste de produits]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nouveaux champs ajoutés pour les options sélectionnées et le montant de la remise. |
| Extension (Intelligent Services) | [[!UICONTROL Optimisation du temps d’envoi pour Intelligent Services JourneyAI]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimisez le format de stockage pour les scores d’heure d’envoi. |
| Extension (Workfront) | [[!UICONTROL Événement de modification Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Plusieurs champs remplacés par un `workfront:customData` pour les champs de formulaire personnalisés. |
| Extension (Workfront) | [[!UICONTROL Attributs de tâche de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Plusieurs champs ont été ajoutés. |
| Extension (Workfront) | [[!UICONTROL Objet de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nouveaux champs pour le type d’objet parent et les champs de formulaire personnalisés. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, voir [Présentation du système XDM](../../xdm/home.md).

### Édition B2B de Real-time Customer Data Platform {#B2B}

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux professionnels du marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de `isDeleted` fonctionnalité | Tous [!DNL Marketo] jeux de données, sauf `Activities` prend désormais en charge la fonction `isDeleted` mappage. Le nouveau mappage est automatiquement ajouté à vos flux de données B2B existants. Vous pouvez utiliser la variable `isDeleted` pour filtrer les enregistrements supprimés afin que vos données dans la variable [!DNL Data Lake] est cohérent avec vos données source. Voir [[!DNL Marketo] guide des champs de mappage](../../sources/connectors/adobe-applications/mapping/marketo.md) pour plus d’informations sur `isDeleted`. |

Pour en savoir plus sur Real-time Customer Data Platform B2B Edition, voir [Présentation B2B](../../rtcdp/b2b-overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de [!DNL OneTrust Integration] | Vous pouvez désormais utiliser la variable [!DNL OneTrust Integration] source pour ingérer les données de consentement et de préférences de votre [!DNL OneTrust] compte à Platform. Consultez la documentation relative à [création d’un [!DNL OneTrust Integration] connexion source](../../sources/connectors/consent-and-preferences/onetrust.md) pour plus d’informations. |
| Prise en charge de [!DNL Square] | Vous pouvez désormais utiliser la variable [!DNL Square] source pour ingérer des données de paiement à partir de votre [!DNL Square] compte à Platform. |
| Prise en charge de la suppression des flux de données Attributs du client | Vous pouvez désormais supprimer les flux de données créés avec le connecteur source Attributs du client. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
