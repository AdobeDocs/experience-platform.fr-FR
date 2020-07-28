---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Activer les données source entrantes pour renseigner les profils client
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 22%

---


# Activer les données source entrantes pour renseigner les profils client

Les données entrantes provenant de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos [!DNL Real-time Customer Profile] données.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Système de modèle de données d’expérience (XDM)](../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Real-time Customer Profile](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

De plus, ce didacticiel nécessite que vous ayez déjà créé et configuré un connecteur source.  Vous trouverez une liste de didacticiels pour la création de différents connecteurs dans l’interface utilisateur dans l’aperçu [des connecteurs](../../home.md)source.

## Renseigner vos [!DNL Real-time Customer Profile] données

Pour enrichir les profils du client, le schéma source du jeu de données de cible doit être compatible pour une utilisation dans [!DNL Real-time Customer Profile]. Un schéma compatible répond aux critères suivants :

- Le schéma comporte au moins un attribut défini comme propriété d’identité.
- Le schéma comporte au moins une propriété d’identité définie comme identité principale.
- Il existe un mappage dans le flux de données où l&#39;identité principale est un attribut de cible.

Dans l’espace de travail Sources, cliquez sur l’onglet **[!UICONTROL Parcourir]** pour liste vos connexions de base. Dans la liste affichée, recherchez la connexion qui contient le flux de données que vous souhaitez renseigner sur les profils. Cliquez sur le nom de la connexion pour accéder à ses détails.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

L&#39;écran activité ** source de la connexion s&#39;affiche, affichant les jeux de données dans lesquels la connexion imbrique des données source. Cliquez sur le nom du jeu de données que vous souhaitez activer [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

L’écran activité *[!UICONTROL des]* jeux de données s’affiche. La colonne *[!UICONTROL Propriétés]* située à droite de l&#39;écran affiche les détails du jeu de données et inclut un commutateur de **[!UICONTROL Profil]** et un lien vers le schéma auquel adhère le jeu de données. Cliquez sur le nom du schéma pour en vue la composition.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

L’éditeur *[!UICONTROL de]* Schéma s’affiche, indiquant la structure du schéma dans la trame centrale. Dans la trame, sélectionnez le champ à définir comme identité principale. Sous l’onglet Propriétés *[!UICONTROL du]* champ qui s’affiche, cochez la case **[!UICONTROL Identité]** , puis l’identité **[!UICONTROL du]** Principal. Enfin, sélectionnez un espace de nommage **[!UICONTROL d&#39;]** identité approprié, puis cliquez sur **[!UICONTROL Appliquer]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Cliquez sur l’objet de niveau supérieur de la structure du schéma et la colonne des propriétés *[!UICONTROL du]* Schéma s’affiche. Activez le schéma pour [!DNL Profile] en basculant le commutateur **[!UICONTROL Profil]** . Cliquez sur **[!UICONTROL Enregistrer]** pour finaliser vos modifications.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Maintenant que le schéma est activé pour [!DNL Profile], revenez à l&#39;écran activité *[!UICONTROL du jeu de]* données et activez le jeu de données pour [!DNL Profile] en cliquant sur l&#39;option **[!UICONTROL Profil]** de la colonne *Propriétés.*

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Avec le schéma et le jeu de données activés pour [!DNL Profile], les données ingérées dans ce jeu de données renseigneront également les profils client.

>[!NOTE]
>
>Les données existantes dans un jeu de données récemment activé ne sont pas utilisées par [!DNL Profile]

## Étapes suivantes

En suivant ce didacticiel, vous avez activé avec succès les données entrantes pour [!DNL Profile] la population. Pour plus d’informations, consultez la [présentation de Real-time Customer Profile](../../../profile/home.md).