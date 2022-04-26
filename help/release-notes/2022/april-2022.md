---
title: Notes de mise à jour de Adobe Experience Platform - Avril 2022
description: Notes de mise à jour d’avril 2022 pour Adobe Experience Platform.
source-git-commit: fe30444fb2d11c38433c73d88ee4c8e9a32bdff8
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 21%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 avril 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Flux de données](#dataflows)
- [Modèle de données d’expérience (XDM)](#xdm)

## Flux de données {#dataflows}

Dans Platform, les données sont ingérées à partir de nombreuses sources différentes, analysées dans le système et activées pour un large éventail de destinations. En offrant de la transparence au niveau des flux de données, Platform facilite le processus de suivi de ce flux de données potentiellement non linéaire.

Les flux de données sont une représentation des tâches qui déplacent des données dans Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers les jeux de données cibles, où elles sont ensuite utilisées par le service d’identités et le profil client en temps réel avant d’être finalement activées vers les destinations.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Tableau de bord Segments | Vous pouvez désormais utiliser le tableau de bord de surveillance pour surveiller les flux de données des segments. Pour en savoir plus, veuillez lire le guide sur [surveillance des segments dans l’interface utilisateur](../../dataflows/ui/monitor-segments.md) |

Pour des informations plus générales sur les flux de données, reportez-vous à la [présentation des flux de données](../../dataflows/home.md). Pour en savoir plus sur la segmentation, reportez-vous à la section [présentation de la segmentation](../../segmentation/home.md).

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

