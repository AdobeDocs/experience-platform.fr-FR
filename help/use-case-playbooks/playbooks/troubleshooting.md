---
solution: Experience Platform
title: Limites connues et résolution des problèmes liés aux livres de lecture
description: En savoir plus sur les problèmes connus et les problèmes courants liés aux playbooks et comment les résoudre
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# Dépannage et limites connues {#troubleshooting-known-limitations}

## Dépannage {#troubleshooting}

### Surfaces Adobe Journey Optimizer non configurées

Lors de la création d’une instance d’un playbook, le message ci-dessous peut s’afficher.

![Dépannage](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Cela est dû au fait que les playbooks Journey Optimizer créent des messages pour les canaux email, push et SMS. Lisez la section [prise en main](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) pour configurer les différentes surfaces.

### État *failed* lors de la création d’une instance

Si un message d’échec s’affiche lorsque vous essayez de créer une instance, cela peut être dû au fait que votre administrateur ne vous a pas accordé les autorisations utilisateur requises. Un playbook contient de nombreuses ressources différentes et votre utilisateur a besoin d’autorisations pour créer ces ressources afin de pouvoir créer correctement l’instance du playbook. Voir [permissions](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) de ce guide sur la configuration des autorisations.

## Limites connues

Deux limites connues s’affichent lorsque vous créez une instance d’un playbook et que vous générez des ressources.

* Pour les schémas générés, si un schéma est généré dans une instance d’un playbook et que vous le modifiez, alors un autre schéma *will not* est généré si vous activez une autre instance du playbook. Continuez également à utiliser le schéma que vous avez modifié dans l’instance.

* Lors de l’utilisation de la variable [fonctionnalité de sensibilisation aux données](/help/use-case-playbooks/playbooks/data-awareness.md) pour promouvoir le schéma de l’environnement de test d’inspiration vers l’environnement de test de développement, vous pouvez voir des erreurs similaires à celles ci-dessous :

![schema-errors](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

En effet, certains des champs générés à partir de votre schéma ne sont pas présents dans le schéma de l’environnement de test de développement vers lequel vous effectuez la copie. Cherchez ces champs. Ensuite, revenez à l’environnement de test de développement dans lequel vous pouvez :

* Créez un groupe de champs qui comprend ces champs ou
* Incluez dans votre schéma un groupe de champs standard prédéfini qui inclut les champs manquants.

Une fois que vous avez inclus ces champs dans le schéma dans l’environnement de test de développement, revenez au workflow pour copier les champs de schéma de l’environnement de test d’inspiration vers l’environnement de test de développement. Les erreurs ont maintenant disparu.

Pour plus d’informations, regardez la vidéo ci-dessous pour créer des groupes de champs de schéma.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
