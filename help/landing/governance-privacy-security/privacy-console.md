---
title: Présentation de la console de confidentialité
description: Découvrez comment surveiller vos workflows liés à la confidentialité dans l’interface utilisateur de Adobe Experience Platform.
feature: Privacy
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 4%

---

# Présentation de la console de confidentialité

L’onglet [!UICONTROL Console de confidentialité] de l’interface utilisateur de Adobe Experience Platform fournit une vue sous forme de tableau de bord de vos opérations liées à la confidentialité dans Experience Platform, y compris les ordres de travail de nettoyage de données, les demandes des titulaires de données de Privacy Service et les journaux d’audit pour les activités des utilisateurs d’Experience Platform.

Pour accéder au tableau de bord, sélectionnez **[!UICONTROL Console de confidentialité]** dans le volet de navigation de gauche.

![Image montrant la sélection de [!UICONTROL Console de confidentialité] dans le volet de navigation de gauche de l’interface utilisateur d’Experience Platform](../images/governance-privacy-security/privacy-console/left-nav.png)

À partir de là, vous pouvez consulter les [widgets de surveillance](#widgets) fournis par la console ou explorer l’un des nombreux [guides de cas d’utilisation](#use-case-guides) sur les fonctionnalités de confidentialité d’Experience Platform.

## Widgets

[!UICONTROL Privacy Console] fournit plusieurs widgets pour vous aider à surveiller vos opérations de confidentialité.

![Image montrant la sélection de [!UICONTROL Console de confidentialité] dans le volet de navigation de gauche de l’interface utilisateur d’Experience Platform](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Selon les SKU achetés par votre organisation, certains des widgets mentionnés ci-dessous peuvent ne pas être disponibles.

La fonction de chaque widget est expliquée ci-dessous :

| Nom du widget | Description |
| --- | --- |
| Statut de l’ordre de travail d’hygiène des données | Affiche les statuts des processus de suppression d&#39;enregistrements sous [Hygiène des données](../../hygiene/home.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7, 14 et 30 derniers jours. |
| Ordres de travail d’hygiène des données récents | Affiche les derniers ordres de travail [Hygiène des données](../../hygiene/home.md) traités par le système. Utilisez la liste déroulante pour basculer entre les ordres de travail récemment créés et les ordres de travail récemment mis à jour. |
| Actions les plus fréquentes | Affiche les actions les plus fréquentes sur Experience Platform, telles qu’elles sont capturées par [journaux d’audit](./audit-logs/overview.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7, 14 et 30 derniers jours. |
| Utilisateurs les plus actifs | Affiche les utilisateurs Experience Platform les plus actifs au sein de votre organisation, tels qu’ils sont capturés par [journaux d’audit](./audit-logs/overview.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7, 14 et 30 derniers jours. |
| Requêtes des titulaires de données | Affiche le nombre de demandes des titulaires de données envoyées et traitées par [Privacy Service](../../privacy-service/home.md) pour un jour donné. |

{style="table-layout:auto"}

## Guides de cas d’utilisation

La console fournit plusieurs guides intégrés au produit qui vous présentent les workflows courants relatifs à la confidentialité dans Experience Platform, y compris des instructions concises sur la configuration d’une implémentation de base.

![Image montrant la sélection de [!UICONTROL Console de confidentialité] dans le volet de navigation de gauche de l’interface utilisateur d’Experience Platform](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Étapes suivantes

Pour plus d’informations sur les différents services Experience Platform liés aux cas d’utilisation de confidentialité, consultez la documentation suivante :

* [Contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md)
* [Journaux d’audit](./audit-logs/overview.md)
* [Gouvernance des données](../../data-governance/home.md)
* [Hygiène des données](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
