---
title: Norme de rétrocompatibilité
description: Découvrez la norme de rétrocompatibilité dans Adobe Experience Platform, qui garantit que les versions mises à jour des extensions de balises sont compatibles avec les versions précédentes.
exl-id: 325390f1-88c7-4b9e-a484-5442ca649bdf
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 100%

---

# Norme de rétrocompatibilité

Les mises à jour dʼune extension de balise dans Adobe Experience Platform doivent être rétrocompatibles avec les versions précédentes de lʼextension. Cela signifie que :

* Toute modification des composants principaux des extensions doit être compatible avec les versions précédentes. Cela inclut la configuration de l’extension, les types d’événement, les types de condition, les types d’action, les types d’éléments de données et les modules partagés.
* Les composants qu’un utilisateur a créés avec l’ancienne version de l’extension doivent être en mesure de transmettre la validation par rapport aux schémas fournis par la nouvelle version.
* Un utilisateur dʼAdobe Experience Platform doit pouvoir installer une version mise à jour de votre extension et faire en sorte que tout ce quʼil a fait continue à fonctionner exactement comme précédemment avant dʼeffectuer des modifications délibérées.

## Modifications autorisées

Les types de modifications suivants apportés à votre extension sont autorisés :

1. Vous pouvez ajouter de nouveaux composants (types d’événement, types de condition, etc.).
1. Vous pouvez ajouter de nouveaux champs facultatifs à vos paramètres de configuration des extensions.
1. Vous pouvez transformer les champs obligatoires en champs facultatifs.

## Modifications interdites

Les types de modifications suivants apportés à votre extension ne sont pas autorisés :

1. Vous ne pouvez pas renommer un composant.
1. Vous ne pouvez pas supprimer un composant.
1. Vous ne pouvez pas supprimer un champ d’un composant.
1. Vous ne pouvez pas remplacer les champs facultatifs par des champs obligatoires.
1. Vous ne pouvez pas ajouter de nouveaux champs obligatoires.
1. Vous ne pouvez pas modifier l’API des modules partagés existants.

Si vous effectuez l’une de ces modifications, toute personne ayant installé votre extension dans sa propriété commencera immédiatement à rencontrer des problèmes tels que :

* Les règles ne s’affichent plus correctement, car l’un des composants de règle recherche un composant qui n’existe pas.
* Toutes les versions échouent car la bibliothèque contient une ressource en amont qui n’existe plus sur l’extension.
* Toutes les versions échouent car la bibliothèque inclut une ressource dont les paramètres ne sont pas validés par rapport au nouveau schéma.

En particulier dans ce deuxième cas, les utilisateurs peuvent être laissés sans recours et sans moyen de réparer leur propriété pour pouvoir publier à nouveau.

## Suppression des fonctionnalités

Il peut y avoir des cas où vous avez une raison commerciale valable de penser que vous avez vraiment besoin de faire un changement interdit (répertoriés ci-dessus). Vous ne pouvez toujours pas le faire, mais voici ce que vous pouvez faire à la place :

1. Je veux supprimer un composant => Créer un nouveau composant et abandonner l’ancien.
1. Je veux supprimer un champ d’un composant => Créer un nouveau composant avec ce champ supprimé et abandonner l’ancien.
1. Je souhaite modifier un champ facultatif pour qu’il soit obligatoire => Créer un nouveau composant nécessitant le champ souhaité et abandonner l’ancien
1. Je veux modifier l’API d’un module partagé => Créer un nouveau module partagé et abandonner l’ancien

Il se peut que vous remarquiez un point commun. Tant mieux. Lors de l’abandon d’un ancien composant, vous devez informer les utilisateurs de votre extension que celui-ci a été abandonné et qu’ils doivent passer à un nouveau composant.  Quelques suggestions pour communiquer avec les utilisateurs :

* Mettez à jour le nom d’affichage de l’ancien composant pour inclure « (Obsolète) ».
* Mettez à jour la vue de l’ancien composant pour qu’elle contienne un texte d’avertissement rouge indiquant que ce composant est obsolète et que l’utilisateur devrait passer au nouveau composant.
* Mettez à jour le code de votre module pour consigner les avis d’abandon dans la console. Gardez à l’esprit que les utilisateurs finaux les liront. Par conséquent, mieux vaut faire en sorte qu’ils restent clairs et quelque peu génériques.
* Envoyez des emails conviviaux depuis votre système CRM.

Lorsque l’ancienne fonctionnalité n’est pas seulement indésirable, mais n’existe plus dans votre solution, il existe une étape supplémentaire que vous pouvez effectuer - mais vous ne devez le faire qu’après avoir averti vos utilisateurs et leur avoir donné le temps d’effectuer la mise à jour.

* Mettez à jour le contenu de votre module pour qu’il ne fasse rien. Cette opération supprimera la fonctionnalité de la bibliothèque déployée de l’utilisateur lors de la prochaine version, mais n’enfreindra aucune de ses règles ou versions.

### Restauration des fonctionnalités supprimées

Si vous avez déjà supprimé la fonctionnalité et que les utilisateurs vous disent que ça ne fonctionne pas, vous devez publier une nouvelle version de votre extension qui restaure les composants que vous avez supprimés.

Leur restauration dans un état obsolète comme décrit ci-dessus est acceptable, mais ils doivent exister.

Par exemple, supposons que vous ayez une version 1.0 avec le composant XYZ que les gens utilisent. Ensuite, vous lancez une version 1.1 qui ne contient plus le composant XYZ. Vos utilisateurs vous disent que votre extension a endommagé leurs propriétés et que vous devez la réparer. Vous devez sortir une version 1.2 qui ramènera le composant XYZ (peut-être dans un état obsolète, c’est à vous de décider) et demander à vos utilisateurs d’effectuer une mise à niveau vers la version 1.2 pour que les choses fonctionnent à nouveau.
