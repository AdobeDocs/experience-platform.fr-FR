---
title: Présentation de la console de confidentialité
description: Découvrez comment surveiller vos workflows liés à la confidentialité dans l’interface utilisateur de Adobe Experience Platform.
feature: Privacy
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 4%

---

# Présentation de Privacy Console

L’onglet [!UICONTROL Console de confidentialité] de l’interface utilisateur de Adobe Experience Platform fournit un tableau de bord de vos opérations liées à la confidentialité dans Platform, y compris les commandes de travail relatives à l’hygiène des données, les demandes des titulaires de données de Privacy Service et les journaux d’audit pour les activités des utilisateurs de Platform.

Pour accéder au tableau de bord, sélectionnez **[!UICONTROL Console de confidentialité]** dans le volet de navigation de gauche.

![Image montrant la [!UICONTROL console de confidentialité] sélectionnée dans le volet de navigation de gauche de l’interface utilisateur de Platform](../images/governance-privacy-security/privacy-console/left-nav.png)

À partir de là, vous pouvez consulter les [widgets de surveillance](#widgets) disponibles fournis par la console, ou vous pouvez explorer l’un des [ ](#use-case-guides) guides de cas d’utilisation sur les fonctionnalités de confidentialité de Platform.

## Widgets

[!UICONTROL Privacy Console] fournit plusieurs widgets pour vous aider à surveiller vos opérations de confidentialité.

![Image montrant la [!UICONTROL console de confidentialité] sélectionnée dans le volet de navigation de gauche de l’interface utilisateur de Platform](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Selon les SKU achetés par votre entreprise, certains widgets mentionnés ci-dessous peuvent ne pas être disponibles.

La fonction de chaque widget est expliquée ci-dessous :

| Nom du widget | Description |
| --- | --- |
| Statut de l’ordre de travail relatif à l’hygiène des données | Affiche les états des processus de suppression d’enregistrements sous [Hygiène des données](../../hygiene/home.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7 derniers jours, 14 et 30 jours. |
| Instructions d’hygiène des données récentes | Affiche les ordres de travail [Hygiène des données](../../hygiene/home.md) les plus récents traités par le système. Utilisez la liste déroulante pour basculer entre les ordres de travail récemment créés et les ordres de travail récemment mis à jour. |
| Actions les plus fréquentes | Affiche les actions les plus fréquentes sur Platform telles qu’elles sont capturées par les [journaux d’audit](./audit-logs/overview.md) pendant la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7 derniers jours, 14 et 30 jours. |
| Utilisateurs les plus actifs | Affiche les utilisateurs de Platform les plus actifs au sein de votre organisation, tels qu’ils ont été capturés par les [journaux d’audit](./audit-logs/overview.md) pendant la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7 derniers jours, 14 et 30 jours. |
| Requêtes de titulaire de données | Affiche le nombre de demandes des titulaires de données soumises et terminées par [Privacy Service](../../privacy-service/home.md) pour un jour donné. |

{style="table-layout:auto"}

## Guides de cas d’utilisation

La console fournit plusieurs guides intégrés au produit qui vous présentent les processus de confidentialité communs de Platform, y compris des instructions concises sur la configuration d’une mise en oeuvre de base.

![Image montrant la [!UICONTROL console de confidentialité] sélectionnée dans le volet de navigation de gauche de l’interface utilisateur de Platform](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Étapes suivantes

Pour plus d’informations sur les différents services Platform liés aux cas d’utilisation de la confidentialité, consultez la documentation suivante :

* [Contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md)
* [Journaux d’audit](./audit-logs/overview.md)
* [Gouvernance des données](../../data-governance/home.md)
* [Hygiène des données](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
