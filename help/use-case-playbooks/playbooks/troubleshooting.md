---
solution: Experience Platform
title: Limites connues et résolution des problèmes liés aux playbooks
description: Découvrez les problèmes connus et courants des playbooks et comment les résoudre
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Résolution des problèmes {#troubleshooting}

Afficher les suggestions de dépannage pour les erreurs courantes lors de l’utilisation des playbooks de cas d’utilisation

## Surfaces Adobe Journey Optimizer non configurées {#surfaces-not-configured}

Lors de la création d’une instance d’un playbook, il se peut que le message ci-dessous s’affiche.

![Dépannage](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

En effet, les playbooks Journey Optimizer créent des messages pour les canaux e-mail, push et SMS. Lisez le guide [prise en main](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) pour configurer les différentes surfaces.

## Statut *échec* lors de la création d’une instance {#status-failed}

Si un message d’échec s’affiche lorsque vous essayez de créer une instance, cela peut être dû au fait que votre administrateur ne vous a pas accordé les autorisations utilisateur requises. Un playbook contient de nombreuses ressources différentes et votre utilisateur a besoin d’autorisations pour créer ces ressources afin de pouvoir créer l’instance du playbook avec succès. Voir la section [autorisations](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) de ce guide sur la configuration des autorisations.

## Échec de l’importation {#import-failure}

Les clients opèrent dans différents environnements de test et parfois, lors de l’importation d’une instance de leur environnement vers le sandbox Adobe, elle peut échouer. Pour afficher le statut de ces imports, sélectionnez Sandbox dans le volet de navigation de gauche, puis sélectionnez Tâches. Vous pouvez y afficher tous les détails des fichiers importés. Sélectionnez un fichier dont le statut est En échec , puis sélectionnez Afficher les détails de la tâche. Une boîte de dialogue modale s’affiche. Sélectionnez Afficher le fichier JSON , faites défiler l’écran vers le bas et copiez le message d’erreur qui s’affiche sous « messages ». Il est tout à fait possible que plusieurs messages d’erreur s’affichent, alors veillez à tous les copier. Envoyez-les à votre équipe Adobe lors de la tentative de journalisation d’un ticket de bogue. Cela permet d’accélérer le processus de résolution et de donner à votre équipe plus de contexte sur ce qui se passe.
