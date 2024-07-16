---
solution: Experience Platform
title: Limites connues des livres de lecture
description: En savoir plus sur les problèmes connus et les problèmes courants liés aux playbooks et comment les résoudre
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Limites connues {#known-limitations}

Découvrez comment résoudre les erreurs lors de l’utilisation de classeurs de cas d’utilisation et comprendre les limites connues de la version de disponibilité générale.

## Limites connues

Deux limites connues s’affichent lorsque vous créez une instance d’un playbook et que vous générez des ressources.

* Pour les schémas générés, si un schéma est généré dans une instance d’un playbook et que vous le modifiez, un autre schéma *n’est pas généré si vous activez une autre instance du playbook.* Continuez également à utiliser le schéma que vous avez modifié dans l’instance.

* Lors de l’utilisation de la [fonctionnalité de sensibilisation aux données](/help/use-case-playbooks/playbooks/data-awareness.md) pour promouvoir le schéma de l’environnement de test d’inspiration vers l’environnement de test de développement, vous pouvez voir des erreurs similaires à celles ci-dessous :

![Erreurs affichées dans le workflow de mappage de schéma.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

En effet, certains des champs générés à partir de votre schéma ne sont pas présents dans le schéma de l’environnement de test de développement vers lequel vous effectuez la copie. Cherchez ces champs. Ensuite, revenez à l’environnement de test de développement dans lequel vous pouvez :

* Créez un groupe de champs qui comprend ces champs ou
* Incluez dans votre schéma un groupe de champs standard prédéfini qui inclut les champs manquants.

Une fois que vous avez inclus ces champs dans le schéma dans l’environnement de test de développement, revenez au workflow pour copier les champs de schéma de l’environnement de test d’inspiration vers l’environnement de test de développement. Les erreurs ont maintenant disparu.

Pour plus d’informations, regardez la vidéo ci-dessous pour créer des groupes de champs de schéma.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
