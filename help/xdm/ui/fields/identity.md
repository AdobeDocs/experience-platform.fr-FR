---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;identité;champ;
solution: Experience Platform
title: Définition des champs d’identité dans l’interface utilisateur
description: Découvrez comment définir un champ d’identité dans l’interface utilisateur de l’Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: d1b571fe72208cf2f2ae339273f05cc38dda9845
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 16%

---

# Définir des champs d’identité dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), un champ d’identité représente un champ qui peut être utilisé pour identifier une personne individuelle liée à un événement d’enregistrement ou de série temporelle. Ce document explique comment définir un champ d’identité dans l’interface utilisateur de Adobe Experience Platform.

## Conditions préalables

Les champs d’identité sont un composant essentiel de la manière dont les graphiques d’identités client sont créés dans Platform, ce qui affecte finalement la manière dont Real-Time Customer Profile fusionne des fragments de données disparates pour obtenir une vue d’ensemble complète du client. Avant de définir des champs d’identité dans vos schémas, reportez-vous à la documentation suivante pour en savoir plus sur les services clés et les concepts liés aux champs d’identité :

* [Service d’identités d’Adobe Experience Platform](../../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
   * [Espaces de noms d’identité](../../../identity-service/features/namespaces.md) : définissent les différents types d’informations d’identité qui peuvent être associés à une seule personne et constituent un composant obligatoire pour chaque champ d’identité.
* [ Real-Time Customer Profile ](../../../profile/home.md) : exploite des graphiques d’identités client pour fournir un profil client unifié basé sur des données agrégées provenant de plusieurs sources, mis à jour en temps quasi réel.

## Définir un champ d’identité {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Restrictions de l&#39;identité principale"
>abstract="Ce schéma utilise un groupe de champs destiné à être utilisé dans une connexion source spécifique. La connexion nécessite l&#39;utilisation d&#39;identityMap comme identité principale et l&#39;a défini automatiquement."

Lorsque [vous définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur, vous pouvez le définir comme champ d’identité en cochant la case **[!UICONTROL Identité]** dans le rail de droite.

![](../../images/ui/fields/special/identity.png)

D’autres contrôles s’affichent après avoir coché la case. Si vous souhaitez que ce champ soit l’identité principale du schéma, cochez la case **[!UICONTROL Identité par Principal]** .

>[!NOTE]
>
>Un schéma unique peut comporter de nombreux champs d’identité définis, mais ne peut comporter qu’une seule identité principale. Tous les champs d’identité (principaux ou autres) contribuent au graphique d’identités pour un client individuel, mais Real-Time Customer Profile utilise uniquement l’identité principale comme source de vérité lors de la fusion de fragments de données. Si vous souhaitez activer un schéma à utiliser dans Profile, une identité principale doit être définie pour le schéma.

Sous **[!UICONTROL Espace de noms d’identité]**, utilisez le menu déroulant pour sélectionner l’espace de noms approprié pour le champ d’identité. Les espaces de noms standard fournis par Adobe sont répertoriés, ainsi que les espaces de noms personnalisés définis par votre organisation.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer la modification au schéma.

![](../../images/ui/fields/special/identity-config.png)

Le canevas se met à jour pour refléter les modifications, le champ sélectionné gagnant un symbole d’empreinte digitale (![](/help/images/icons/identity-service.png)) pour le désigner comme identité. Dans le rail de gauche, le champ d’identité est désormais répertorié sous le nom de la classe ou du groupe de champs de schéma qui fournit le champ au schéma.

Si le champ a également été défini comme identité principale, il sera également répertorié sous **[!UICONTROL Champs obligatoires]** dans le rail de gauche. Si le champ d’identité est imbriqué dans la structure du schéma, tous les champs parents sont également répertoriés selon les besoins.

![](../../images/ui/fields/special/identity-applied.png)

Si vous avez défini une identité principale pour le schéma, vous pouvez maintenant passer à [activer le schéma pour l’utiliser dans Real-time Customer Profile](../resources/schemas.md#profile).

## Étapes suivantes

Ce guide explique comment définir un champ d’identité dans l’interface utilisateur. Lorsque les données sont ingérées à l’aide de ce schéma, les graphiques d’identités client sont mis à jour pour refléter les champs d’identité du schéma. Consultez le guide sur la [visionneuse de graphiques d’identités](../../../identity-service/features/identity-graph-viewer.md) pour découvrir comment explorer le graphique privé de votre entreprise dans l’interface utilisateur.

Consultez la présentation de la [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champs XDM dans [!DNL Schema Editor].
