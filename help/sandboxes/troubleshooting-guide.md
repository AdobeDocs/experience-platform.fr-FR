---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage des sandbox
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba

---


# Guide de dépannage des sandbox

Ce répond aux questions les plus fréquentes sur les sandbox dans Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services de plateforme, reportez-vous au guide [de dépannage de](../landing/troubleshooting.md)la plateforme d’expérience.

Les sandbox partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique. See the [sandboxes overview](home.md) for more information.

## Qu&#39;est-ce qu&#39;un sandbox ?

Les sandbox sont des partitions virtuelles au sein d’une seule instance de la plateforme d’expérience. Chaque sandbox conserve sa propre bibliothèque indépendante de ressources de plateforme (y compris les  de, les jeux de données, les, les , etc.). Tout le contenu et les actions entreprises dans un sandbox sont limités à ce sandbox et n’affectent aucun autre sandbox. See the [sandboxes overview](home.md) for more information.

## Quels types de sandbox sont disponibles et quelles sont leurs différences ?

Il existe deux types de sandbox dans la plateforme d’expérience :

* Sandbox de production
* Sandbox hors production

Experience Platform fournit un sandbox **de** production unique, qui ne peut pas être supprimé ni réinitialisé. Un seul sandbox de production peut exister pour une instance de plateforme unique.

En revanche, plusieurs sandbox **de** non production peuvent être créés par les administrateurs de sandbox pour une instance de plateforme unique. Les sandbox hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. En outre, les sandbox hors production disposent d’une fonction de réinitialisation qui supprime toutes les ressources créées par les clients du sandbox. Les sandbox hors production ne peuvent pas être convertis en sandbox de production.

See the [sandboxes overview](./home.md) for more information.

## Puis-je accéder à une ressource à partir de plusieurs sandbox ?

Les sandbox sont des partitions isolées d’une instance de plateforme unique, chaque sandbox conservant sa propre bibliothèque indépendante de ressources. Une ressource qui existe dans un sandbox n’est accessible à partir d’aucun autre sandbox, quel que soit le type de sandbox (production ou non-production).

## Combien de sandbox de production puis-je avoir ?

Experience Platform ne prend en charge qu’un seul sandbox de production par organisation IMS, qui est fourni prêt à l’emploi. Bien que le sandbox de production puisse être renommé, il ne peut pas être supprimé ni réinitialisé. Les utilisateurs disposant des autorisations d’administration de sandbox peuvent uniquement créer, réinitialiser et supprimer des sandbox hors production.

## Combien de sandbox hors production puis-je avoir ?

Experience Platform permet actuellement à 15 sandbox hors production d’être actifs au sein d’une seule organisation IMS.

## Je viens de créer un sandbox. Comment définir les autorisations pour les utilisateurs qui vont travailler avec ce sandbox ?

La console d’administration Adobe associe les utilisateurs aux sandbox et aux autorisations grâce à l’utilisation des **de produits**. Après avoir créé un nouveau sandbox, accédez à l’onglet _Autorisations_ du de produits auquel vous souhaitez accorder l’accès, puis cliquez sur **Sandbox**. A partir de là, vous pouvez ajouter ou supprimer l’accès au nouveau sandbox de la même manière que les autres autorisations.

Si vous souhaitez ajouter des autorisations uniques aux utilisateurs d’un sandbox particulier, vous devrez peut-être créer un nouveau de produits auquel seront appliqués les sandbox et les autorisations appropriées, puis affecter ces utilisateurs à ce .

Pour plus d’informations sur la gestion des sandbox et des autorisations dans la Console d’administration, reportez-vous au guide [de l’utilisateur des ](../access-control/ui/overview.md) .