---
keywords: Experience Platform;home;popular topics;troubleshooting;access control
solution: Experience Platform
title: Guide de dépannage du contrôle d’accès
topic: troubleshooting guide
description: Ce document répond aux questions fréquentes sur le contrôle d’accès dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 71%

---


# Guide de dépannage du contrôle d’accès

Ce document répond aux questions fréquentes sur le contrôle d’accès dans Adobe Experience Platform. For questions and troubleshooting related to other [!DNL Platform] services, please refer to the [Experience Platform troubleshooting guide](../landing/troubleshooting.md).

[!DNL Experience Platform] exploite les profils de produit dans [Adobe Admin Console](http://adminconsole.adobe.com) pour fournir des **contrôles d’accès** en fonction du rôle, en liant les utilisateurs à des autorisations et des environnements de test.  Pour plus d’informations, consultez la [présentation du contrôle d’accès](home.md).

## Où puis-je trouver mes autorisations d’accès actuelles ?

Si vous êtes un administrateur système, un administrateur de produit ou un administrateur de profils de produit pour votre organisation IMS, vous pouvez afficher le profil de produit qui vous a été attribué et les autorisations qu’il accorde dans Adobe Admin Console. Consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md) pour obtenir des instructions sur la navigation dans afin d’afficher les autorisations d’un profil de produit.[!DNL Admin Console]

Si vous n’êtes pas un administrateur, vous pouvez tout de même consulter vos autorisations d’accès actuelles en envoyant une requête sur le point de terminaison `/acl/effective-policies` dans l’API Access Control. Pour plus d’informations, consultez la section « Affichage des stratégies efficaces » du [guide de développement du contrôle d’accès](./api/effective-policies.md).

## Some features in the [!DNL Platform] UI are not available. Comment les autorisations contrôlent-elles l’accès à ces fonctionnalités ?

If you do not have access permissions for a particular [!DNL Platform] feature, that feature will be hidden or greyed-out in the [!DNL Experience Platform] UI. For example, in order to view the &quot;[!UICONTROL Profiles]&quot; tab, you must have either the &quot;[!UICONTROL View Profiles]&quot; or &quot;[!UICONTROL Manage Profiles]&quot; permissions. Contact your administrator if you require additional permissions for [!DNL Experience Platform] capabilities.

## Comment les autorisations sont-elles regroupées et quel groupe contient l’autorisation que je souhaite utiliser ?

Les autorisations sont regroupées et classées en fonction des [!DNL Platform] capacités auxquelles elles s’appliquent (par exemple [!DNL Data Management] et [!DNL Profile Management]). Pour obtenir une liste complète des autorisations disponibles et des groupes auxquels elles appartiennent, consultez la [section des autorisations](home.md#permissions) dans la présentation du contrôle d’accès.

Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez la [présentation du contrôle d’accès](home.md).