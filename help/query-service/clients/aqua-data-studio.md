---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connexion à Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Connexion à Aqua Data Studio

Ce document décrit les étapes nécessaires pour connecter Aqua Data Studio à Adobe Experience Platform Requête Service.

Après avoir installé Aqua Data Studio, vous devez d’abord enregistrer le serveur. Dans le menu principal, cliquez sur **Serveur**, puis sur **Enregistrer le serveur**.

![](../images/clients/aqua-data-studio/register-server.png)

La boîte de dialogue *Enregistrer le serveur* s&#39;affiche. Sous l&#39;onglet *Général* , sélectionnez **PostgreSQL** dans la liste située à gauche. Dans la boîte de dialogue qui s’affiche, fournissez les détails suivants pour les paramètres du serveur.

- **Nom**: Nom de votre connexion.
- **Nom de connexion et mot de passe**: Identifiants de connexion qui seront utilisés. Le nom d&#39;utilisateur prend la forme de `ORG_ID@AdobeOrg`.
- **Hôte et port**: Point de terminaison hôte et son port pour Requête Service.
- **Base de données :** Base de données qui sera utilisée.

>[!NOTE] Pour plus d&#39;informations sur la recherche de vos informations d&#39;identification de connexion, de votre hôte, de votre port et de votre nom de base de données, consultez la page d&#39; [informations d&#39;identification sur la plate-forme](https://platform.adobe.com/query/configuration). Pour rechercher vos informations d’identification, connectez-vous à la plateforme, cliquez sur **Requêtes**, puis sur **Informations d’identification**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **Driver** tab. Sous *Paramètres*, définissez la valeur sur `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Après avoir saisi les détails de votre connexion, cliquez sur **Tester la connexion** pour vérifier que vos informations d’identification fonctionnent correctement. Si votre connexion réussit, cliquez sur **Enregistrer** pour enregistrer votre serveur. La connexion s’affiche sur le *Tableau de bord* lors d’une inscription réussie, confirmant que vous pouvez désormais vous connecter au serveur et vue ses objets schéma.

## Étapes suivantes

Maintenant que vous êtes connecté à Requête Service, vous pouvez utiliser l&#39;Analyseur *de* Requête d&#39;Aqua Data Studio pour exécuter et modifier des instructions SQL. Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des requêtes, veuillez lire le guide [des requêtes](../creating-queries/creating-queries.md)en cours d&#39;exécution.