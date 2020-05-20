---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage des Contrôles d'accès
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Guide de dépannage des Contrôles d&#39;accès

Ce document fournit des réponses aux questions fréquentes sur le contrôle d&#39;accès dans Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services de plate-forme, reportez-vous au guide [de dépannage de](../landing/troubleshooting.md)Experience Platform.

Experience Platform tire parti des profils de produits de la Console [d’administration](http://adminconsole.adobe.com) Adobe pour fournir un **contrôle d&#39;accès** basé sur les rôles, en liant les utilisateurs à des autorisations et des sandbox.  See the [access control overview](home.md) for more information.

## Où puis-je trouver mes autorisations d’accès actuelles ?

Si vous êtes un administrateur système, un administrateur de produit ou un administrateur de profil de produit pour votre organisation IMS, vous pouvez vue le profil de produit qui vous a été attribué et les autorisations qu’il fournit dans Adobe Admin Console. Consultez le guide [d&#39;utilisation du](./ui/overview.md) contrôle d&#39;accès pour savoir comment accéder à la Console d&#39;administration pour vue des autorisations d&#39;un profil de produits.

Si vous n’êtes pas un administrateur, vous pouvez toujours vue vos autorisations d’accès actuelles en envoyant une demande au point de `/acl/effective-policies` terminaison dans l’API de Contrôle d&#39;accès. Pour plus d&#39;informations, consultez la section &quot;Stratégies efficaces en matière de Vue&quot; du guide [des développeurs de](./api/effective-policies.md) contrôles d&#39;accès.

## Certaines fonctionnalités de l’interface utilisateur de la plate-forme ne sont pas disponibles. Comment l&#39;accès à ces fonctionnalités est-il contrôlé par les autorisations ?

Si vous ne disposez pas des autorisations d’accès pour une fonction de plateforme particulière, cette fonction sera masquée ou grisée dans l’interface utilisateur de la plate-forme d’expérience. Par exemple, pour vue à l’onglet &quot;Profils&quot;, vous devez disposer des autorisations &quot;Profils de Vue&quot; ou &quot;Gérer les Profils&quot;. Contactez votre administrateur si vous avez besoin d’autorisations supplémentaires pour les fonctionnalités de la plate-forme d’expérience.

## Comment les autorisations sont-elles regroupées et quel groupe contient l’autorisation que je souhaite utiliser ?

Les autorisations sont regroupées et classées en fonction des capacités de la plateforme auxquelles elles s’appliquent (telles que la gestion des Datas Management et des Profils). Pour obtenir une liste complète des autorisations disponibles et des groupes auxquels elles appartiennent, voir la section [](home.md#permissions) permissions dans l’aperçu du contrôle d&#39;accès.

Pour plus d’informations sur la fourniture d’un contrôle d&#39;accès basé sur les rôles, consultez la présentation [des](home.md) contrôles d&#39;accès.