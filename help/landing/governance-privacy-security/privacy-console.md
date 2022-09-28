---
title: Présentation de la console de confidentialité
description: Découvrez comment surveiller vos workflows liés à la confidentialité dans l’interface utilisateur de Adobe Experience Platform.
source-git-commit: 4fa1b826d033ace6536af920b070e8eebbbf401c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# Présentation de Privacy Console

Le [!UICONTROL Console de confidentialité] L’onglet de l’interface utilisateur de Adobe Experience Platform fournit une vue de tableau de bord de vos opérations liées à la confidentialité dans Platform, y compris les ordres de travail d’hygiène des données, les demandes des sujets de données provenant de Privacy Service et les journaux d’audit pour les activités des utilisateurs de Platform.

Pour accéder au tableau de bord, sélectionnez **[!UICONTROL Console de confidentialité]** dans le volet de navigation de gauche.

![Affichage de l&#39;image [!UICONTROL Console de confidentialité] sélectionné dans le volet de navigation de gauche de l’interface utilisateur de Platform](../images/governance-privacy-security/privacy-console/left-nav.png)

À partir de là, vous pouvez consulter les [widgets de surveillance](#widgets) fourni par la console, ou vous pouvez explorer l’une des [guides de cas d’utilisation](#use-case-guides) sur les fonctionnalités de confidentialité de Platform.

## Widgets

[!UICONTROL Console de confidentialité] fournit plusieurs widgets pour vous aider à surveiller vos opérations de confidentialité.

![Affichage de l&#39;image [!UICONTROL Console de confidentialité] sélectionné dans le volet de navigation de gauche de l’interface utilisateur de Platform](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Selon les SKU achetés par votre entreprise, certains widgets mentionnés ci-dessous peuvent ne pas être disponibles.

La fonction de chaque widget est expliquée ci-dessous :

| Nom du widget | Description |
| --- | --- |
| Statut de l’ordre de travail relatif à l’hygiène des données | Affiche les états des processus de suppression des consommateurs sous [Hygiène des données](../../hygiene/home.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7 derniers jours, 14 et 30 jours. |
| Instructions d’hygiène des données récentes | Affiche la plus récente [Hygiène des données](../../hygiene/home.md) les ordres de travail en cours de traitement par le système. Utilisez la liste déroulante pour basculer entre les ordres de travail récemment créés et les ordres de travail récemment mis à jour. |
| Actions les plus fréquentes | Affiche les actions les plus fréquentes sur Platform telles qu’elles sont capturées par [journaux d’audit](./audit-logs/overview.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7 derniers jours, 14 et 30 jours. |
| Les utilisateurs les plus principaux | Affiche les utilisateurs de Platform les plus principaux de votre entreprise, tels qu’ils ont été capturés par [journaux d’audit](./audit-logs/overview.md) pour la période sélectionnée. Utilisez le menu déroulant pour modifier la période entre les 7 derniers jours, 14 et 30 jours. |
| Requêtes de titulaire de données | Affiche le nombre de demandes du sujet des données envoyées et terminées par [Privacy Service](../../privacy-service/home.md) pour un jour donné. |

{style=&quot;table-layout:auto&quot;}

## Guides de cas d’utilisation

La console fournit plusieurs guides intégrés au produit qui vous présentent les processus de confidentialité communs de Platform, y compris des instructions concises sur la configuration d’une mise en oeuvre de base.

![Affichage de l&#39;image [!UICONTROL Console de confidentialité] sélectionné dans le volet de navigation de gauche de l’interface utilisateur de Platform](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Étapes suivantes

Pour plus d’informations sur les différents services Platform liés aux cas d’utilisation de la confidentialité, consultez la documentation suivante :

* [Contrôle d’accès basé sur attribut](../../access-control/abac/overview.md)
* [Journaux d’audit](./audit-logs/overview.md)
* [Gouvernance des données](../../data-governance/home.md)
* [Hygiène des données](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
