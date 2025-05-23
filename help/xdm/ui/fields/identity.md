---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;interface utilisateur;espace de travail;identité;champ;
solution: Experience Platform
title: Définir des champs d’identité dans l’interface utilisateur
description: Découvrez comment définir un champ d’identité dans l’interface utilisateur Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 3570197ca6cff95368b4facb034386e793033fe2
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 15%

---

# Définir des champs d’identité dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ d’identité représente un champ qui peut être utilisé pour identifier une personne individuelle liée à un enregistrement ou à un événement de série temporelle. Ce document explique comment définir un champ d’identité dans l’interface utilisateur de Adobe Experience Platform.

## Conditions préalables

Les champs d’identité sont un composant essentiel dans la construction des graphiques d’identités client dans Experience Platform, ce qui affecte finalement la manière dont le profil client en temps réel fusionne des fragments de données disparates pour obtenir une vue complète du client. Avant de définir des champs d’identité dans vos schémas, reportez-vous à la documentation suivante pour en savoir plus sur les services et concepts clés liés aux champs d’identité :

* [Service d’identités d’Adobe Experience Platform](../../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
   * [Espaces de noms d’identité](../../../identity-service/features/namespaces.md) : définissent les différents types d’informations d’identité qui peuvent être associés à une seule personne et constituent un composant obligatoire pour chaque champ d’identité.
* [Real-Time Customer Profile](../../../profile/home.md) : utilise des graphiques d’identités client pour fournir un profil de consommateur unifié basé sur des données agrégées issues de plusieurs sources et mis à jour pratiquement en temps réel.

## Définir un champ d’identité {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Restrictions de l&#39;identité principale"
>abstract="Ce schéma utilise un groupe de champs destiné à être utilisé dans une connexion source spécifique. La connexion nécessite l&#39;utilisation d&#39;identityMap comme identité principale et l&#39;a défini automatiquement."

Lors de la [définition d’un nouveau champ](./overview.md#define) dans l’interface utilisateur, vous pouvez le définir en tant que champ d’identité en cochant la case **[!UICONTROL Identité]** dans le rail de droite.

![](../../images/ui/fields/special/identity.png)

Des commandes supplémentaires s’affichent après avoir coché la case. Si vous souhaitez que ce champ soit l&#39;identité principale du schéma, cochez la case **[!UICONTROL Identité du Principal]**.

>[!NOTE]
>
>Plusieurs champs d’identité peuvent être définis pour un même schéma, mais une seule identité principale est autorisée. Tous les champs d’identité (principaux ou autres) contribuent au graphique d’identités d’un client individuel, mais le profil client en temps réel utilise uniquement l’identité principale comme source de vérité lors de la fusion de fragments de données. Si vous souhaitez activer un schéma pour l’utiliser dans Profile, une identité principale doit être définie pour ce schéma.

Sous **[!UICONTROL Espace de noms d’identité]**, utilisez le menu déroulant pour sélectionner l’espace de noms approprié pour le champ d’identité. Les espaces de noms standard fournis par Adobe sont répertoriés, ainsi que les espaces de noms personnalisés définis par votre organisation.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

>[!IMPORTANT]
>
>Une fois qu’un schéma peut être utilisé dans le profil client en temps réel et que les données ont été ingérées, **vous ne pouvez pas modifier le champ de l’identité principale**. Toute tentative de ce type entraînera une erreur de validation. Si vous devez utiliser une autre identité principale, vous devez créer un nouveau schéma ainsi qu’un nouveau jeu de données avec la configuration d’identité mise à jour.

![](../../images/ui/fields/special/identity-config.png)

La zone de travail se met à jour pour refléter les modifications, le champ sélectionné obtenant un symbole d’empreinte digitale (![](/help/images/icons/identity-service.png)) pour le désigner en tant qu’identité. Dans le rail de gauche, le champ d’identité est désormais répertorié sous le nom de la classe ou du groupe de champs de schéma qui fournit le champ au schéma.

Si le champ a également été défini comme identité principale, il sera également répertorié sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche. Si le champ d’identité est imbriqué dans la structure du schéma, tous les champs parents sont également répertoriés selon les besoins.

![](../../images/ui/fields/special/identity-applied.png)

Si vous avez défini une identité principale pour le schéma, vous pouvez maintenant passer à [activer le schéma à utiliser dans le profil client en temps réel](../resources/schemas.md#profile).

## Étapes suivantes

Ce guide explique comment définir un champ d’identité dans l’interface utilisateur. Comme les données sont ingérées à l’aide de ce schéma, vos graphiques d’identités client sont mis à jour pour refléter les champs d’identité du schéma. Consultez le guide sur la [visionneuse de graphiques d’identité](../../../identity-service/features/identity-graph-viewer.md) pour savoir comment explorer le graphique privé de votre organisation dans l’interface utilisateur.

Consultez la présentation sur la [définition de champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans l’[!DNL Schema Editor].
