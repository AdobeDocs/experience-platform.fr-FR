---
solution: Experience Platform
title: Créer, partager et réutiliser des instances de playbook
description: Découvrez comment créer, partager et réutiliser des instances de playbook pour réaliser votre cas d’utilisation marketing.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 51e4a77472ccb560dbfa5f56011ce50932d87b64
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# (Version bêta) Créer, partager et réutiliser des instances de playbook

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Pour utiliser un manuel, accédez à **[!UICONTROL Cas d’utilisation des classeurs] > [!UICONTROL Livres]**. Parcourez et utilisez les différentes options de recherche et de filtrage de la page pour sélectionner et commencer à utiliser un playbook spécifique.

## Création d’une instance de livre de lecture {#create-playbook-instance}

Avant de créer une instance de playbook, explorez les classeurs disponibles à la rubrique [découvrez le bon playbook pour vous](/help/use-case-playbooks/playbooks/discover.md). Lorsque vous êtes prêt à poursuivre un playbook et à créer une instance, sélectionnez **[!UICONTROL Créer une instance]** pour poursuivre le playbook et générer des ressources techniques.

![Créez une instance d’un playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Cette action génère plusieurs ressources que vous pouvez utiliser pour réaliser le cas d’utilisation décrit par le playbook.

![Vue Playbook des ressources générées après activation.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Utilisez les commandes de configuration pour modifier les noms et descriptions des instances. {#edit-instance-metadata}

Après avoir créé une instance basée sur un playbook, vous pouvez la personnaliser pour la distinguer des autres instances créées à partir du même playbook. Sélectionnez le contrôle de configuration comme illustré ci-dessous. Modifiez le nom, la description et les notes, puis sélectionnez **[!UICONTROL Enregistrer]** lorsque vous avez terminé.

![Modifiez le nom et la description d’une instance.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Présentation des ressources générées {#understand-assets}

>[!IMPORTANT]
>
>Pas besoin de vous inquiéter ! C&#39;est un espace sûr pour expérimenter et vous ne pouvez rien casser. Aucune donnée n’est encore associée aux ressources que vous créez. Vous devez d’abord ingérer des données pour réaliser les cas d’utilisation.

Il est important de comprendre que les ressources générées diffèrent selon le cas d’utilisation que vous activez :

* Différentes ressources sont générées pour différents types de livres de lecture. Ces ressources sont créées spécifiquement pour le cas d’utilisation réalisé via le manuel de lecture. Par exemple, un playbook génère un schéma, un segment, un parcours et des messages. Un autre playbook génère un schéma, un segment et une destination vers lesquels activer les données.
* Les ressources elles-mêmes diffèrent d’un playbooks à l’autre. Par exemple, pour la variable **[!UICONTROL Envoyer Un Message D’Anniversaire Aux Invités]** playbook, l’audience créée comporte la règle `birthday=today AND year=any`.

Pour illustrer un exemple, pour le **[!UICONTROL Panier abandonné : Marchandisage]** playbook, vous pouvez constater qu’un parcours spécifique est créé et contient les messages créés pour ce cas d’utilisation.

![Parcours créé à partir du scénario d’utilisation.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Utilisation et modification des ressources générées {#use-and-edit-assets}

Lorsque vous explorez les ressources qui sont générées après avoir créé une instance d’un playbook, vous pouvez modifier l’une des ressources créées.

Si vous ou un membre de votre équipe créez une autre instance du playbook, les ressources modifiées sont conservées et de nouvelles ressources sont créées pour la nouvelle instance du playbook.

Le comportement décrit ci-dessus est vrai pour toutes les ressources qui sont créées, à l’exception des schémas. Dans le cas des schémas, les nouveaux schémas ne sont pas créés lorsqu’une nouvelle instance d’un playbook est créée. Vous allez donc utiliser le schéma modifié d’une autre instance du playbook dans l’instance nouvellement créée.

>[!TIP]
>
>Testez dans l’environnement de test de développement et passez en production lorsque vous êtes prêt.
>
>Une fois les objets générés, vous pouvez continuer à les tester dans les environnements de test de développement en ajoutant des données. Vous pouvez tester les ressources tant que vous le souhaitez dans l’environnement de test de développement et vous pouvez répliquer la logique des ressources (définitions de segment, parcours, schémas, etc.) dans l’environnement de test de production lorsque vous êtes prêt.

### Réutilisation des classeurs {#reuse-playbooks}

En créant plusieurs instances du même playbook, vous pouvez mettre en oeuvre le même cas d’utilisation ultérieurement, sans modifier les détails de votre mise en oeuvre précédente du cas d’utilisation.

### Partage du playbook et des ressources générées avec d’autres membres de l’équipe {#share-playbook}

Vous pouvez partager l’instance et les ressources générées avec d’autres membres de l’équipe. Pour ce faire, copiez le lien URL du navigateur et partagez-le avec votre équipe afin de leur donner un aperçu des ressources générées.

![URL mise en surbrillance dans une vue playbook de cas d’utilisation.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Étapes suivantes {#next-steps}

En lisant ce guide et celui sur la découverte du playbook approprié, vous savez maintenant comment interpréter les différentes sections d’un playbook et comment utiliser les ressources qui sont générées après avoir créé une instance d’un playbook.

Vous pouvez ensuite parcourir le catalogue des livres de jeu pour trouver le bon manuel à utiliser et lire le [guide de dépannage](/help/use-case-playbooks/playbooks/troubleshooting.md) si vous rencontrez des problèmes.