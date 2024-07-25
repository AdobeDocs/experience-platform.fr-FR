---
title: Afficher Insight SQL
description: Affichez le code SQL derrière votre profil, audience, destination et informations personnalisées et exécutez la requête à la demande via Query Editor.
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Afficher les informations SQL

Utilisez la fonction [!UICONTROL Afficher SQL] pour afficher le code SQL derrière votre profil, audience, destination et informations personnalisées et exécuter la requête à la demande via l’éditeur de requêtes. Tirer parti du SQL de plus de 40 insights existants pour créer de nouvelles requêtes qui obtiennent des insights uniques à partir des données de Platform en fonction des besoins de votre entreprise.

## Accès à la présentation du tableau de bord {#navigate-to-overview}

Pour ouvrir le tableau de bord de votre choix, sélectionnez **[!UICONTROL Profils]**, **[!UICONTROL Audiences]** ou **[!UICONTROL Destinations]** dans le volet de navigation de gauche. Sélectionnez ensuite **[!UICONTROL Aperçu]** dans les options de l’onglet si l’espace de travail n’apparaît pas automatiquement.

Vous pouvez également sélectionner **[!UICONTROL Tableaux de bord]** dans le volet de navigation de gauche suivi du nom de votre tableau de bord personnalisé. L’aperçu de votre tableau de bord défini par l’utilisateur s’affiche.

![L’interface utilisateur de l’Experience Platform avec [!UICONTROL  Profils], [!UICONTROL Audiences], [!UICONTROL Destinations] et [!UICONTROL Tableaux de bord] surlignés.](./images/view-sql/dashboard-navigation.png)

## Bascule de l’affichage SQL {#toggle}

Un bouton d’activation/désactivation est disponible dans la vue d’ensemble des tableaux de bord Profil, Audience, Destination et définis par l’utilisateur pour activer ou désactiver la fonctionnalité.

>[!NOTE]
>
>Si vous activez le bouton d’activation/désactivation [!UICONTROL Afficher SQL], vous ne pouvez pas modifier les filtres globaux et de niveau widget tant que vous n’avez pas désactivé la fonction.

![Le bouton bascule [!UICONTROL Afficher SQL] mis en surbrillance.](./images/view-sql/view-sql-toggle.png)

Activez le bouton à bascule pour afficher le texte [!UICONTROL Afficher SQL] sur chaque insight individuelle.

![Une information avec [!UICONTROL Afficher SQL] mise en évidence.](./images/view-sql/insight-view-sql.png)

Sélectionnez **[!UICONTROL Afficher SQL]** pour ouvrir une boîte de dialogue contenant le SQL du widget.

## Boîte de dialogue SQL {#sql-dialog}

Une boîte de dialogue s’affiche et contient le titre de l’insight et du code SQL qui la génère.

>[!TIP]
>
>Vous pouvez copier l’intégralité de l’instruction SQL dans le presse-papiers en sélectionnant l’icône Copier (![Icône Copier.](/help/images/icons/copy.png)) en haut à droite de la boîte de dialogue.

![Une boîte de dialogue d’informations avec l’instruction SQL mise en surbrillance.](./images/view-sql/sql-dialog.png)

Sélectionnez **[!UICONTROL Exécuter SQL]** pour ouvrir l’éditeur de requêtes avec la requête prérenseignée.

![Une boîte de dialogue d’informations avec [!UICONTROL Exécuter SQL] mise en surbrillance.](./images/view-sql/run-sql.png)

## Modifier le SQL existant {#edit-sql}

L’éditeur de requêtes s’affiche. Vous pouvez désormais modifier l’instruction et interroger les données de votre plateforme de manière à mieux répondre à vos besoins en matière de rapports. Enregistrez votre nouveau modèle de requête avec le nom approprié.

![L’éditeur de requêtes avec l’insight SQL choisie préremplie.](./images/view-sql/edit-sql.png)

## Étapes suivantes

Après avoir lu ce document, vous comprenez désormais comment accéder au SQL pour obtenir des informations dans les tableaux de bord standard ou dans un tableau de bord défini par l’utilisateur. Si vous ne l’avez pas déjà fait, nous vous recommandons de lire le [document de modèle de données Real-Time Customer Data Platform Insights](./data-models/cdp-insights-data-model-b2c.md). Ce document contient des informations sur la personnalisation des modèles SQL pour les rapports Real-Time CDP adaptés à vos besoins marketing et IPC.
