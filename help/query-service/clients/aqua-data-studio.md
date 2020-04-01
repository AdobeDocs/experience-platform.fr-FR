---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connexion à Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Connexion à Aqua Data Studio

Ce décrit les étapes à suivre pour connecter Aqua Data Studio au service de Adobe Experience Platform.

Après avoir installé Aqua Data Studio, vous devez d’abord enregistrer le serveur. Dans le menu principal, cliquez sur **Serveur**, puis sur **Enregistrer le serveur**.

![](../images/clients/aqua-data-studio/register-server.png)

La boîte de dialogue *Enregistrer le serveur* s’affiche. Sous l&#39;onglet *Général* , sélectionnez **PostgreSQL** dans le  de gauche. Dans la boîte de dialogue qui s’affiche, fournissez les détails suivants pour les paramètres du serveur.

- **Nom**: Nom de votre connexion.
- **Nom de connexion et mot de passe**: Informations de connexion qui seront utilisées. Le nom d&#39;utilisateur prend la forme de `ORG_ID@AdobeOrg`.
- **Hôte et port**: Point de terminaison hôte et son port pour le service de .
- **Base de données :** Base de données qui sera utilisée.

>[!NOTE] Pour plus d’informations sur la recherche de vos informations d’identification de connexion, de votre hôte, du port et du nom de la base de données, consultez la page [d’identification de la plateforme](https://platform.adobe.com/query/configuration). Pour rechercher vos informations d’identification, connectez-vous à Platform, cliquez sur ****, puis sur **Credentials**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **Driver** tab. Sous *Paramètres*, définissez la valeur sur `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Après avoir saisi les détails de votre connexion, cliquez sur **Tester la connexion** pour vous assurer que vos informations d’identification fonctionnent correctement. Si votre connexion réussit, cliquez sur **Enregistrer** pour enregistrer votre serveur. La connexion s’affiche sur le ** lors de l’enregistrement réussi, confirmant que vous pouvez désormais vous connecter au serveur et  ses objets .

## Étapes suivantes

Maintenant que vous êtes connecté à  Service, vous pouvez utiliser l’analyseur *de  de* d’Aqua Data Studio pour exécuter et modifier des instructions SQL. Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des  de, veuillez lire le [guide](../creating-queries/creating-queries.md)de  de en cours d&#39;exécution.