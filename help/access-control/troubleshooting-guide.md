---
keywords: Experience Platform;accueil;rubriques populaires;dépannage;contrôle dʼaccès
solution: Experience Platform
title: Guide de dépannage du contrôle dʼaccès
topic-legacy: troubleshooting guide
description: Ce document répond aux questions fréquentes sur le contrôle d’accès dans Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 79ffdf35e27d74a64ea8e25544fdeeb293b58306
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 78%

---

# Guide de dépannage du contrôle d’accès

Ce document répond aux questions fréquentes sur le contrôle d’accès dans Adobe Experience Platform. Pour les questions et le dépannage relatifs aux autres services [!DNL Platform], consultez le [guide de dépannage dʼExperience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] exploite les profils de produit dans [Adobe Admin Console](https://adminconsole.adobe.com) pour fournir des contrôles d’accès en fonction du rôle, en liant les utilisateurs à des autorisations et des environnements de test.  Pour plus d’informations, consultez la [présentation du contrôle d’accès](home.md).

## Où puis-je trouver mes autorisations d’accès actuelles ?

Si vous êtes un administrateur système, un administrateur de produit ou un administrateur de profils de produit pour votre organisation IMS, vous pouvez afficher le profil de produit qui vous a été attribué et les autorisations qu’il accorde dans Adobe Admin Console. Consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md) pour obtenir des instructions sur la navigation dans afin d’afficher les autorisations d’un profil de produit[!DNL Admin Console].

Si vous n’êtes pas un administrateur, vous pouvez tout de même consulter vos autorisations d’accès actuelles en envoyant une requête sur le point d’entrée `/acl/effective-policies` dans l’API Access Control. Pour plus d’informations, consultez la section « Affichage des stratégies efficaces » du [guide de développement du contrôle d’accès](./api/effective-policies.md).

## Certaines fonctionnalités de lʼinterface utilisateur de [!DNL Platform] ne sont pas disponibles. Comment les autorisations contrôlent-elles l’accès à ces fonctionnalités ?

Si vous ne disposez pas des autorisations dʼaccès pour une fonctionnalité de [!DNL Platform] spécifique, cette fonctionnalité sera masquée ou grisée dans lʼinterface utilisateur dʼ[!DNL Experience Platform]. Par exemple, pour afficher lʼonglet « [!UICONTROL Profils] », vous devez disposer de lʼautorisation « [!UICONTROL Affichage des profils] » ou « [!UICONTROL Gestion des profils] ». Contactez votre administrateur si vous avez besoin dʼautorisations supplémentaires pour les fonctionnalités dʼ[!DNL Experience Platform].

## Comment les autorisations sont-elles regroupées et quel groupe contient l’autorisation que je souhaite utiliser ?

Les autorisations sont regroupées et classées en fonction des fonctionnalités de [!DNL Platform] auxquelles elles sʼappliquent (par exemple [!DNL Data Management] et [!DNL Profile Management]). Pour obtenir une liste complète des autorisations disponibles et des groupes auxquels elles appartiennent, consultez la [section des autorisations](home.md#permissions) dans la présentation du contrôle d’accès.

Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez la [présentation du contrôle d’accès](home.md).

## Qu’advient-il des autorisations après la migration d’Adobe IO vers Business ID ?

Le contrôle d’accès utilise un ID utilisateur (un ID unique interne attribué à un utilisateur) pour accorder des autorisations. Lorsqu’une organisation est migrée d’Adobe ID vers Business ID, toutes les autorisations définies pour ses utilisateurs seront perdues car l’ID utilisateur change et le contrôle d’accès utilisera l’ID utilisateur nouvellement généré. Si votre entreprise est migrée vers un identifiant professionnel, contactez votre représentant d’Adobe pour migrer votre identifiant utilisateur d’Adobe ID vers un identifiant professionnel.
