---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;identité;champ;
solution: Experience Platform
title: Définition des champs d’identité dans l’interface utilisateur
description: Découvrez comment définir un champ d’identité dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---

# Définition des champs d’identité dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ d’identité représente un champ qui peut être utilisé pour identifier une personne individuelle liée à un événement d’enregistrement ou de série temporelle. Ce document explique comment définir un champ d’identité dans l’interface utilisateur de Adobe Experience Platform.

## Conditions préalables

Les champs d’identité sont un composant essentiel de la manière dont les graphiques d’identités client sont créés dans Platform, ce qui affecte finalement la manière dont Real-time Customer Profile fusionne des fragments de données disparates pour obtenir une vue d’ensemble complète du client. Avant de définir des champs d’identité dans vos schémas, reportez-vous à la documentation suivante pour en savoir plus sur les services clés et les concepts liés aux champs d’identité :

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
   * [Espaces de noms d’identité](../../../identity-service/namespaces.md) : Les espaces de noms d’identité définissent les différents types d’informations d’identité qui peuvent être associés à une seule personne et qui sont un composant requis pour chaque champ d’identité.
* [Real-time Customer Profile](../../../profile/home.md) : tire parti des graphiques d’identités des clients pour fournir un profil client unifié basé sur des données agrégées provenant de plusieurs sources, mis à jour en temps quasi réel.

## Définition d’un champ d’identité

Lorsque vous [définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur, vous pouvez le définir comme champ d’identité en cochant la case **[!UICONTROL Identité]** dans le rail de droite.

![](../../images/ui/fields/special/identity.png)

D’autres contrôles s’affichent après avoir coché la case. Si vous souhaitez que ce champ soit l’identité Principale du schéma, cochez la case **[!UICONTROL Identité Principal]** .

>[!NOTE]
>
>Un schéma unique peut comporter de nombreux champs d’identité définis, mais ne peut comporter qu’une seule identité Principale. Tous les champs d’identité (Principaux ou non) contribuent au graphique d’identités pour un client individuel, mais Real-time Customer Profile utilise uniquement la Principale identité comme source de vérité lors de la fusion de fragments de données. Si vous souhaitez activer un schéma à utiliser dans Profile, une identité Principale doit être définie pour le schéma.

Sous **[!UICONTROL Espace de noms d’identité]**, utilisez le menu déroulant pour sélectionner l’espace de noms approprié pour le champ d’identité. Les espaces de noms standard fournis par Adobe sont répertoriés, ainsi que les espaces de noms personnalisés définis par votre organisation.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/identity-config.png)

Le canevas se met à jour pour refléter les modifications, le champ sélectionné obtenant un symbole d’empreinte digitale (![](../../images/ui/fields/special/identity-symbol.png)) pour le désigner comme identité. Dans le rail de gauche, le champ d’identité est désormais répertorié sous le nom de la classe ou du groupe de champs de schéma qui fournit le champ au schéma.

Comme tous les champs d’identité sont obligatoires par défaut, le champ est désormais répertorié sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche. Si le champ d’identité est imbriqué dans la structure du schéma, tous les champs parents sont également répertoriés selon les besoins.

![](../../images/ui/fields/special/identity-applied.png)

Si vous avez défini une identité Principale pour le schéma, vous pouvez maintenant passer à [activer le schéma pour l’utiliser dans Real-time Customer Profile](../resources/schemas.md#profile).

## Étapes suivantes

Ce guide explique comment définir un champ d’identité dans l’interface utilisateur. Lorsque les données sont ingérées à l’aide de ce schéma, les graphiques d’identités client sont mis à jour pour refléter les champs d’identité du schéma. Consultez le guide sur la [visionneuse de graphiques d’identités](../../../identity-service/ui/identity-graph-viewer.md) pour savoir comment explorer le graphique privé de votre entreprise dans l’interface utilisateur.

Consultez la présentation sur la [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans la [!DNL Schema Editor].
