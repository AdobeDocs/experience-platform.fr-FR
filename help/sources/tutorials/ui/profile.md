---
keywords: Experience Platform ; accueil ; rubriques populaires ; activer les données entrantes ; renseigner le profil ; renseigner rtcp ; profil unifié renseigné
solution: Experience Platform
title: Activer les données source entrantes pour renseigner les Profils clients dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Les données entrantes de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos données de Profil client en temps réel.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 16%

---

# Activer les données source entrantes pour renseigner les profils client

Les données entrantes de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos données [!DNL Real-time Customer Profile].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

De plus, ce didacticiel nécessite que vous ayez déjà créé et configuré un connecteur source.  Vous trouverez une liste de didacticiels pour la création de différents connecteurs dans l’interface utilisateur dans la section [présentation des connecteurs source](../../home.md).

## Renseigner vos données [!DNL Real-time Customer Profile]

Pour enrichir les profils du client, le schéma source du jeu de données de cible doit être compatible avec [!DNL Real-time Customer Profile]. Un schéma compatible répond aux critères suivants :

- Le schéma comporte au moins un attribut défini comme propriété d’identité.
- Le schéma comporte au moins une propriété d’identité définie comme identité principale.
- Il existe un mappage dans le flux de données où l&#39;identité Principale est un attribut de cible.

Dans l’espace de travail Sources, cliquez sur l’onglet **[!UICONTROL Parcourir]** pour liste vos connexions de base. Dans la liste affichée, recherchez la connexion qui contient le flux de données que vous souhaitez renseigner sur les profils. Cliquez sur le nom de la connexion pour accéder à ses détails.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

L&#39;écran **[!UICONTROL activité source]** de la connexion s&#39;affiche, affichant les jeux de données dans lesquels la connexion ingère des données source. Cliquez sur le nom du jeu de données que vous souhaitez activer pour [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

L&#39;écran **[!UICONTROL activité des ensembles de données]** s&#39;affiche. La colonne **[!UICONTROL Propriétés]** située sur le côté droit de l&#39;écran affiche les détails du jeu de données et inclut un commutateur **[!UICONTROL Profil]** et un lien vers le schéma auquel adhère le jeu de données. Cliquez sur le nom du schéma pour en vue la composition.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

L&#39;**[!UICONTROL éditeur de Schéma]** s&#39;affiche, indiquant la structure du schéma dans la trame centrale. Dans la trame, sélectionnez le champ à définir comme identité Principale. Sous l&#39;onglet **[!UICONTROL Propriétés du champ]** qui s&#39;affiche, cochez la case **[!UICONTROL Identité]**, puis **[!UICONTROL Identité Principal]**. Enfin, sélectionnez un **[!UICONTROL espace de nommage d&#39;identité]** approprié, puis cliquez sur **[!UICONTROL Appliquer]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Cliquez sur l’objet de niveau supérieur de la structure du schéma et la colonne **[!UICONTROL Propriétés du Schéma]** s’affiche. Activez le schéma pour [!DNL Profile] en basculant le commutateur **[!UICONTROL Profil]**. Cliquez sur **[!UICONTROL Enregistrer]** pour finaliser vos modifications.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Maintenant que le schéma est activé pour [!DNL Profile], revenez à l&#39;écran **[!UICONTROL activité du jeu de données]** et activez le jeu de données pour [!DNL Profile] en cliquant sur le bouton **[!UICONTROL Profil]** dans la colonne **[!UICONTROL Propriétés]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Avec le schéma et le jeu de données activés pour [!DNL Profile], les données ingérées dans ce jeu de données renseigneront également les profils client.

>[!NOTE]
>
>Les données existantes dans un jeu de données récemment activé ne sont pas consommées par [!DNL Profile].

## Étapes suivantes

En suivant ce didacticiel, vous avez activé avec succès les données entrantes pour la population [!DNL Profile]. Pour plus d’informations, voir [[!DNL Real-time Customer Profile] overview](../../../profile/home.md).
