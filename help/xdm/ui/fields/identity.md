---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;identity;field;
solution: Experience Platform
title: Définition des champs d’identité dans l’interface utilisateur
description: Découvrez comment définir un champ d'identité dans l'interface utilisateur de l'Experience Platform.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---

# Définition des champs d&#39;identité dans l&#39;interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ d’identité représente un champ qui peut être utilisé pour identifier une personne liée à un enregistrement ou un événement de séries chronologiques. Ce document explique comment définir un champ d’identité dans l’interface utilisateur de Adobe Experience Platform.

## Conditions préalables  

Les champs d’identité constituent un composant essentiel de la manière dont les graphiques d’identité du client sont créés dans Platform, ce qui affecte en fin de compte la manière dont le Profil client en temps réel fusionne des fragments de données disparates afin d’obtenir une vue complète du client. Avant de définir des champs d&#39;identité dans vos schémas, reportez-vous à la documentation suivante pour en savoir plus sur les services et concepts clés liés aux champs d&#39;identité :

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
   * [Espaces de nommage](../../../identity-service/namespaces.md) d&#39;identité : Les espaces de nommage d&#39;identité définissent les différents types d&#39;informations d&#39;identité qui peuvent se rapporter à une seule personne et constituent un composant obligatoire pour chaque champ d&#39;identité.
* [Profil](../../../profile/home.md) client en temps réel : Exploite les graphiques d’identité des clients pour fournir un profil unifié du consommateur, basé sur des données agrégées provenant de plusieurs sources, mis à jour en temps quasi réel.

## Définir un champ d&#39;identité

Lorsque [vous définissez un nouveau champ](./overview.md#define) dans l&#39;interface utilisateur, vous pouvez le définir comme champ d&#39;identité en cochant la case **[!UICONTROL Identité]** dans le rail de droite.

![](../../images/ui/fields/special/identity.png)

D’autres commandes s’affichent après avoir coché la case. Si vous souhaitez que ce champ soit l&#39;identité Principale du schéma, cochez la case **[!UICONTROL identité Principal]**.

>[!NOTE]
>
>Un schéma unique peut avoir plusieurs champs d&#39;identité définis, mais ne peut avoir qu&#39;une seule identité Principale. Tous les champs d’identité (Principaux ou non) contribuent au graphique d’identité d’un client individuel, mais le Profil du client en temps réel utilise uniquement l’identité Principale comme source de vérité lors de la fusion de fragments de données. Si vous souhaitez activer un schéma pour une utilisation dans le Profil, le schéma doit avoir une Principale identité définie.

Sous **[!UICONTROL espace de nommage d&#39;identité]**, utilisez le menu déroulant pour sélectionner l&#39;espace de nommage approprié au champ d&#39;identité. Les espaces de nommage standard fournis par l’Adobe sont répertoriés, ainsi que les espaces de nommage personnalisés définis par votre organisation.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/identity-config.png)

Le canevas se met à jour pour refléter les modifications, le champ sélectionné gagnant un symbole d&#39;empreinte digitale (![](../../images/ui/fields/special/identity-symbol.png)) pour le désigner comme une identité. Dans le rail de gauche, le champ d&#39;identité est désormais répertorié sous le nom de la classe ou du groupe de champs de schéma qui fournit le champ au schéma.

Comme tous les champs d&#39;identité sont obligatoires par défaut, le champ est désormais répertorié sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche. Si le champ d&#39;identité est imbriqué dans la structure du schéma, tous les champs parents sont également répertoriés comme requis.

![](../../images/ui/fields/special/identity-applied.png)

Si vous avez défini une identité Principale pour le schéma, vous pouvez maintenant passer à [activer le schéma pour l&#39;utiliser dans le Profil client en temps réel](../resources/schemas.md#profile).

## Étapes suivantes

Ce guide explique comment définir un champ d&#39;identité dans l&#39;interface utilisateur. À mesure que les données sont ingérées à l’aide de ce schéma, les graphiques d’identité du client sont mis à jour pour refléter les champs d’identité du schéma. Consultez le guide de la [visionneuse de graphiques d&#39;identité](../../../identity-service/ui/identity-graph-viewer.md) pour savoir comment explorer le graphique privé de votre entreprise dans l&#39;interface utilisateur.

Consultez l&#39;aperçu sur [la définition des champs dans l&#39;interface utilisateur](./overview.md#special) pour savoir comment définir d&#39;autres types de champs XDM dans [!DNL Schema Editor].
