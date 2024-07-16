---
solution: Experience Platform
title: Créer, partager et réutiliser des instances de playbook
description: Découvrez comment créer, partager et réutiliser des instances de playbook pour réaliser votre cas d’utilisation marketing.
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 81%

---

# Créer, partager et réutiliser des instances de playbook

Pour utiliser un playbook, accédez à **[!UICONTROL Playbooks de cas d’utilisation] > [!UICONTROL Playbooks]**. Parcourez et utilisez les différentes options de recherche et de filtrage de la page pour sélectionner et commencer à utiliser un playbook spécifique.

## Créer une instance de playbook {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="Créer une instance"
>abstract="Générez une liste de ressources telles que des parcours, des audiences, des schémas ou des destinations à utiliser dans des scénarios de parcours ou d’activation."

Avant de créer une instance de playbook, explorez les playbooks disponibles pour [choisir le playbook approprié](/help/use-case-playbooks/playbooks/choose.md). Lorsque vous êtes prêt(e) à poursuivre un playbook et à créer une instance, sélectionnez **[!UICONTROL Créer une instance]** pour poursuivre le playbook et générer des ressources techniques.

![Créer une instance d’un playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Cette action génère plusieurs ressources que vous pouvez utiliser pour réaliser le cas d’utilisation décrit par le playbook.

![Vue Playbook des ressources générées après activation.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Utilisez les commandes de configuration pour modifier les noms et les descriptions des instances. {#edit-instance-metadata}

Après avoir créé une instance basée sur un playbook, vous pouvez la personnaliser pour la différencier des autres instances créées à partir du même playbook. Sélectionnez la commande de configuration tel qu’indiqué ci-dessous. Modifiez le nom, la description et les notes, puis sélectionnez **[!UICONTROL Enregistrer]** lorsque vous avez terminé.

![Modifier le nom et la description d’une instance.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Comprendre les ressources générées {#understand-assets}

>[!IMPORTANT]
>
>Ne vous inquiétez pas ! Il s’agit d’un espace sûr pour faire des expériences et vous n’allez rien casser. Aucune donnée n’est encore associée aux ressources que vous créez. Vous devez d’abord ingérer des données pour réaliser les cas d’utilisation.

Il est important de comprendre que les ressources générées varient selon le cas d’utilisation que vous activez :

* Différentes ressources sont générées pour différents types de playbooks. Ces ressources sont créées spécifiquement pour le cas d’utilisation réalisé via le playbook. Par exemple, un playbook génère un schéma, une audience, un parcours et des messages. Un autre playbook génère un schéma, une audience et une destination vers laquelle activer les données.
* Les ressources elles-mêmes varient d’un playbook à l’autre. Par exemple, pour le playbook **[!UICONTROL Envoyer un message d’anniversaire aux clients/clientes]**, l’audience créée comporte la règle `birthday=today AND year=any`.

À titre d’exemple, pour le playbook **[!UICONTROL Panier abandonné : contenu]**, vous pouvez constater qu’un parcours spécifique est créé et contient les messages créés pour ce cas d’utilisation.

![Parcours créé à partir du playbook de cas d’utilisation.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Utiliser et modifier les ressources générées {#use-and-edit-assets}

Lorsque vous explorez les ressources qui sont générées après avoir créé une instance d’un playbook, vous pouvez modifier n’importe quelle ressource créée.

Si vous ou un membre de votre équipe créez une autre instance du playbook, les ressources modifiées sont conservées et de nouvelles ressources sont créées pour la nouvelle instance du playbook.

Le comportement décrit ci-dessus est valable pour toutes les ressources qui sont créées, à l’exception des schémas. Dans le cas des schémas, les nouveaux schémas ne sont pas créés lorsqu’une nouvelle instance d’un playbook est créée. Vous allez donc utiliser le schéma modifié à partir d’une autre instance du playbook dans l’instance qui vient d’être créée.

>[!TIP]
>
>Effectuez des tests dans le sandbox de développement et passez en production lorsque vous êtes prêt(e).
>
>Une fois les objets générés, vous pouvez continuer à les tester dans les sandbox de développement en y rajoutant des données. Vous pouvez tester les ressources tant que vous le souhaitez dans l’environnement de test de développement et vous pouvez répliquer la logique des ressources (définitions d’audience, parcours, schémas, etc.) dans l’environnement de test de production lorsque vous êtes prêt. Vous pouvez passer à l’environnement de test de développement, puis à l’environnement de test de production à l’aide de la [fonctionnalité de sensibilisation aux données](/help/use-case-playbooks/playbooks/data-awareness.md).

## Réutiliser des playbooks {#reuse-playbooks}

En créant plusieurs instances du même playbook, vous pouvez mettre en œuvre le même cas d’utilisation ultérieurement, et ce sans modifier les détails de votre mise en œuvre précédente du cas d’utilisation.

## Partager un playbook et des ressources générées avec d’autres membres de l’équipe {#share-playbook}

Vous pouvez partager l’instance et les ressources générées avec d’autres membres de l’équipe. Pour ce faire, copiez le lien URL du navigateur et partagez-le avec votre équipe afin de lui donner un aperçu des ressources générées.

![URL mise en surbrillance dans une vue playbook de cas d’utilisation.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Présentation vidéo du processus de lecture de bout en bout

Regardez cette vidéo pour découvrir, créer, publier et dépanner des instances d’un manuel de cas d’utilisation de bout en bout, ainsi que pour copier les ressources générées par le manuel dans d’autres environnements de test configurés dans votre entreprise.

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## Étapes suivantes {#next-steps}

Après avoir lu ce guide et celui sur la découverte du playbook approprié, vous savez maintenant comment interpréter les différentes sections d’un playbook et comment utiliser les ressources qui sont générées après avoir créé une instance d’un playbook.

Vous pouvez maintenant parcourir le catalogue des playbooks pour trouver le bon playbook à utiliser et lire le [guide de dépannage](/help/use-case-playbooks/playbooks/troubleshooting.md) si vous rencontrez des problèmes.
