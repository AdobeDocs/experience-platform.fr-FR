---
solution: Experience Platform
title: Limites connues et résolution des problèmes liés aux livres de lecture
description: En savoir plus sur les problèmes connus et les problèmes courants liés aux playbooks et comment les résoudre
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Dépannage {#troubleshooting}

Affichage des suggestions de dépannage pour les erreurs courantes lors de l’utilisation de classeurs de cas d’utilisation

## Surfaces Adobe Journey Optimizer non configurées {#surfaces-not-configured}

Lors de la création d’une instance d’un playbook, le message ci-dessous peut s’afficher.

![Dépannage](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Cela est dû au fait que les playbooks Journey Optimizer créent des messages pour les canaux email, push et SMS. Lisez la section [prise en main](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) pour configurer les différentes surfaces.

## État *failed* lors de la création d’une instance {#status-failed}

Si un message d’échec s’affiche lorsque vous essayez de créer une instance, cela peut être dû au fait que votre administrateur ne vous a pas accordé les autorisations utilisateur requises. Un playbook contient de nombreuses ressources différentes et votre utilisateur a besoin d’autorisations pour créer ces ressources afin de pouvoir créer correctement l’instance du playbook. Voir [permissions](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) de ce guide sur la configuration des autorisations.

## Échec de l’importation {#import-failure}

Les clients opèrent dans différents environnements de test et, parfois, lors de l’importation d’une instance de leur environnement vers l’environnement de test d’Adobe, cela peut échouer. Pour afficher l’état de ces importations, sélectionnez Environnement de test dans le volet de navigation de gauche, puis Tâches. Vous pouvez y afficher tous les détails des fichiers importés. Sélectionnez un fichier dont l’état a échoué, puis cliquez sur Afficher les détails de la tâche. Un modal s’affiche. Sélectionnez Afficher le fichier JSON, faites défiler l’écran vers le bas et copiez le message d’erreur qui apparaît sous &quot;messages&quot;. Il est tout à fait possible que plusieurs messages d’erreur s’affichent. Vous devez donc tous les copier. Envoyez-les à votre équipe d’Adobe en essayant de consigner un ticket de bogue. Cela accélère le processus de résolution et donne à votre équipe plus de contexte sur ce qui se passe.
