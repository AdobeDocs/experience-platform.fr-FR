---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Activer les données source entrantes pour renseigner le client '
topic: overview
translation-type: tm+mt
source-git-commit: d6d2faf3d5eabcd8e948d3717fd8f8df4b9cb85a

---


# Activer les données source entrantes pour renseigner le client 

Les données entrantes de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos données de client en temps réel.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
- [](../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

De plus, ce didacticiel nécessite que vous ayez déjà créé et configuré un connecteur source.  Un de didacticiels pour la création de différents connecteurs dans l’interface utilisateur se trouve dans la présentation [des connecteurs](../../home.md)source.

## Renseigner vos données de client en temps réel 

Afin d’enrichir les  du client, lejeu de données source du jeu de données doit être compatible avec le du client en temps réel. Un  compatible satisfait aux exigences suivantes :

- Le  comporte au moins un attribut spécifié comme propriété d’identité.
- La propriété d’identité du est définie en tant qu’identité principale.
- Il existe un mappage au sein du flux de données dans lequel l’identité principale est un attribut .

Dans l’espace de travail Sources, cliquez sur l’onglet **Parcourir** pour vos connexions de base. Dans le  affiché, recherchez la connexion qui contient le flux de données que vous souhaitez renseigner sur le. Cliquez sur le nom de la connexion pour accéder à ses détails.

![](../../images/tutorials/dataflow/cloud-storage/browse.png)

L’écran *Source* de la connexion s’affiche, affichant les jeux de données dans lesquels la connexion imbrique des données source. Cliquez sur le nom du jeu de données que vous souhaitez activer pour les  de.

![](../../images/tutorials/dataflow/cloud-storage/dataset-dataflow.png)

L’écran  de de *données* s’affiche. La colonne *Propriétés* sur le côté droit de l&#39;écran affiche les détails du jeu de données et inclut un commutateur de **** et un lien vers le auquel le jeu de données adhère. Cliquez sur le nom du  pour  sa composition.

![](../../images/tutorials/dataflow/cloud-storage/select-dataset-schema.png)

L’éditeur *de* s’affiche, indiquant la structure du  de dans la trame centrale. Dans le canevas, sélectionnez le champ à définir comme identité principale. Sous l’onglet Propriétés *du* champ qui s’affiche, cochez la case **Identité** , puis identité **** principale. Enfin, sélectionnez un **d’identité  approprié**, puis cliquez sur **Appliquer**.

![](../../images/tutorials/dataflow/cloud-storage/set-schema-identity.png)

Cliquez sur l’objet de niveau supérieur de la structure de  de et la colonne des propriétés *de  de* s’affiche. Activez le  pour les  de en activant le commutateur de **** -. Cliquez sur **Enregistrer** pour finaliser vos modifications.

![](../../images/tutorials/dataflow/cloud-storage/enable-profile.png)

Maintenant que le  de est activé pour les  de, revenez à l’écran de *jeu de données* et activez le jeu de données pour les **en cliquant sur la bascule de la**** Propriétés.

![](../../images/tutorials/dataflow/cloud-storage/enable-dataset-profile.png)

Avec le  et le jeu de données activés pour les  de, les données imbriquées dans ce jeu de données renseigneront désormais également les  clients.

>[!NOTE] Les données existantes dans un jeu de données récemment activé ne sont pas consommées par le 

## Étapes suivantes

En suivant ce didacticiel, vous avez activé avec succès les données d’entrée pour la population de . Pour plus d’informations, reportez-vous à la présentation [du de clients en temps](../../../profile/home.md)réel.