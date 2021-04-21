---
keywords: Experience Platform ; accueil ; rubriques populaires ; dépannage ; contrôle d'accès
solution: Experience Platform
title: Guide de dépannage des contrôles d'accès
topic-legacy: troubleshooting guide
description: Ce document répond aux questions fréquentes sur le contrôle d’accès dans Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 68%

---

# Guide de dépannage du contrôle d’accès

Ce document répond aux questions fréquentes sur le contrôle d’accès dans Adobe Experience Platform. Pour toute question ou dépannage concernant d&#39;autres services [!DNL Platform], consultez le [guide de dépannage Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] exploite les profils de produit dans [Adobe Admin Console](http://adminconsole.adobe.com) pour fournir des contrôles d’accès en fonction du rôle, en liant les utilisateurs à des autorisations et des environnements de test.  Pour plus d’informations, consultez la [présentation du contrôle d’accès](home.md).

## Où puis-je trouver mes autorisations d’accès actuelles ?

Si vous êtes un administrateur système, un administrateur de produit ou un administrateur de profils de produit pour votre organisation IMS, vous pouvez afficher le profil de produit qui vous a été attribué et les autorisations qu’il accorde dans Adobe Admin Console. Consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md) pour obtenir des instructions sur la navigation dans afin d’afficher les autorisations d’un profil de produit.[!DNL Admin Console]

Si vous n’êtes pas un administrateur, vous pouvez tout de même consulter vos autorisations d’accès actuelles en envoyant une requête sur le point de terminaison `/acl/effective-policies` dans l’API Access Control. Pour plus d’informations, consultez la section « Affichage des stratégies efficaces » du [guide de développement du contrôle d’accès](./api/effective-policies.md).

## Certaines fonctionnalités de l&#39;interface utilisateur [!DNL Platform] ne sont pas disponibles. Comment les autorisations contrôlent-elles l’accès à ces fonctionnalités ?

Si vous ne disposez pas des autorisations d&#39;accès pour une fonction [!DNL Platform] particulière, cette fonction sera masquée ou grisée dans l&#39;interface utilisateur [!DNL Experience Platform]. Par exemple, pour vue à l’onglet &quot;[!UICONTROL Profils]&quot;, vous devez disposer des autorisations &quot;[!UICONTROL Profils de Vue]&quot; ou &quot;[!UICONTROL Gérer les Profils]&quot;. Contactez votre administrateur si vous avez besoin d&#39;autorisations supplémentaires pour les fonctionnalités [!DNL Experience Platform].

## Comment les autorisations sont-elles regroupées et quel groupe contient l’autorisation que je souhaite utiliser ?

Les autorisations sont regroupées et classées en fonction des capacités [!DNL Platform] auxquelles elles s&#39;appliquent (par exemple [!DNL Data Management] et [!DNL Profile Management]). Pour obtenir une liste complète des autorisations disponibles et des groupes auxquels elles appartiennent, consultez la [section des autorisations](home.md#permissions) dans la présentation du contrôle d’accès.

Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez la [présentation du contrôle d’accès](home.md).
