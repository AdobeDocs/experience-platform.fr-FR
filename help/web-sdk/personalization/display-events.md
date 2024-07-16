---
title: Gestion des événements d’affichage dans le SDK Web
description: Cet article explique ce que sont les événements d’affichage et comment les utiliser dans le SDK Web.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Gestion des événements d’affichage dans le SDK Web

Les événements d’affichage sont utilisés par le SDK Web pour informer votre service de personnalisation ou d’analyse lorsqu’un contenu de personnalisation spécifique est affiché sur une page.

L’envoi d’événements d’affichage améliore la précision des mesures de personnalisation et vous donne un aperçu précis de ce que voient les utilisateurs sur votre page.

Le SDK Web vous permet d’envoyer des événements d’affichage de deux manières :

* [Automatically](#send-automatically), immédiatement après le rendu du contenu personnalisé sur la page. Pour plus d’informations, consultez la documentation sur la [personnalisation du rendu du contenu](rendering-personalization-content.md) .
* [Manuellement](#send-sendEvent-calls), par le biais des appels `sendEvent` suivants.

>[!NOTE]
>
>Les événements d’affichage ne sont pas envoyés automatiquement lors de l’appel de la fonction `applyPropositions`.

## Envoi automatique des événements d’affichage {#send-automatically}

L’envoi d’événements d’affichage fournit automatiquement des mesures d’analyse plus précises, car l’événement est envoyé immédiatement après le chargement de la personnalisation. Cette mise en oeuvre comporte également une méthode de mise en oeuvre plus simplifiée.

Pour envoyer automatiquement des événements d&#39;affichage après le rendu du contenu personnalisé sur la page, vous devez configurer les paramètres suivants :

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` ou non spécifié

Le SDK Web envoie les événements d’affichage immédiatement après le rendu d’une personnalisation suite à un appel `sendEvent`.

## Envoi d’événements d’affichage dans les appels sendEvent suivants {#send-sendEvent-calls}

Par rapport à l’envoi d’événements d’affichage [automatique](#send-automatically), lorsque vous les incluez dans les appels `sendEvent` suivants, vous avez également la possibilité d’inclure plus d’informations sur le chargement de la page dans l’appel . Il peut s’agir d’informations supplémentaires, qui n’étaient pas disponibles lors de la demande du contenu personnalisé.

De plus, l’envoi d’événements d’affichage dans les appels `sendEvent` minimise les erreurs de taux de rebond lors de l’utilisation d’Adobe Analytics.

>[!IMPORTANT]
>
>Lors de l’utilisation de propositions générées manuellement, les événements d’affichage ne sont pris en charge que par des appels `sendEvent`. Dans ce cas, vous ne pouvez pas envoyer automatiquement des événements d’affichage.

### Envoi d’événements d’affichage pour les propositions générées automatiquement {#auto-rendered-propositions}

Pour envoyer des événements d’affichage pour les propositions générées automatiquement, vous devez configurer les paramètres suivants dans l’appel `sendEvent` :

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` pour l’accès en haut de la page

Pour envoyer les événements d’affichage, appelez `sendEvent` avec `personalization.includePendingDisplayNotifications: true`

### Envoyer des événements d’affichage pour les propositions générées manuellement {#manually-rendered-propositions}

Pour envoyer des événements d’affichage pour les propositions générées manuellement, vous devez les inclure dans le champ XDM `_experience.decisioning.propositions`, y compris les champs `id`, `scope` et `scopeDetails` des propositions.

De plus, définissez le champ `include _experience.decisioning.propositionEventType.display` sur `1`.
