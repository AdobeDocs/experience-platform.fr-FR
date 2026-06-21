---
solution: Experience Platform
title: Limites connues des playbooks
description: Découvrez les problèmes connus et courants des playbooks et comment les résoudre
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# Limites connues {#known-limitations}

Découvrez comment résoudre les erreurs lors de l’utilisation des playbooks de cas d’utilisation et comprendre les limites connues de la version de disponibilité générale.

## Limites connues

Certaines limites connues s’affichent lorsque vous créez une instance d’un playbook et que vous générez des ressources.

* Pour les schémas générés, si un schéma est généré dans une instance d’un playbook et que vous le modifiez, un autre schéma *ne le sera pas* n’est pas généré si vous activez une autre instance du playbook. Au lieu de cela, continuez à utiliser le schéma que vous avez modifié dans l’instance.

* Lors de l’utilisation de la [fonctionnalité de reconnaissance des données](/help/use-case-playbooks/playbooks/data-awareness.md) pour promouvoir le schéma du sandbox d’inspiration au sandbox de développement, vous pouvez voir des erreurs similaires à celles-ci :

![Erreurs affichées dans le workflow de mappage de schéma.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

En effet, certains des champs générés à partir de votre schéma ne sont pas présents dans le schéma du sandbox de développement vers lequel vous effectuez une copie. Recherchez ce que sont ces champs. Revenez ensuite au sandbox de développement où vous pouvez :

* Créez un groupe de champs qui inclut ces champs ou
* Incluez dans votre schéma un groupe de champs standard prédéfini qui comprend les champs manquants.

Après avoir inclus ces champs dans le schéma dans le sandbox de développement, revenez au workflow pour copier les champs de schéma du sandbox d’inspiration vers le sandbox de développement. Les erreurs ont maintenant disparu.

Pour plus d’informations, regardez la vidéo ci-dessous pour créer des groupes de champs de schéma.

>[!VIDEO](https://video.tv.adobe.com/v/3413606/?captions=fre_fr&learn=on)
