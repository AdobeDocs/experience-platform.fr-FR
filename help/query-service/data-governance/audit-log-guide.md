---
title: Intégration du journal d’audit de Query Service
description: Les journaux d’audit de Query Service conservent des enregistrements pour diverses actions de l’utilisateur afin de former un journal d’audit pour la résolution des problèmes ou le respect des politiques de gestion des données d’entreprise et des exigences réglementaires. Ce tutoriel présente un aperçu des fonctionnalités de journal d’audit spécifiques à Query Service.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 8%

---

# [!DNL Query Service] intégration du journal d’audit

L’intégration du journal d’audit Adobe Experience Platform [!DNL Query Service] fournit des enregistrements des actions utilisateur liées aux requêtes. Les journaux d’audit sont un outil essentiel pour résoudre les problèmes et respecter les politiques de gestion des données d’entreprise et les exigences réglementaires. La fonctionnalité vous permet de renvoyer un journal des actions pour de nombreux types d’événements, de filtrer et d’exporter les enregistrements. Les journaux sont accessibles via l’interface utilisateur de Platform ou l’ [API de requête d’audit](https://www.adobe.io/experience-platform-apis/references/audit-query/) et téléchargés au format de fichier CSV ou JSON.

Pour en savoir plus sur l’interface utilisateur des journaux d’audit, consultez le [document de présentation des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md). Pour en savoir plus sur l’émission d’appels aux API Platform, consultez le [guide de l’API des journaux d’audit](../../landing/api-guide.md).

## Conditions préalables

Vous devez disposer de l’autorisation [!DNL Data Governance] [!UICONTROL Afficher le journal d’activité de l’utilisateur] activée pour afficher le tableau de bord du journal d’audit dans l’interface utilisateur de Platform. L’autorisation est activée via l’[Admin Console](https://adminconsole.adobe.com/) d’Adobe. Contactez l’administrateur ou administratrice de votre organisation si vous ne disposez pas des privilèges d’administrateur pour activer cette autorisation. Consultez la documentation sur le contrôle d’accès pour des [instructions complètes sur l’ajout d’autorisations via Admin Console](../../access-control/home.md).

## [!DNL Query Service] catégories de journaux d’audit {#audit-log-categories}

Les catégories de journaux d’audit fournies par [!DNL Query Service] sont les suivantes.

| Catégorie | Description |
|---|---|
| [!UICONTROL Requête] | Cette catégorie permet de contrôler les exécutions de requête. |
| [!UICONTROL Modèle de requête] | Cette catégorie permet de contrôler les différentes actions (création, mise à jour et suppression) effectuées sur un modèle de requête. |
| [!UICONTROL Requête planifiée] | Cette catégorie vous permet de contrôler les plannings qui ont été créés, mis à jour ou supprimés dans [!DNL Query Service]. |

## Exécution d’un journal d’audit [!DNL Query Service] {#perform-an-audit-log}

Pour effectuer un audit pour les activités [!DNL Query Service], sélectionnez **[!UICONTROL Audits]** dans le volet de navigation de gauche, suivi de l’icône d’entonnoir (![Icône de filtre).](/help/images/icons/filter.png)) pour afficher une liste de contrôles de filtre permettant d’affiner les résultats.

![Le tableau de bord du journal d’audit de l’interface utilisateur de Platform avec &quot;Audits&quot; dans le volet de navigation de gauche et les contrôles de filtre mis en surbrillance.](../images/audit-log/filter-controls.png)

Depuis l’onglet [!UICONTROL Audits] du tableau de bord [!UICONTROL Journal d’activité] , vous pouvez filtrer toutes les actions de la plateforme enregistrées par l’une des catégories [!DNL Query Service] . Les résultats du journal peuvent être filtrés davantage en fonction de la période pendant laquelle ils ont été exécutés, de l’action/de la fonction entreprise ou de l’utilisateur ayant déclenché la requête. Consultez la documentation du journal d’audit pour obtenir des [ instructions complètes sur la manière de filtrer les journaux en fonction de la catégorie, de l’action, de l’utilisateur et de l’état](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Les données du journal d’audit renvoyées contiennent les informations suivantes sur toutes les requêtes qui répondent aux critères de filtrage de votre choix.

| Nom de la colonne | Description |
|---|---|
| [!UICONTROL Horodatage] | Date et heure exactes de l’action effectuée au format `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Nom de ressource] | La valeur du champ [!UICONTROL Nom de la ressource] dépend de la catégorie choisie comme filtre. Lors de l’utilisation de la catégorie [!UICONTROL Requête planifiée], il s’agit du **nom du planning**. Lors de l’utilisation de la catégorie [!UICONTROL Modèle de requête], il s’agit du **nom du modèle**. Lors de l’utilisation de la catégorie [!UICONTROL Query], il s’agit de l’ **ID de session** |
| [!UICONTROL Catégorie] | Ce champ correspond à la catégorie que vous avez sélectionnée dans la liste déroulante des filtres. |
| [!UICONTROL Action] | Il peut s’agir de créer, supprimer, mettre à jour ou exécuter . Les actions disponibles dépendent de la catégorie choisie comme filtre. |
| [!UICONTROL Utilisateur] | Ce champ indique l’identifiant de l’utilisateur qui a exécuté la requête. |

![Le tableau de bord Audits avec le journal d’activité filtré en surbrillance.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Pour plus d’informations sur les requêtes, téléchargez les résultats du journal dans des formats de fichiers CSV ou JSON, par défaut, affichés dans le tableau de bord du journal d’audit.

## Panneau Détails

Sélectionnez une ligne de résultats du journal d’audit pour ouvrir un panneau de détails à droite de l’écran.

![Onglet Journal d’activité du tableau de bord Audits avec le panneau des détails surligné.](../images/audit-log/details-panel.png)

Le panneau Détails peut être utilisé pour trouver l’ [!UICONTROL ID de ressource] et l’ [!UICONTROL  état de l’événement].

La valeur de l’ [!UICONTROL ID de ressource] varie en fonction de la catégorie utilisée dans l’audit.

* Lors de l&#39;utilisation de la catégorie [!UICONTROL Requête], l&#39; [!UICONTROL ID de ressource] est l&#39; **ID de session**.
* Lors de l’utilisation de la catégorie [!UICONTROL Modèle de requête], l’ [!UICONTROL ID de ressource] est l’ **ID de modèle** et est précédé de `[!UICONTROL templateID:]`.
* Lors de l’utilisation de la catégorie [!UICONTROL Requête planifiée], l’ [!UICONTROL ID de ressource] est l’ **ID de planification** et est précédé du préfixe `[!UICONTROL scheduleID:]`.

La valeur de l’ [!UICONTROL état de l’événement] change en fonction de la catégorie utilisée dans l’audit.

* Lors de l’utilisation de la catégorie [!UICONTROL Requête], le champ [!UICONTROL État de l’événement] fournit une liste de tous les **ID de requête** exécutés par l’utilisateur au cours de cette session.
* Lors de l’utilisation de la catégorie [!UICONTROL Modèle de requête], le champ [!UICONTROL État de l’événement] fournit le **nom du modèle** comme préfixe pour l’état de l’événement.
* Lors de l’utilisation de la catégorie [!UICONTROL Planification de la requête], le champ [!UICONTROL État de l’événement] fournit le **nom du planning** comme préfixe pour l’état de l’événement.

## Filtres disponibles pour les catégories de journaux d’audit [!DNL Query Service] {#available-filters}

Les filtres disponibles varient selon la catégorie sélectionnée dans la liste déroulante. Le tableau suivant décrit les filtres disponibles pour les [[!DNL Query Service] catégories de journaux d’audit](#audit-log-categories).

| Filtre | Description |
|---|---|
| Catégorie | Pour obtenir la liste complète des catégories disponibles, reportez-vous à la section [[!DNL Query Service] catégories de journaux d’audit](#audit-log-categories) . |
| Action | En ce qui concerne les catégories d’audit [!DNL Query Service], la mise à jour est une **modification du formulaire existant**, la suppression est la **suppression du planning ou du modèle**, la création est **création d’un nouveau planning ou modèle** et l’exécution est **exécution d’une requête**. |
| Utilisateur | Saisissez l’ID utilisateur complet (par exemple, johndoe@acme.com) à filtrer par utilisateur. |
| Statut | Les options [!UICONTROL Autoriser], [!UICONTROL Succès] et [!UICONTROL Échec] filtrent les journaux en fonction de &quot;État&quot; ou &quot;État de l’événement&quot;, tandis que l’option [!UICONTROL Refuser] filtrera les **tous** journaux. |
| Date | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. |

## Étapes suivantes

En lisant ce document, vous comprenez mieux la fonctionnalité de journal d’audit [!DNL Query Service] et son utilisation pour filtrer vos actions utilisateur [!DNL Query Service].

Si vous utilisez la fonctionnalité de journal d’audit [!DNL Query Service] à des fins de dépannage, il est recommandé de lire le [guide de dépannage](../troubleshooting-guide.md).
