---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide de dépannage des '
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# Guide de dépannage des 

Ce répond aux questions les plus fréquentes sur l’ des dans Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services de plateforme, reportez-vous au guide [de dépannage de](../landing/troubleshooting.md)la plateforme d’expérience.

Experience Platform tire parti des  de produits dans la console [d’administration](http://adminconsole.adobe.com) Adobe pour fournir des **de** basés sur les rôles, liant les utilisateurs à des autorisations et des sandbox.  See the [access control overview](home.md) for more information.

## Où puis-je trouver mes autorisations d’accès actuelles ?

Si vous êtes un administrateur système, un administrateur de produit ou un administrateur de  de produits pour votre organisation IMS, vous pouvez  leproduit que vous avez attribué et les autorisations qu’il fournit dans la console d’administration Adobe. Voir le guide [de l’utilisateur](./ui/overview.md) pour savoir comment naviguer dans la Console d’administration pour  des autorisations de l’utilisateur d’un produit.

Si vous n’êtes pas un administrateur, vous pouvez toujours  vos autorisations d’accès actuelles en envoyant une requête au point de `/acl/effective-policies` fin dans l’API . Pour plus d&#39;informations, consultez la section &quot; stratégies efficaces&quot; du guide [des développeurs de  de](./api/effective-policies.md) .

## Certaines fonctionnalités de l’interface utilisateur de la plateforme ne sont pas disponibles. Comment l’accès à ces fonctionnalités est-il contrôlé par les autorisations ?

Si vous ne disposez pas des autorisations d’accès pour une fonctionnalité de plateforme spécifique, cette fonctionnalité sera masquée ou grisée dans l’interface utilisateur de la plateforme d’expérience. Par exemple, pour pouvoir  l’onglet &quot;&quot;, vous devez disposer des autorisations &quot; de l’&quot; ou &quot;Gérer le&quot;. Contactez votre administrateur si vous avez besoin d’autorisations supplémentaires pour les fonctionnalités de la plateforme d’expérience.

## Comment les autorisations sont-elles regroupées et quel groupe contient l’autorisation que je souhaite utiliser ?

Les autorisations sont regroupées et classées selon les capacités de la plateforme auxquelles elles s’appliquent (par exemple,  de et gestion des  de). Pour un  complet des permissions disponibles et des groupes auxquels elles appartiennent, reportez-vous à la section [](home.md#permissions) permissions dans l’ d’aperçu du.

Pour plus d’informations sur la fourniture d’ basées sur les rôles, reportez-vous à la présentation [des ](home.md) .