---
keywords: Experience Platform;accueil;rubriques populaires;activer les données entrantes;remplir le profil;renseigner rtcp;profil unifié renseigné
solution: Experience Platform
title: Activation des données source entrantes pour remplir les profils client dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et remplir vos données Real-time Customer Profile.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 16%

---

# Activation des données source entrantes pour renseigner les profils client

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel](../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

En outre, ce tutoriel nécessite que vous ayez déjà créé et configuré un connecteur source.  Vous trouverez une liste des tutoriels pour la création de différents connecteurs dans l’interface utilisateur dans la [présentation des connecteurs source](../../home.md).

## Renseignez vos données [!DNL Real-time Customer Profile]

Pour enrichir les profils clients, le schéma source du jeu de données cible doit être compatible avec l’utilisation dans [!DNL Real-time Customer Profile]. Un schéma compatible répond aux critères suivants :

- Le schéma comporte au moins un attribut défini comme propriété d’identité.
- Le schéma comporte au moins une propriété d’identité définie comme identité principale.
- Il existe un mappage dans le flux de données, dans lequel l’identité Principale est un attribut cible.

Dans l’espace de travail Sources, cliquez sur l’onglet **[!UICONTROL Parcourir]** pour répertorier vos connexions de base. Dans la liste affichée, recherchez la connexion qui contient le flux de données que vous souhaitez renseigner dans les profils. Cliquez sur le nom de la connexion pour accéder à ses détails.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

L’écran **[!UICONTROL Activité source]** de la connexion s’affiche, affichant les jeux de données dans lesquels la connexion ingère des données source. Cliquez sur le nom du jeu de données que vous souhaitez activer pour [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

L’écran **[!UICONTROL Activité du jeu de données]** s’affiche. La colonne **[!UICONTROL Propriétés]** sur le côté droit de l’écran affiche les détails du jeu de données et inclut un commutateur **[!UICONTROL Profile]** et un lien vers le schéma auquel le jeu de données adhère. Cliquez sur le nom du schéma pour en visualiser la composition.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

L’ **[!UICONTROL éditeur de schémas]** s’affiche, indiquant la structure du schéma dans la zone de travail centrale. Dans la zone de travail, sélectionnez le champ à définir comme identité Principale. Sous l’onglet **[!UICONTROL Propriétés du champ]** qui s’affiche, cochez la case **[!UICONTROL Identité]**, puis **[!UICONTROL Identité Principal]**. Enfin, sélectionnez un **[!UICONTROL espace de noms d’identité]** approprié, puis cliquez sur **[!UICONTROL Appliquer]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Cliquez sur l’objet de niveau supérieur de la structure du schéma et la colonne **[!UICONTROL Propriétés du schéma]** apparaît. Activez le schéma pour [!DNL Profile] en activant le commutateur **[!UICONTROL Profil]**. Cliquez sur **[!UICONTROL Enregistrer]** pour finaliser vos modifications.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Maintenant que le schéma est activé pour [!DNL Profile], revenez à l’écran **[!UICONTROL Activité du jeu de données]** et activez le jeu de données pour [!DNL Profile] en cliquant sur le bouton d’activation **[!UICONTROL Profil]** dans la colonne **[!UICONTROL Propriétés]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Avec le schéma et le jeu de données activés pour [!DNL Profile], les données ingérées dans ce jeu de données renseigneront désormais également les profils client.

>[!NOTE]
>
>Les données existantes dans un jeu de données récemment activé ne sont pas consommées par [!DNL Profile].

## Étapes suivantes

En suivant ce tutoriel, vous avez correctement activé les données entrantes pour la population [!DNL Profile]. Pour plus d’informations, consultez la [[!DNL Real-time Customer Profile] présentation](../../../profile/home.md).
