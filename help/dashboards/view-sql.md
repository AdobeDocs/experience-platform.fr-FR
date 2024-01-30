---
title: Afficher Insight SQL
description: Affichez le code SQL derrière votre profil, audience, destination et informations personnalisées et exécutez la requête à la demande via Query Editor.
source-git-commit: be90cf38970a54431f48799bf506fb0a20ec0166
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Afficher les informations SQL

Utilisez la variable [!UICONTROL Afficher SQL] pour afficher le code SQL derrière votre profil, audience, destination et informations personnalisées et exécuter la requête à la demande via l’éditeur de requêtes. Tirer parti du SQL de plus de 40 insights existants pour créer de nouvelles requêtes qui obtiennent des insights uniques à partir des données de Platform en fonction des besoins de votre entreprise.

## Accès à la présentation du tableau de bord {#navigate-to-overview}

Pour ouvrir le tableau de bord de votre choix, sélectionnez l’une des options suivantes : **[!UICONTROL Profils]**, **[!UICONTROL Audiences]**, ou **[!UICONTROL Destinations]** dans le volet de navigation de gauche. Sélection suivante **[!UICONTROL Présentation]** dans les options de l’onglet si l’espace de travail n’apparaît pas automatiquement.

Vous pouvez également sélectionner **[!UICONTROL Tableaux de bord]** dans le volet de navigation de gauche, suivi du nom de votre tableau de bord personnalisé. L’aperçu de votre tableau de bord défini par l’utilisateur s’affiche.

![L’interface utilisateur Experience Platform avec [!UICONTROL Profils], [!UICONTROL Audiences], [!UICONTROL Destinations], et [!UICONTROL Tableaux de bord] surlignée.](./images/view-sql/dashboard-navigation.png)

## Bascule de l’affichage SQL {#toggle}

Un bouton d’activation/désactivation est disponible dans la vue d’ensemble des tableaux de bord Profil, Audience, Destination et définis par l’utilisateur pour activer ou désactiver la fonctionnalité.

>[!NOTE]
>
>Si vous activez la variable [!UICONTROL Afficher SQL] vous ne pouvez pas modifier les filtres globaux et au niveau du widget tant que vous n’avez pas désactivé la fonction.

![La variable [!UICONTROL Afficher SQL] bascule en surbrillance.](./images/view-sql/view-sql-toggle.png)

Activation du bouton bascule à afficher [!UICONTROL Afficher SQL] texte sur chaque insight individuelle.

![Un aperçu avec [!UICONTROL Afficher SQL] surlignée.](./images/view-sql/insight-view-sql.png)

Sélectionner **[!UICONTROL Afficher SQL]** pour ouvrir une boîte de dialogue contenant le code SQL du widget.

## Boîte de dialogue SQL {#sql-dialog}

Une boîte de dialogue s’affiche et contient le titre de l’insight et du code SQL qui la génère.

>[!TIP]
>
>Vous pouvez copier l’intégralité de l’instruction SQL dans le presse-papiers en cliquant sur l’icône de copie (![Icône Copier.](./images/view-sql/copy-icon.png)) en haut à droite de la boîte de dialogue.

![Une boîte de dialogue d’informations avec l’instruction SQL mise en surbrillance.](./images/view-sql/sql-dialog.png)

Sélectionner **[!UICONTROL Exécuter SQL]** pour ouvrir l’éditeur de requêtes avec la requête est prérenseigné.

![Boîte de dialogue d’informations [!UICONTROL Exécuter SQL] surlignée.](./images/view-sql/run-sql.png)

## Modifier le SQL existant {#edit-sql}

L’éditeur de requêtes s’affiche. Vous pouvez désormais modifier l’instruction et interroger les données de votre plateforme de manière à mieux répondre à vos besoins en matière de rapports. Enregistrez votre nouveau modèle de requête avec le nom approprié.

![L’éditeur de requêtes avec le code SQL d’informations sélectionné est prérempli.](./images/view-sql/edit-sql.png)

## Étapes suivantes

Après avoir lu ce document, vous comprenez désormais comment accéder au SQL pour obtenir des informations dans les tableaux de bord standard ou dans un tableau de bord défini par l’utilisateur. Si vous ne l’avez pas déjà fait, il est recommandé de lire la [Document de modèle de données Real-time Customer Data Platform Insights](./cdp-insights-data-model.md). Ce document contient des informations sur la personnalisation des modèles SQL pour les rapports Real-Time CDP adaptés à vos besoins marketing et IPC.
