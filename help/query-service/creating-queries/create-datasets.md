---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Générer des jeux de données à partir de résultats '
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Générer des jeux de données à partir de résultats 

La puissance réelle du service de  est révélée lorsque les  sont utilisés pour générer des jeux de données dans le lac de données à utiliser comme entrée dans un plus grand nombre d’applications ou dans d’autres services, tels que Data Science Workspace, Real-time Customerou le service de l’espace de travail de l’utilisateur en temps réel.

Le service  permet la création de jeux de données à partir de l’interface utilisateur. Procédez comme suit :

1. Ecrivez votre  à l’aide d’un client connecté et validez la sortie.
2. Connectez-vous à l’interface utilisateur de la plate-forme et accédez au  de.
3. Recherchez votre  dans le  et passez la souris sur la ligne.
4. Cliquez sur **Créer un jeu de données**. ![Image](../images/queries/create-datasets/click-create-dataset.png)
5. Entrez un nom de jeu de données, précédé de votre ID LDAP (il n&#39;est pas nécessaire que ce soit unique ou que SQL-safe) ; le système génère un &quot;nom de table&quot; basé sur le nom donné ici).
6. Entrez une description de jeu de données et cliquez sur **Exécuter le**.![Image](../images/queries/create-datasets/run-query.png)
7. Observez le  terminé, puis accédez à la page du de jeux de données pour voir le jeu de données que vous venez de créer.

Une fois un jeu de données créé, il est accessible comme tout autre jeu de données dans le lac de données et utilisé pour divers cas d’utilisation.

>[!NOTE] Dans une implémentation en direct, vous devez appliquer des étiquettes de gouvernance des données une fois le jeu de données créé.

## Générer des jeux de données avec un de modèle de données d’expérience prédéfini 

Pour générer un jeu de données avec un  de modèle de données d’expérience (XDM) prédéfini, vous devez utiliser la syntaxe SQL. Pour plus d&#39;informations sur la syntaxe à utiliser, lisez le guide [de syntaxe](../sql/syntax.md#create-table-as-select)SQL.

## Jeu de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un ad hoc qui correspond à la structure des données de sortie telle que définie dans l’instruction SQL. Certains services en aval nécessitent des jeux de données avec des  de modèle de données d’expérience (XDM) spécifiques. Vérifiez les exigences de formatage des données pour les services en aval avant d’écrire votre .