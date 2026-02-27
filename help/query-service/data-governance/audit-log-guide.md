---
title: Intégration du journal d’audit de Query Service
description: Les journaux d’audit de Query Service conservent des enregistrements pour diverses actions des utilisateurs afin de former un journal d’audit pour résoudre les problèmes ou respecter les politiques de gestion des données d’entreprise et les exigences réglementaires. Ce tutoriel présente une vue d’ensemble des fonctionnalités du journal d’audit spécifiques à Query Service.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: d3b73124795cfdeb5f8f1890105bf9c174711b36
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 8%

---

# Intégration du journal d’audit [!DNL Query Service]

L’intégration du journal d’audit Adobe Experience Platform [!DNL Query Service] fournit des enregistrements des actions utilisateur liées aux requêtes. Les journaux d’audit sont un outil essentiel pour résoudre les problèmes et respecter les politiques de gestion des données d’entreprise et les exigences réglementaires. Cette fonctionnalité vous permet de renvoyer un journal d’actions pour de nombreux types d’événements, ainsi que de filtrer et d’exporter les enregistrements. Les journaux sont accessibles via l’interface utilisateur d’Experience Platform ou l’[API Audit Query](https://www.adobe.io/experience-platform-apis/references/audit-query/) et téléchargés au format CSV ou JSON.

Pour en savoir plus sur l’interface utilisateur des journaux d’audit, consultez le document [présentation des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md). Pour en savoir plus sur l’émission d’appels vers les API Experience Platform, consultez le guide [API des journaux d’audit](../../landing/api-guide.md).

>[!NOTE]
>
>Les actions d’éviction de session sont consignées. Pour les workflows de l’interface utilisateur, voir [Gestion des sessions Query Service](../ui/session-management.md).

## Conditions préalables

L’autorisation [!DNL Data Governance] [!UICONTROL View User Activity Log] doit être activée pour afficher le tableau de bord du journal d’audit dans l’interface utilisateur d’Experience Platform. L’autorisation est activée via l’[Admin Console](https://adminconsole.adobe.com/) d’Adobe. Contactez l’administrateur ou administratrice de votre organisation si vous ne disposez pas des privilèges d’administrateur pour activer cette autorisation. Consultez la documentation sur le contrôle d’accès pour des [instructions complètes sur l’ajout d’autorisations via Admin Console](../../access-control/home.md).

## Catégories de journaux d’audit [!DNL Query Service] {#audit-log-categories}

Les catégories de journaux d’audit fournies par [!DNL Query Service] sont les suivantes.

| Catégorie | Description |
|---|---|
| [!UICONTROL Query] | Cette catégorie vous permet d’auditer les exécutions de requêtes. |
| [!UICONTROL Query template] | Cette catégorie vous permet d’auditer les différentes actions (création, mise à jour et suppression) effectuées sur un modèle de requête. |
| [!UICONTROL Scheduled query] | Cette catégorie vous permet de contrôler les plannings qui ont été créés, mis à jour ou supprimés dans [!DNL Query Service]. |

## Exécution d’un journal d’audit [!DNL Query Service] {#perform-an-audit-log}

Pour effectuer un audit des activités [!DNL Query Service], sélectionnez **[!UICONTROL Audits]** dans le volet de navigation de gauche, suivi de l’icône funnel (![Icône Filtrer .](/help/images/icons/filter.png)) pour afficher une liste de contrôles de filtre afin de limiter les résultats.

![Tableau de bord du journal d’audit de l’interface utilisateur d’Experience Platform avec « Audits » en surbrillance dans les commandes de navigation et de filtrage de gauche.](../images/audit-log/filter-controls.png)

Dans l’onglet [!UICONTROL Audits] du tableau de bord [!UICONTROL Activity log] , vous pouvez filtrer toutes les actions Experience Platform enregistrées par l’une des catégories de [!DNL Query Service]. Les résultats du journal peuvent être filtrés en fonction de la période pendant laquelle ils ont été exécutés, de l’action/la fonction exécutée ou de l’utilisateur qui a exécuté la requête. Consultez la documentation sur le journal d’audit pour [des instructions complètes sur la manière de filtrer les journaux en fonction de la catégorie, de l’action, de l’utilisateur et du statut](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Les données du journal d’audit renvoyées contiennent les informations suivantes sur toutes les requêtes qui répondent aux critères de filtre de votre choix.

| Nom de la colonne | Description |
|---|---|
| [!UICONTROL Timestamp] | Date et heure exactes de l’action effectuée au format `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Asset Name] | La valeur du champ [!UICONTROL Asset Name] dépend de la catégorie choisie comme filtre. Lors de l’utilisation de la catégorie de [!UICONTROL Scheduled query], il s’agit du **nom du planning**. Lors de l’utilisation de la catégorie de [!UICONTROL Query template], il s’agit du **nom du modèle**. Lors de l’utilisation de la catégorie [!UICONTROL Query] , il s’agit de l’**ID de session** |
| [!UICONTROL Category] | Ce champ correspond à la catégorie sélectionnée par vous dans la liste déroulante de filtre. |
| [!UICONTROL Action] | Il peut s’agir de créer, supprimer, mettre à jour ou exécuter. Les actions disponibles dépendent de la catégorie choisie comme filtre. |
| [!UICONTROL User] | Ce champ fournit l’identifiant utilisateur qui a exécuté la requête. |

![Tableau de bord Audits avec le journal d’activité filtré en surbrillance.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Vous obtiendrez plus de détails sur la requête en téléchargeant les résultats du journal au format CSV ou JSON que ce qui s’affiche par défaut dans le tableau de bord du journal d’audit.

## Panneau Détails

Sélectionnez une ligne de résultats du journal d’audit pour ouvrir un panneau de détails à droite de l’écran.

![Onglet Journal d’activité du tableau de bord Audits avec le panneau des détails en surbrillance.](../images/audit-log/details-panel.png)

Le panneau des détails peut être utilisé pour rechercher le [!UICONTROL Asset ID] et le [!UICONTROL Event status].

La valeur de la [!UICONTROL Asset ID] varie en fonction de la catégorie utilisée dans l’audit.

* Lors de l’utilisation de la catégorie de [!UICONTROL Query], la [!UICONTROL Asset ID] est l’**ID de session**.
* Lors de l’utilisation de la catégorie de [!UICONTROL Query template], la [!UICONTROL Asset ID] est l’**ID de modèle** et comporte le préfixe `[!UICONTROL templateID:]`.
* Lors de l’utilisation de la catégorie de [!UICONTROL Scheduled query], la [!UICONTROL Asset ID] est l’**ID de planning** et comporte le préfixe `[!UICONTROL scheduleID:]`.

La valeur de la [!UICONTROL Event status] varie en fonction de la catégorie utilisée dans l’audit.

* Lors de l’utilisation de la catégorie [!UICONTROL Query] , le champ [!UICONTROL Event status] fournit une liste de tous les **ID de requête** exécutés par l’utilisateur au cours de cette session.
* Lors de l’utilisation de la catégorie [!UICONTROL Query template] , le champ [!UICONTROL Event status] fournit le **nom du modèle** comme préfixe du statut de l’événement.
* Lors de l’utilisation de la catégorie [!UICONTROL Query schedule] , le champ [!UICONTROL Event status] fournit le **nom du planning** comme préfixe du statut de l’événement.

## Filtres disponibles pour [!DNL Query Service] catégories de journaux d’audit {#available-filters}

Les filtres disponibles varient en fonction de la catégorie sélectionnée dans la liste déroulante. Le tableau suivant décrit les filtres disponibles pour les [[!DNL Query Service] catégories du journal d’audit](#audit-log-categories).

| Filtre | Description |
|---|---|
| Catégorie | Consultez la section [[!DNL Query Service] catégories du journal d’audit](#audit-log-categories) pour obtenir une liste complète des catégories disponibles. |
| Action | Lorsque vous faites référence à [!DNL Query Service] catégories d’audit, la mise à jour est une **modification du formulaire existant**, la suppression est la **suppression du planning ou du modèle**, la création est **création d’un planning ou d’un modèle** et l’exécution est **exécution d’une requête**. |
| Utilisateur ou utilisatrice | Saisissez l’ID utilisateur complet (par exemple, johndoe@acme.com) à filtrer par utilisateur. |
| Statut | Les options [!UICONTROL Allow], [!UICONTROL Success] et [!UICONTROL Failure] filtrent les journaux en fonction du « Statut » ou du « Statut de l’événement », tandis que l’option [!UICONTROL Deny] filtre **tous** les journaux. |
| Date | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. |

## Étapes suivantes

Grâce à la lecture de ce document, vous comprenez mieux la fonctionnalité de journal d’audit [!DNL Query Service] et comment elle peut être utilisée pour filtrer vos actions utilisateur [!DNL Query Service].

Si vous utilisez la fonctionnalité de journal d’audit [!DNL Query Service] à des fins de dépannage, nous vous recommandons de lire le guide de dépannage [](../troubleshooting-guide.md).
